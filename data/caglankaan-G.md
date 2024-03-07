
### Unneeded initializations of integer variable to `0`.
In Solidity, it is common practice to initialize variables with default values when declaring them. However, initializing integer variables to `0` when they are not subsequently used in the code can lead to unnecessary gas consumption and code clutter. This issue points out instances where such initializations are present but serve no functional purpose.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

116:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {	// @audit-issue

135:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {	// @audit-issue

185:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {	// @audit-issue

209:            for (uint256 i = 0; i < _newBatchesData.length; ++i) {	// @audit-issue
```
[116](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116-L116), [135](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L135-L135), [185](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185-L185), [209](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209-L209), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

142:        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {	// @audit-issue

257:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {	// @audit-issue

289:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {	// @audit-issue

311:        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {	// @audit-issue

351:        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {	// @audit-issue

405:        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {	// @audit-issue

580:        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {	// @audit-issue

629:        uint256 versionedHashIndex = 0;	// @audit-issue

636:        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {	// @audit-issue

667:        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {	// @audit-issue
```
[142](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L142), [257](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257), [289](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289-L289), [311](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311-L311), [351](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351-L351), [405](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405-L405), [580](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580), [629](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629-L629), [636](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636), [667](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

208:        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {	// @audit-issue
```
[208](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208-L208), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

356:        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {	// @audit-issue
```
[356](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356-L356), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

101:        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {	// @audit-issue

138:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {	// @audit-issue

158:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {	// @audit-issue

178:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {	// @audit-issue
```
[101](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101-L101), [138](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138-L138), [158](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158-L158), [178](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178-L178), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol

92:        uint256 costForPubdata = 0;	// @audit-issue
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L92-L92), 


```solidity
Path: ./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

226:        for (uint256 i = 0; i < _factoryDeps.length; ++i) {	// @audit-issue
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226), 


```solidity
Path: ./code/contracts/ethereum/contracts/governance/Governance.sol

225:        for (uint256 i = 0; i < _calls.length; ++i) {	// @audit-issue
```
[225](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L225-L225), 


```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/Multicall3.sol

49:        for (uint256 i = 0; i < length; ) {	// @audit-issue

72:        for (uint256 i = 0; i < length; ) {	// @audit-issue

117:        for (uint256 i = 0; i < length; ) {	// @audit-issue

151:        for (uint256 i = 0; i < length; ) {	// @audit-issue
```
[49](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/Multicall3.sol#L49-L49), [72](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/Multicall3.sol#L72-L72), [117](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/Multicall3.sol#L117-L117), [151](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/Multicall3.sol#L151-L151), 


```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/Multicall.sol

36:        for (uint256 i = 0; i < calls.length; ++i) {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/Multicall.sol#L36-L36), 


```solidity
Path: ./code/system-contracts/contracts/Compressor.sol

61:            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {	// @audit-issue

124:        uint256 numInitialWritesProcessed = 0;	// @audit-issue
```
[61](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L61-L61), [124](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L124-L124), 


```solidity
Path: ./code/system-contracts/contracts/ImmutableSimulator.sol

38:            for (uint256 i = 0; i < immutablesLength; ++i) {	// @audit-issue
```
[38](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ImmutableSimulator.sol#L38-L38), 


```solidity
Path: ./code/system-contracts/contracts/KnownCodesStorage.sol

30:            for (uint256 i = 0; i < hashesLen; ++i) {	// @audit-issue
```
[30](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/KnownCodesStorage.sol#L30-L30), 


```solidity
Path: ./code/system-contracts/contracts/PubdataChunkPublisher.sol

36:        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {	// @audit-issue
```
[36](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/PubdataChunkPublisher.sol#L36-L36), 


```solidity
Path: ./code/system-contracts/contracts/L1Messenger.sol

197:        uint256 calldataPtr = 0;	// @audit-issue

206:        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {	// @audit-issue

224:            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {	// @audit-issue

236:        for (uint256 i = 0; i < numberOfMessages; ++i) {	// @audit-issue

254:        for (uint256 i = 0; i < numberOfBytecodes; ++i) {	// @audit-issue
```
[197](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L197-L197), [206](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L206-L206), [224](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L224-L224), [236](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L236-L236), [254](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L254-L254), 


```solidity
Path: ./code/system-contracts/contracts/ContractDeployer.sol

247:        uint256 sumOfValues = 0;	// @audit-issue

248:        for (uint256 i = 0; i < deploymentsLength; ++i) {	// @audit-issue

253:        for (uint256 i = 0; i < deploymentsLength; ++i) {	// @audit-issue
```
[247](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L247-L247), [248](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L248-L248), [253](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L253-L253), 


#### Recommendation


It is recommended not to initialize integer variables to `0` to save some Gas.


### Unnecessary Assert
Unnecessary `assert` statements in Solidity contracts can have several detrimental impacts on code readability, gas efficiency, and overall contract functionality. `assert` statements are typically used to check for conditions that should never occur under normal circumstances. While they can be valuable for catching unexpected errors and halting contract execution, their misuse can lead to unnecessary complexity and increased gas costs.


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

106:        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);	// @audit-issue
```
[106](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L106-L106), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol

51:        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);	// @audit-issue
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51-L51), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

426:        assert(block.chainid != 1);	// @audit-issue
```
[426](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L426-L426), 


```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/RevertTransferERC20.sol

26:        assert(!revertTransfer);	// @audit-issue
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/RevertTransferERC20.sol#L26-L26), 


```solidity
Path: ./code/contracts/ethereum/contracts/dev-contracts/RevertReceiveAccount.sol

24:        assert(!revertReceive);	// @audit-issue
```
[24](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/dev-contracts/RevertReceiveAccount.sol#L24-L24), 


```solidity
Path: ./code/system-contracts/contracts/DefaultAccount.sol

222:        assert(msg.sender != BOOTLOADER_FORMAL_ADDRESS);	// @audit-issue
```
[222](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/DefaultAccount.sol#L222-L222), 


```solidity
Path: ./code/system-contracts/contracts/libraries/RLPEncoder.sol

50:        assert(_len != 1);	// @audit-issue
```
[50](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/RLPEncoder.sol#L50-L50), 


#### Recommendation

Use 'assert' statements in Solidity judiciously, reserving them for conditions that indicate critical and unforeseen errors. Avoid overuse to maintain code clarity and prevent unnecessary gas consumption due to these costly checks.


### Unnecessary Assignment
The identified issue involves an unnecessary step of assigning a condition's result to a boolean variable before using it in an if-statement. This extra variable assignment is not required as the condition can be directly evaluated within the if-statement itself, making the code more concise and efficient.

```solidity
Path: ./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

467:            bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));	// @audit-issue: This assignment is not needed. Binary operation can be used in condition directly.
468:            address l2Sender = baseTokenWithdrawal ? L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR : l2BridgeAddress[_chainId];
```
[467](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L467-L468), 


#### Recommendation

Review your Solidity code for instances where boolean variables are unnecessarily assigned from conditions only to be used in immediate if-statements. Simplify these constructs by directly placing the conditional expression within the if-statement, eliminating the intermediary boolean variable. This practice not only streamlines your code, making it more concise, but also potentially reduces gas costs by minimizing the operations performed. Refactoring in this manner can enhance the readability and efficiency of your smart contracts. Always ensure that such optimizations maintain the original logic and intent of the code.


### Unnecessary casting as variable is already of the same type
In Solidity, explicitly casting a variable to a type that it already represents is redundant and can lead to confusion and clutter in the code. This unnecessary casting doesn't typically consume additional gas since Solidity's optimizer often removes such redundant conversions during compilation. However, it does affect code readability and may obscure the actual intent of the code, making it harder for developers to understand and maintain. Ensuring that casting is used only when necessary helps maintain clean, clear, and efficient code.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

266:            bytes32(uint256(protocolVersion)),	// @audit-issue: Variable `protocolVersion` is converted to `uint256` from type `uint256`.
```
[266](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L266-L266), 


#### Recommendation

Review your Solidity code for instances of unnecessary casting where variables are cast to their own type. Remove these redundant casts to enhance code clarity and maintainability. When writing new code, ensure that casting is only applied when changing a variable's type is genuinely needed. This practice helps in keeping the codebase straightforward and understandable, reducing potential confusion and errors associated with misinterpreting the variable types.


### Conditions Can Be Optimized
In Solidity development, the way conditional statements are written can significantly impact the contract's gas efficiency, readability, and overall maintainability. Complex or poorly structured conditions can lead to increased execution costs and potential security vulnerabilities. There is often an opportunity to simplify and streamline these statements. By optimizing conditional logic, developers can create smarter contracts that are not only more cost-effective in terms of gas usage but also more secure and easier to understand and maintain. This optimization plays a crucial role in enhancing the performance and reliability of smart contracts on the Ethereum blockchain.

`require(bool_var)` is better than `require(bool_var == True)`.


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

68:        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");	// @audit-issue
```
[68](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L68), 


#### Recommendation

Optimize conditional statements in Solidity for better gas efficiency, readability, and maintainability. Simplify logic where possible and consider the cost implications of each condition to create more effective and secure smart contracts.


### `event` Declared But Not Emitted
An event within the contract is declared but not utilized in any of the contract's functions or operations. Having unused event declarations can consume unnecessary space and may lead to misunderstandings for developers or users expecting this event as part of the contract's functionality.


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol

17:    event ProposeTransparentUpgrade(	// @audit-issue
```
[17](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L17-L17), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol

134:    event EthWithdrawalFinalized(address indexed to, uint256 amount);	// @audit-issue
```
[134](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L134-L134), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol

22:    event BaseTokenReceived(uint256 amount);	// @audit-issue
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/interfaces/IL2SharedBridge.sol#L22-L22), 


#### Recommendation


Consider removing the unused event declaration to optimize the contract and enhance clarity. If there is an intent for this event to be part of certain operations, ensure it is emitted appropriately. Otherwise, for the sake of clean and efficient code, it is advisable to remove any unused declarations.



### Unused `struct`s
Note that there may be cases where a struct superficially appears to be used, but this is only because there are multiple definitions of the struct in different files. In such cases, the struct definition should be moved into a separate file. The instances below are the unused definitions.

```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol

51:struct InitializeDataNewChain {	// @audit-issue
52:    IVerifier verifier;
53:    VerifierParams verifierParams;
54:    bytes32 l2BootloaderBytecodeHash;
55:    bytes32 l2DefaultAccountBytecodeHash;
56:    uint256 priorityTxMaxGasLimit;
57:    FeeParams feeParams;
58:    address blobVersionedHashRetriever;
59:}
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L51-L59), 


#### Recommendation

Identify and remove any unused `struct` definitions from your Solidity contracts. If a `struct` is defined multiple times across different files, centralize its definition in a single file and import it wherever required. This approach reduces code redundancy, ensures consistency in data structures, and helps maintain a clean and efficient codebase. Regularly auditing your contracts for unused or duplicated code elements like `structs` is a good practice for optimal contract maintenance and development.


### Revert String Size Optimization
Shortening the revert strings to fit within 32 bytes will decrease deployment time and decrease runtime Gas when the revert condition is met.

Revert strings that are longer than 32 bytes require at least one additional `mstore`, along with additional overhead to calculate memory offset, etc.



```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol

256:        require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");	// @audit-issue: String length is `41`
```
[256](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256-L256), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol

62:        require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");	// @audit-issue: String length is `35`

68:        require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");	// @audit-issue: String length is `33`
```
[62](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62-L62), [68](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L68), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol

90:        require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed	// @audit-issue: String length is `43`

105:        require(	// @audit-issue: String length is `33`
106:            cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:            "StateTransition: cutHash mismatch"
108:        );

110:        require(	// @audit-issue: String length is `63`
111:            s.protocolVersion == _oldProtocolVersion,
112:            "StateTransition: protocolVersion mismatch in STC when upgrading"
113:        );

116:        require(	// @audit-issue: String length is `64`
117:            s.protocolVersion > _oldProtocolVersion,
118:            "StateTransition: protocolVersion mismatch in STC after upgrading"
119:        );
```
[90](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90-L90), [105](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105-L108), [110](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110-L113), [116](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116-L119), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

226:        require(	// @audit-issue: String length is `38`
227:            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:            "Executor facet: wrong protocol version"
229:        );

616:        require(success, "failed to call point evaluation precompile");	// @audit-issue: String length is `42`
```
[226](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226-L229), [616](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616-L616), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol

22:        require(s.validators[msg.sender], "StateTransition Chain: not validator");	// @audit-issue: String length is `36`

27:        require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");	// @audit-issue: String length is `51`

32:        require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");	// @audit-issue: String length is `36`

37:        require(	// @audit-issue: String length is `64`
38:            msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39:            "StateTransition Chain: Only by admin or state transition manager"
40:        );

45:        require(	// @audit-issue: String length is `68`
46:            s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47:            "StateTransition Chain: Only by validator or state transition manager"
48:        );

53:        require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");	// @audit-issue: String length is `41`
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L22), [27](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27-L27), [32](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32-L32), [37](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40), [45](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48), [53](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53-L53), 


```solidity
Path: ./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

39:        require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");	// @audit-issue: String length is `59`

158:        require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");	// @audit-issue: String length is `45`

185:        require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");	// @audit-issue: String length is `55`

206:        require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");	// @audit-issue: String length is `45`
```
[39](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L39), [158](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L158), [185](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185-L185), [206](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206-L206), 


```solidity
Path: ./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

190:        require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");	// @audit-issue: String length is `34`

205:        require(	// @audit-issue: String length is `71`
206:            _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207:            "The new protocol version should be included in the L2 system upgrade tx"
208:        );

238:        require(	// @audit-issue: String length is `56`
239:            _newProtocolVersion > previousProtocolVersion,
240:            "New protocol version is not greater than the current one"
241:        );

242:        require(	// @audit-issue: String length is `35`
243:            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244:            "Too big protocol version difference"
245:        );

249:        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");	// @audit-issue: String length is `39`

250:        require(	// @audit-issue: String length is `61`
251:            s.l2SystemContractsUpgradeBatchNumber == 0,
252:            "The batch number of the previous upgrade has not been cleaned"
253:        );
```
[190](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190-L190), [205](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205-L208), [238](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L241), [242](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L242-L245), [249](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249-L249), [250](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L250-L253), 


```solidity
Path: ./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol

22:        require(	// @audit-issue: String length is `56`
23:            // Genesis Upgrade difference: Note this is the only thing change > to >=
24:            _newProtocolVersion >= previousProtocolVersion,
25:            "New protocol version is not greater than the current one"
26:        );

27:        require(	// @audit-issue: String length is `35`
28:            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:            "Too big protocol version difference"
30:        );

33:        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");	// @audit-issue: String length is `39`

34:        require(	// @audit-issue: String length is `61`
35:            s.l2SystemContractsUpgradeBatchNumber == 0,
36:            "The batch number of the previous upgrade has not been cleaned"
37:        );
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22-L26), [27](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27-L30), [33](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33-L33), [34](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L37), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol

83:        require(	// @audit-issue: String length is `46`
84:            !stateTransitionManagerIsRegistered[_stateTransitionManager],
85:            "Bridgehub: state transition already registered"
86:        );

93:        require(	// @audit-issue: String length is `46`
94:            stateTransitionManagerIsRegistered[_stateTransitionManager],
95:            "Bridgehub: state transition not registered yet"
96:        );

102:        require(!tokenIsRegistered[_token], "Bridgehub: token already registered");	// @audit-issue: String length is `35`

125:        require(	// @audit-issue: String length is `42`
126:            stateTransitionManagerIsRegistered[_stateTransitionManager],
127:            "Bridgehub: state transition not registered"
128:        );

132:        require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");	// @audit-issue: String length is `37`

225:                require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");	// @audit-issue: String length is `40`

300:        require(	// @audit-issue: String length is `40`
301:            _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302:            "Bridgehub: second bridge address too low"
303:        ); // to avoid calls to precompiles
```
[83](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L86), [93](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93-L96), [102](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102-L102), [125](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125-L128), [132](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132-L132), [225](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225-L225), [300](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300-L303), 


```solidity
Path: ./code/contracts/ethereum/contracts/governance/Governance.sol

59:        require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");	// @audit-issue: String length is `64`

65:        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");	// @audit-issue: String length is `54`

71:        require(	// @audit-issue: String length is `69`
72:            msg.sender == owner() || msg.sender == securityCouncil,
73:            "Only the owner and security council are allowed to call this function"
74:        );

172:        require(isOperationReady(id), "Operation must be ready before execution");	// @audit-issue: String length is `40`

177:        require(isOperationReady(id), "Operation must be ready after execution");	// @audit-issue: String length is `39`

191:        require(isOperationPending(id), "Operation must be pending before execution");	// @audit-issue: String length is `42`

196:        require(isOperationPending(id), "Operation must be pending after execution");	// @audit-issue: String length is `41`

216:        require(!isOperation(_id), "Operation with this proposal id already exists");	// @audit-issue: String length is `46`

217:        require(_delay >= minDelay, "Proposed delay is less than minimum delay");	// @audit-issue: String length is `41`

240:        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");	// @audit-issue: String length is `35`
```
[59](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L59-L59), [65](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L65-L65), [71](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74), [172](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L172-L172), [177](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L177-L177), [191](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L191-L191), [196](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L196-L196), [216](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L216-L216), [217](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L217-L217), [240](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/governance/Governance.sol#L240-L240), 


```solidity
Path: ./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol

75:        require(	// @audit-issue: String length is `42`
76:            msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77:            "L1SharedBridge: not bridgehub or era chain"
78:        );

155:            require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");	// @audit-issue: String length is `45`

195:        require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");	// @audit-issue: String length is `36`

427:            require(!alreadyFinalized, "Withdrawal is already finalized 2");	// @audit-issue: String length is `33`

564:        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");	// @audit-issue: String length is `33`
```
[75](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78), [155](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155-L155), [195](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195-L195), [427](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427-L427), [564](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564-L564), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

51:        require(_l1Address != address(0), "L1 WETH token address cannot be zero");	// @audit-issue: String length is `36`
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol#L51-L51), 


```solidity
Path: ./code/contracts/zksync/contracts/bridge/L2SharedBridge.sol

92:        require(msg.value == 0, "Value should be 0 for ERC20 bridge");	// @audit-issue: String length is `34`
```
[92](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92-L92), 


```solidity
Path: ./code/system-contracts/contracts/Compressor.sol

51:            require(	// @audit-issue: String length is `72`
52:                encodedData.length * 4 == _bytecode.length,
53:                "Encoded data length should be 4 times shorter than the original bytecode"
54:            );

56:            require(	// @audit-issue: String length is `77`
57:                dictionary.length / 8 <= encodedData.length / 2,
58:                "Dictionary should have at most the same number of entries as the encoded data"
59:            );

63:                require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");	// @audit-issue: String length is `36`

68:                require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");	// @audit-issue: String length is `50`

119:        require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");	// @audit-issue: String length is `35`

156:        require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");	// @audit-issue: String length is `41`

187:        require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");	// @audit-issue: String length is `35`

230:                require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");	// @audit-issue: String length is `58`

232:                require(	// @audit-issue: String length is `46`
233:                    _initialValue + convertedValue == _finalValue,
234:                    "add: initial plus converted not equal to final"
235:                );

237:                require(	// @audit-issue: String length is `47`
238:                    _initialValue - convertedValue == _finalValue,
239:                    "sub: initial minus converted not equal to final"
240:                );
```
[51](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L51-L54), [56](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L56-L59), [63](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L63-L63), [68](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L68-L68), [119](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L119-L119), [156](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L156-L156), [187](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L187-L187), [230](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L230-L230), [232](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L232-L235), [237](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/Compressor.sol#L237-L240), 


```solidity
Path: ./code/system-contracts/contracts/ImmutableSimulator.sol

35:        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");	// @audit-issue: String length is `45`
```
[35](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ImmutableSimulator.sol#L35-L35), 


```solidity
Path: ./code/system-contracts/contracts/KnownCodesStorage.sol

76:        require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");	// @audit-issue: String length is `34`
```
[76](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/KnownCodesStorage.sol#L76-L76), 


```solidity
Path: ./code/system-contracts/contracts/NonceHolder.sol

66:        require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");	// @audit-issue: String length is `48`

136:        require(	// @audit-issue: String length is `61`
137:            msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138:            "Only the contract deployer can increment the deployment nonce"
139:        );
```
[66](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/NonceHolder.sol#L66-L66), [136](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/NonceHolder.sol#L136-L139), 


```solidity
Path: ./code/system-contracts/contracts/SystemContext.sol

242:        require(_isFirstInBatch, "Upgrade transaction must be first");	// @audit-issue: String length is `33`

245:        require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");	// @audit-issue: String length is `44`

249:            require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");	// @audit-issue: String length is `39`

287:            require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");	// @audit-issue: String length is `40`

351:            require(	// @audit-issue: String length is `97`
352:                _l2BlockTimestamp >= currentBatchTimestamp,
353:                "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354:            );

355:            require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");	// @audit-issue: String length is `63`

367:            require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");	// @audit-issue: String length is `53`

368:            require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");	// @audit-issue: String length is `47`

369:            require(	// @audit-issue: String length is `51`
370:                _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371:                "The previous hash of the same L2 block must be same"
372:            );

373:            require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");	// @audit-issue: String length is `60`

385:            require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");	// @audit-issue: String length is `38`

386:            require(	// @audit-issue: String length is `93`
387:                _l2BlockTimestamp > currentL2BlockTimestamp,
388:                "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389:            );

413:        require(currentBatchNumber > 0, "The current batch number must be greater than 0");	// @audit-issue: String length is `47`

429:        require(	// @audit-issue: String length is `83`
430:            _newTimestamp > currentBlockTimestamp,
431:            "The timestamp of the batch must be greater than the timestamp of the previous block"
432:        );

452:        require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");	// @audit-issue: String length is `40`
```
[242](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L242-L242), [245](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L245-L245), [249](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L249-L249), [287](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L287-L287), [351](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L351-L354), [355](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L355-L355), [367](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L367-L367), [368](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L368-L368), [369](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L369-L372), [373](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L373-L373), [385](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L385-L385), [386](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L386-L389), [413](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L413-L413), [429](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L429-L432), [452](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/SystemContext.sol#L452-L452), 


```solidity
Path: ./code/system-contracts/contracts/ComplexUpgrader.sol

22:        require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");	// @audit-issue: String length is `36`
```
[22](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ComplexUpgrader.sol#L22-L22), 


```solidity
Path: ./code/system-contracts/contracts/L2BaseToken.sol

33:        require(	// @audit-issue: String length is `62`
34:            msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35:                msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36:                msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37:            "Only system contracts with special access can call this method"
38:        );
```
[33](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L2BaseToken.sol#L33-L38), 


```solidity
Path: ./code/system-contracts/contracts/L1Messenger.sol

214:        require(	// @audit-issue: String length is `60`
215:            reconstructedChainedLogsHash == chainedLogsHash,
216:            "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217:        );

245:        require(	// @audit-issue: String length is `68`
246:            reconstructedChainedMessagesHash == chainedMessagesHash,
247:            "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248:        );

269:        require(	// @audit-issue: String length is `94`
270:            reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271:            "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272:        );

279:        require(	// @audit-issue: String length is `39`
280:            uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281:                STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282:            "state diff compression version mismatch"
283:        );

315:        require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");	// @audit-issue: String length is `42`
```
[214](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L214-L217), [245](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L245-L248), [269](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L269-L272), [279](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L279-L283), [315](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/L1Messenger.sol#L315-L315), 


```solidity
Path: ./code/system-contracts/contracts/DefaultAccount.sol

100:        require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");	// @audit-issue: String length is `34`

202:        require(success, "Failed to pay the fee to the operator");	// @audit-issue: String length is `37`
```
[100](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/DefaultAccount.sol#L100-L100), [202](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/DefaultAccount.sol#L202-L202), 


```solidity
Path: ./code/system-contracts/contracts/ContractDeployer.sol

77:        require(	// @audit-issue: String length is `67`
78:            _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79:                currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80:            "It is only possible to change from sequential to arbitrary ordering"
81:        );

239:        require(	// @audit-issue: String length is `65`
240:            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241:            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:        );

251:        require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");	// @audit-issue: String length is `69`

265:        require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");	// @audit-issue: String length is `40`

350:            require(value == 0, "The value must be zero if we do not call the constructor");	// @audit-issue: String length is `56`
```
[77](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L77-L81), [239](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L239-L242), [251](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L251-L251), [265](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L265-L265), [350](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/ContractDeployer.sol#L350-L350), 


```solidity
Path: ./code/system-contracts/contracts/AccountCodeStorage.sol

26:        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");	// @audit-issue: String length is `45`

37:        require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");	// @audit-issue: String length is `46`

48:        require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");	// @audit-issue: String length is `43`

57:        require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");	// @audit-issue: String length is `46`
```
[26](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/AccountCodeStorage.sol#L26-L26), [37](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/AccountCodeStorage.sol#L37-L37), [48](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/AccountCodeStorage.sol#L48-L48), [57](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/AccountCodeStorage.sol#L57-L57), 


```solidity
Path: ./code/system-contracts/contracts/interfaces/ISystemContract.sol

21:        require(	// @audit-issue: String length is `36`
22:            SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23:            "This method require system call flag"
24:        );

31:        require(	// @audit-issue: String length is `52`
32:            SystemContractHelper.isSystemContract(msg.sender),
33:            "This method require the caller to be system contract"
34:        );
```
[21](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/interfaces/ISystemContract.sol#L21-L24), [31](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/interfaces/ISystemContract.sol#L31-L34), 



```solidity
Path: ./code/system-contracts/contracts/openzeppelin/utils/Address.sol

67:        require(	// @audit-issue: String length is `58`
68:            success,
69:            "Address: unable to send value, recipient may have reverted"
70:        );

155:        require(	// @audit-issue: String length is `38`
156:            address(this).balance >= value,
157:            "Address: insufficient balance for call"
158:        );
```
[67](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/openzeppelin/utils/Address.sol#L67-L70), [155](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/openzeppelin/utils/Address.sol#L155-L158), 


```solidity
Path: ./code/system-contracts/contracts/libraries/TransactionHelper.sol

363:        require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");	// @audit-issue: String length is `58`

367:            require(	// @audit-issue: String length is `64`
368:                _transaction.paymasterInput.length >= 68,
369:                "The approvalBased paymaster input must be at least 68 bytes long"
370:            );
```
[363](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/TransactionHelper.sol#L363-L363), [367](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/TransactionHelper.sol#L367-L370), 


```solidity
Path: ./code/system-contracts/contracts/libraries/SystemContractHelper.sol

319:        require(index < 10, "There are only 10 accessible registers");	// @audit-issue: String length is `38`
```
[319](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319-L319), 


#### Recommendation


To optimize Gas usage in your Solidity contract, it is recommended to keep revert strings as short as possible and to ensure that they fit within 32 bytes. It is possible to use abbreviations or simplified error messages to keep the string length short. Doing so can reduce the amount of Gas used during deployment and runtime when the revert condition is met.


### Do not calculate constants
Due to how constant variables are implemented (replacements at compile-time), an expression assigned to a constant variable is recomputed each time that the variable is used, which wastes some gas.

```solidity
Path: ./code/system-contracts/contracts/NonceHolder.sol

28:    uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;	// @audit-issue

31:    uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;	// @audit-issue
```
[28](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/NonceHolder.sol#L28-L28), [31](https://github.com/code-423n4/2024-03-zksync/blob/2fe9d4e62ab688c92a959e265b9094f82502787b/./code/system-contracts/contracts/NonceHolder.sol#L31-L31), 


#### Recommendation

Precompute and assign literal values to constant variables in your Solidity contracts. Avoid defining constants with expressions or calculations. By providing direct values, you ensure that the compiler replaces these constants efficiently in the bytecode, maximizing gas savings and contract performance. Review your contracts to identify any constants defined with expressions and refactor them to use precomputed literal values instead.
