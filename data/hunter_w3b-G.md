# Gas Optimization zkSync Era Contest

I have conducted a thorough audit of zkSync Era L1 contracts contest, focusing on optimizing gas saving for efficient and cost-effective operations. After rigorous analysis, I am pleased to present the following key findings and recommendations to help improve the gas optmization of `zkSync Era`:

When doing the refactoring, we’ve avoided including any changes that were `reported by the` [4naly3er](https://github.com/code-423n4/2024-03-zksync/blob/main/4naly3er-report.md) and we encourage you to go through the automated findings to maximum the amount of gas being saved.

| Num | Finding Issue                                                                                       | Instances |
| --- | :-------------------------------------------------------------------------------------------------- | :-------- |
| 1   | Make `constructors` payable                                                                         | 10        |
| 2   | The result of function calls should be cached rather than `re-calling` the function                 | 6         |
| 3   | Use `SSTORE2` or `SSTORE3` to store a lot of data                                                   | 3         |
| 4   | Use `ECDSA` signatures instead of merkle trees                                                      | 1         |
| 5   | `selfbalance` is cheaper than `address(this).balance` (more efficient in certain scenarios)         | 3         |
| 6   | `Do-While` loops are cheaper than for loops                                                         | 22        |
| 7   | Don't `Initialize` Variables with Default Value                                                     | 38        |
| 8   | `REQUIRE()/REVERT()` strings longer than 32 bytes cost extra Gas                                    | 66        |
| 9   | Use assembly to check for `address(0)`                                                              | 50        |
| 10  | Using `constants` directly rather than caching the value, saves gas                                 | 2         |
| 11  | Use local variables for `emitting`                                                                  | 12        |
| 12  | Using `this` to access functions results in an external call, wasting gas                           | 3         |
| 13  | State variables only set in their definitions should be declared constant                           | 3         |
| 14  | `Calldata` is cheaper than `memory`                                                                 | 17        |
| 15  | Internal functions only called once can be `inlined` to save gas                                    | 79        |
| 16  | Multiple `address/ID` mappings can be combined into a single mapping of an `address/ID` to a struct | 14        |
| 17  | Using storage instead of `memory` for structs/arrays saves gas                                      | 15        |
| 18  | Multiple accesses of a `mapping/array` should use a local variable cache                            | 49        |
| 19  | `Stack variable` used as a cheaper cache for a state variable is only used once                     | 13        |
| 20  | `require()` statements that check input arguments should be at the top of the function              | 6         |
| 21  | Use solidity version `0.8.20` or above to improve gas performance                                   |           |
| 22  | Expression `is cheaper than`new bytes(0)                                                            | 8         |
| 23  | Initializers can be marked `payable`                                                                | 8         |
| 24  | Use assembly to `emit` events                                                                       | 77        |
| 25  | Don't compare boolean expressions to `boolean` literals                                             | 1         |
| 26  | Don't use `_msgSender()` if not supporting EIP-2771                                                 | 1         |
| 27  | Fewer storage slots can be used by storing timestamps in types smaller than `uint256`               | 5         |
| 28  | `keccak256()` should only need to be called on a specific string literal once                       | 4         |
| 29  | `Emit` Used In Loop                                                                                 | 3         |
| 30  | Private functions used once can be `inlined`                                                        | 15        |
| 31  | `State variable` read in loops                                                                      | 5         |
| 32  | Storage `re-read` via storage pointer                                                               | 3         |
| 33  | Avoid fetching a low-level call's return data by using `assembly`                                   | 3         |
| 34  | Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead                            | 20        |
| 35  | Use assembly to calculate `hashes` to save gas                                                      | 60        |
| 36  | Duplicated `require()`/`revert()` checks should be refactored to a modifier or function             | 3         |
| 37  | Use the `inputs/results` of assignments rather than `re-reading` state variables                    | 11        |
| 38  | Assigning state variables directly with named struct constructors wastes gas                        | 19        |
| 39  | Do not calculate constants                                                                          | 2         |
| 40  | Consider using alternatives to `OpenZeppelin`                                                       |           |
| 41  | Use assembly to write address/contract type storage values                                          | 5         |
| 42  | Use fallback or receive instead of deposit() when transferring Ether                                | 6         |
| 43  | Using assembly to revert with an error message                                                      | 255       |
| 44  | Test if a number is even or odd by checking the last bit instead of using a modulo operator         | 1         |
| 45  | Use Clones for Cheap Contract Deployments                                                           | 2         |
| 46  | Admin functions no uses of the nonReentrant modifier                                                | 19        |
| 47  | Use Mappings instead of arrays                                                                      | 6         |
| 48  | array[index] += amount is cheaper than array[index] = array[index] + amount                         | 1         |

Total: `48` Instances.

## [G-01] Make `constructors` payable

**Issue Description**\
Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

**Proposed Optimization**\

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity 0.8.20;

contract A {}

contract B {
    constructor() payable {}
}
```

**Estimated Gas Savings**\
Making the constructor payable saved 200 gas on deployment. This is because non-payable functions have an implicit `require(msg.value == 0)` inserted in them. Additionally, fewer bytecode at deploy time mean less gas cost due to smaller calldata.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 10 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  55          constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
  56              sharedBridge = _sharedBridge;
  57          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  90          constructor(
  91              address _l1WethAddress,
  92              IBridgehub _bridgehub,
  93              IL1ERC20Bridge _legacyBridge
  94          ) reentrancyGuardInitializer {
  95              _disableInitializers();
  96              l1WethAddress = _l1WethAddress;
  97              bridgehub = _bridgehub;
  98              legacyBridge = _legacyBridge;
  99          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  38          constructor() reentrancyGuardInitializer {}


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  41          constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
  42              require(_admin != address(0), "Admin should be non zero address");
  43
  44              _transferOwnership(_admin);
  45
  46              securityCouncil = _securityCouncil;
  47              emit ChangeSecurityCouncil(address(0), _securityCouncil);
  48
  49              minDelay = _minDelay;
  50              emit ChangeMinDelay(0, _minDelay);
  51          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L41

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  58          constructor(address _bridgehub) reentrancyGuardInitializer {
  59              bridgehub = _bridgehub;
  60          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

  ```solidity
  File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


  55          constructor(address _initialOwner, uint32 _executionDelay) {
  56              _transferOwnership(_initialOwner);
  57              executionDelay = _executionDelay;
  58          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


  19          constructor() reentrancyGuardInitializer {}


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L19

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


  11          constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
  12              // Check that the contract is deployed on the expected chain.
  13              // Thus, the contract deployed by the same Create2 factory on the different chain will have different addresses!
  14              require(_chainId == block.chainid, "pr");
  15              Diamond.diamondCut(_diamondCut);
  16          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11:16

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  41          constructor() {
  42              _disableInitializers();
  43          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41:43

  ```solidity
  File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


  40          constructor() {
  41              // Disable initialization to prevent Parity hack.
  42              _disableInitializers();
  43          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol

    </details>

## [G-02] The result of function calls should be cached rather than `re-calling` the function

**Issue Description**\
The issue is related to the inefficient practice of calling the same function multiple times within a contract, leading to unnecessary gas consumption. When a function is called, its code is executed, and if the function is called multiple times, the same code is executed repeatedly, resulting in higher gas costs.

**Proposed Optimization**\
Instead of calling the same function multiple times, it is recommended to cache the result of the function call in a local variable. By doing so, the contract can avoid executing the function code repeatedly, leading to gas savings.

**Estimated Gas Savings**\
The estimated gas savings depend on the complexity and gas cost of the function being called. In general, the `gas savings` will be proportional to the number of times the function is called after the initial call. For each subsequent call, the gas cost of executing the function code is saved.

**Attachments**

Find more findings

- **Code Snippets**

    <details>
    <summary>Click to show 4 findings</summary>

  ```solidity
  File: contracts/GasBoundCaller.sol


  59              uint256 pubdataPublishedAfter = REAL_SYSTEM_CONTEXT_CONTRACT.getCurrentPubdataSpent();


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L59

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  518                 (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);


  519                 (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);


  520                 (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L518

    </details>

## [G-03] Use `SSTORE2` or `SSTORE3` to store a lot of data

**Issue Description**\
The current implementation uses the `SSTORE` opcode to store persistent data on a key-value basis. However, the costs of writing (SSTORE) and reading (SLOAD) are expensive in terms of gas spent. Writing 32 bytes costs `22,100` gas, which translates to about `690` gas per byte, while writing a smart contract's bytecode costs 200 gas per byte.

**Proposed Optimization**\
Instead of using `SSTORE` for storing data, it is recommended to store the data in the contract's bytecode during deployment. This approach is more gas-efficient as writing to the bytecode costs only 200 gas per byte, compared to `22,100` gas for writing 32 bytes using `SSTORE`.

`SSTORE2` uses a contract's bytecode to write and store data, leveraging its inherent property of immutability. It allows us to write only once, effectively using `CREATE` instead of `SSTORE`. To read, we call `EXTCODECOPY` on the deployed address where the particular data is stored as bytecode. This method significantly reduces the cost of writing data when large amounts of data need to be stored.

`SSTORE3` is a design that makes the newly deployed address independent of our provided data. The provided data is first stored in storage using SSTORE, then a constant `INIT_CODE` is passed as data in `CREATE2`, which internally reads the provided data stored in storage to deploy it as code. This design enables us to efficiently calculate the pointer address of our data just by providing the salt, thereby reducing storage costs.

**Estimated Gas Savings**\
Writing 32 bytes using `SSTORE` costs `22,100` gas, which translates to approximately 690 gas per byte. On the other hand, writing the same data to the contract's bytecode during deployment would cost only 200 gas per byte. Therefore, the estimated gas savings by using this optimization would be `(690 - 200) = 490` gas per byte of data stored.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol


54            sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)

79            sstore(LOCK_FLAG_ADDRESS, _ENTERED)

87            sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L54

## [G-04] Use `ECDSA` signatures instead of merkle trees

**Issue Description**\
Merkle trees use a considerable amount of calldata and increase in cost with the size of the merkle proof. Generally, using digital signatures is cheaper gas-wise compared to merkle proofs.

Although the current implementation of the calculateRoot function in the Merkle contract is correct, it can be more gas-efficient by making use of the following optimizations:

**Proposed Optimization**

### 1. In-place Computation

The `calculateRoot` function can be optimized by using in-place computation to store intermediate hashes at each level of the Merkle tree. This approach eliminates the need to create new arrays, reducing memory usage and gas costs.

Note: this optimization requires the leaves array not to be used again after it is modified. Based on the current implementation, this optimization is safe because the leaves array is not used again after it is modified.

### 2. Assembly

The use of assembly code to load the left and right siblings into memory is more gas-efficient

```solidity
File: contracts/zksync/libraries/Merkle.sol

18    function calculateRoot(
19        bytes32[] calldata _path,
20        uint256 _index,
21        bytes32 _itemHash
22    ) internal pure returns (bytes32) {
23        uint256 pathLength = _path.length;
24        require(pathLength > 0, "xc");
25        require(pathLength < 256, "bt");
26        require(_index < (1 << pathLength), "px");
27
28        bytes32 currentHash = _itemHash;
29        for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
30            currentHash = (_index % 2 == 0)
31                ? _efficientHash(currentHash, _path[i])
32                : _efficientHash(_path[i], currentHash);
33            _index /= 2;
34        }
35
36        return currentHash;
37    }
```

https://github.com/code-423n4/2023-10-zksync/blob/main/code/contracts/ethereum/contracts/zksync/libraries/Merkle.sol#L9

## [G-05] `selfbalance` is cheaper than `address(this).balance` (more efficient in certain scenarios)

**Issue Description**\
The choice between using address(this).balance or the selfbalance() function from the assembly language can impact gas consumption.

**Proposed Optimization**\
To optimize gas usage, it is recommended to use the `selfbalance()` function from Yul instead of `address(this).balance` when retrieving the balance of a contract. The selfbalance() function can be more efficient in certain scenarios.

**Estimated Gas Savings**\
The estimated gas savings from using selfbalance() instead of address(this).balance can vary depending on the specific use case and the overall complexity of the contract. However, in general, selfbalance() can save a few gas units compared to address(this).balance.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol

118            uint256 balanceBefore = address(this).balance;

120            uint256 balanceAfter = address(this).balance;
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

41        uint256 amount = address(this).balance;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41

## [G-06] `Do-While` loops are cheaper than for loops

**Issue Description**\
The choice between using a for loop or a do-while loop can impact gas consumption.

**Proposed Optimization**\
To optimize gas usage, it is recommended to use `do-while` loops instead of for loops, even if an additional condition check is required to handle the case where the loop does not execute at all. Despite the additional condition check, `do-while` loops are generally cheaper in terms of gas cost compared to for loops.

**Estimated Gas Savings**\

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 18 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  225             for (uint256 i = 0; i < _calls.length; ++i) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L255

  ```solidity
  File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


  116                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {


  135                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {


  185                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {


  209                 for (uint256 i = 0; i < _newBatchesData.length; ++i) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  142             for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {


  257             for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {


  289             for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {


  636             for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  226             for (uint256 i = 0; i < _factoryDeps.length; ++i) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

  ```solidity
  File: system-contracts/contracts/Compressor.sol


  61                  for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

  208        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  356        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


  101        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {


  138        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {


  158        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {


  178        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


  29        for (uint256 i; i < pathLength; i = i.uncheckedInc()) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29

    </details>

## [G-07] Don't `Initialize` Variables with Default Value

<details>
<summary>Click to show 38 findings</summary>

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


for (uint256 i = 0; i < _calls.length; ++i) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


for (uint256 i = 0; i < _newBatchesData.length; ++i) {

for (uint256 i = 0; i < _newBatchesData.length; ++i) {

for (uint256 i = 0; i < _newBatchesData.length; ++i) {

for (uint256 i = 0; i < _newBatchesData.length; ++i) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {

for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {

for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {

for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {

for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {

for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

uint256 versionedHashIndex = 0;

for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {

for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {

for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


uint256 costForPubdata = 0;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L92

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


for (uint256 i = 0; i < _factoryDeps.length; ++i) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226

```solidity
File: system-contracts/contracts/Compressor.sol


for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {

uint256 numInitialWritesProcessed = 0;

for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L159

```solidity
File: system-contracts/contracts/ContractDeployer.sol


uint256 sumOfValues = 0;

for (uint256 i = 0; i < deploymentsLength; ++i) {

for (uint256 i = 0; i < deploymentsLength; ++i) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L253

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol


for (uint256 i = 0; i < immutablesLength; ++i) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol


for (uint256 i = 0; i < hashesLen; ++i) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30

```solidity
File: system-contracts/contracts/L1Messenger.sol


uint256 calldataPtr = 0;

for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {

for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {

for (uint256 i = 0; i < numberOfMessages; ++i) {

for (uint256 i = 0; i < numberOfBytecodes; ++i) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L254

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol


for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36

</details>

## [G-08] `REQUIRE()/REVERT()` strings longer than 32 bytes cost extra Gas

**Issue Description**\
When using the `REQUIRE()` strings longer than 32 bytes incur additional gas costs due to the way they are stored and handled.

**Proposed Optimization**\
Refactor the code to avoid passing strings longer than 32 bytes to the `REQUIRE()` or REVERT() functions. Instead, consider using more concise error messages or splitting longer messages into multiple smaller ones.

**Estimated Gas Savings**\

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 66 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");

  require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");

  require(!alreadyFinalized, "Withdrawal is already finalized 2");

  require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  require(!tokenIsRegistered[_token], "Bridgehub: token already registered");

  require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");

  require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");

  require(msg.sender == securityCouncil, "Only security council is allowed to call this function");

  require(isOperationReady(id), "Operation must be ready before execution");

  require(isOperationReady(id), "Operation must be ready after execution");

  require(isOperationPending(id), "Operation must be pending before execution");

  require(isOperationPending(id), "Operation must be pending after execution");

  require(!isOperation(_id), "Operation with this proposal id already exists");

  require(_delay >= minDelay, "Proposed delay is less than minimum delay");

  require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256

  ```solidity
  File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


  require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");

  require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


  require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  require(success, "failed to call point evaluation precompile");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");

  require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");

  require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");

  require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


  require(s.validators[msg.sender], "StateTransition Chain: not validator");

  require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");

  require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");

  require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong");

  require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


  require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  require(msg.value == 0, "Value should be 0 for ERC20 bridge");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92

  ```solidity
  File: system-contracts/contracts/AccountCodeStorage.sol


  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

  require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");

  require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");

  require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57

  ```solidity
  File: system-contracts/contracts/ComplexUpgrader.sol


  require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22

  ```solidity
  File: system-contracts/contracts/Compressor.sol


  require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");

  require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");

  require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");

  require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");

  require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");

  require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230

  ```solidity
  File: system-contracts/contracts/ContractDeployer.sol


  require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

  require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");

  require(value == 0, "The value must be zero if we do not call the constructor");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350

  ```solidity
  File: system-contracts/contracts/DefaultAccount.sol


  require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");

  require(success, "Failed to pay the fee to the operator");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/system-contracts/contracts/DefaultAccount.sol#L202

  ```solidity
  File: system-contracts/contracts/ImmutableSimulator.sol


  require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35

  ```solidity
  File: system-contracts/contracts/KnownCodesStorage.sol


  require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/system-contracts/contracts/KnownCodesStorage.sol#L76

  ```solidity
  File: system-contracts/contracts/L1Messenger.sol


  require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315

  ```solidity
  File: system-contracts/contracts/NonceHolder.sol


  require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66

  ```solidity
  File: system-contracts/contracts/SystemContext.sol


  require(_isFirstInBatch, "Upgrade transaction must be first");

  require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");

  require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");

  require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");

  require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");

  require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");

  require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");

  require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");

  require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");

  require(currentBatchNumber > 0, "The current batch number must be greater than 0");

  require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452

  ```solidity
  File: system-contracts/contracts/libraries/SystemContractHelper.sol


  require(index < 10, "There are only 10 accessible registers");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319

  ```solidity
  File: system-contracts/contracts/libraries/TransactionHelper.sol


  require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long");

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363

</details>

## [G-09] Use assembly to check for `address(0)`

**Issue Description**\
Currently, the contracts may be using the `address(0)` check conventionally, which can consume unnecessary gas.

**Proposed Optimization**\
Utilize assembly to check for the zero address `address(0)` more efficiently, resulting in gas savings.

**Estimated Gas Savings**\
Implementing this optimization can save approximately `6` gas per instance where the zero address check is performed.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 50 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  108             require(_owner != address(0), "ShB owner 0");


  188             require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");


  563             require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");


  578                 if (_refundRecipient == address(0)) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L578

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  130             require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");


  132             require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");


  326             if (_refundRecipient == address(0)) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L326

  ```solidity
  File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


  41              require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  42              require(_admin != address(0), "Admin should be non zero address");


  240             require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  82              require(_initializeData.governor != address(0), "StateTransition: governor zero");


  246             if (stateTransition[_chainId] != address(0)) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L246

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


  25              require(address(_initializeData.verifier) != address(0), "vt");


  26              require(_initializeData.admin != address(0), "vy");


  27              require(_initializeData.validatorTimelock != address(0), "hc");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


  30              require(facetAddress != address(0), "F"); // Proxy has no facet for this selector


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  191             if (_expectedSystemContractUpgradeTxHash == bytes32(0)) {


  237             if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {


  639                 require(blobVersionedHash != bytes32(0), "vh");


  663             require(versionedHash == bytes32(0), "lh");


  669                     (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||


  669                     (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||


  670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),


  670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


  183             require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  275             address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L275

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


  141                 require(oldFacet.facetAddress == address(0), "J"); // facet for this selector already exists


  161                 require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address


  175             require(_facet == address(0), "a1"); // facet address must be zero


  181                 require(oldFacet.facetAddress != address(0), "a2"); // Can't delete a non-existent facet


  279             if (_init == address(0)) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L279

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  93              if (_l2DefaultAccountBytecodeHash == bytes32(0)) {


  110             if (_l2BootloaderBytecodeHash == bytes32(0)) {


  148                 _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) &&


  149                 _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) &&


  150                 _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)


  249             require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L249

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


  33              require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  55              require(_l1Bridge != address(0), "bf");


  56              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");


  57              require(_aliasedOwner != address(0), "sf");


  58              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");


  68                  require(_l1LegecyBridge != address(0), "bf2");


  96              if (currentL1Token == address(0)) {


  129             require(l1Token != address(0), "yh");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129

  ```solidity
  File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


  51              require(_l1Address != address(0), "in6"); // Should be non-zero address


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51

  ```solidity
  File: system-contracts/contracts/DefaultAccount.sol


  94              bytes32 txHash = _suggestedSignedHash != bytes32(0) ? _suggestedSignedHash : _transaction.encodeHash();


  188             return recoveredAddress == address(this) && recoveredAddress != address(0);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188

  ```solidity
  File: system-contracts/contracts/KnownCodesStorage.sol


  76              require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76

  ```solidity
  File: system-contracts/contracts/libraries/TransactionHelper.sol


  406             if (address(uint160(_transaction.paymaster)) != address(0)) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L406

    </details>

## [G-10] Using `constants` directly rather than caching the value, saves gas

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol


103                 codeHash = EMPTY_STRING_KECCAK;


108                 codeHash = EMPTY_STRING_KECCAK;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L108

## [G-11] Use local variables for `emitting`

**Issue Description**\
The issue is related to the inefficient use of state variables when emitting events in contracts. Directly accessing state variables when emitting events can lead to unnecessary gas consumption due to additional read operations (e.g., Gwarmaccess or Gcoldsload).

**Proposed Optimization**\
Instead of directly accessing state variables when emitting events, it is recommended to use local variables or function parameters. By doing so, the contract can avoid unnecessary read operations from storage, resulting in gas savings.

**Estimated Gas Savings**\
The gas savings depend on the specific context and usage of the state variables. However, the following estimates can be provided:

- If the state variable has already been accessed within the function/modifier, using a local copy can save 100 gas (Gwarmaccess) per instance.
- If the state variable has not been accessed yet, using a local copy can save 2100 gas (Gcoldsload) per instance.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 12 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  69              emit NewAdmin(previousAdmin, pendingAdmin);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  250             emit ChangeMinDelay(minDelay, _newDelay);


  257             emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  128             emit NewAdmin(previousAdmin, pendingAdmin);


  227             emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  436             emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);


  496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);


  496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);


  496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496

  ```solidity
  File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


  101             emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);


  126             emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);


  126             emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126

    </details>

## [G-12] Using `this` to access functions results in an external call, wasting gas

**Issue Description**\
External calls have an overhead of 100 gas, which can be avoided by not referencing the function using this. Contracts are allowed to override their parents' functions and change the visibility from external to public, so make this change if it's required in order to call the function internally.

**Estimated Gas Savings**\
External calls have an overhead of `100` gas

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


75              try this.decodeString(nameBytes) returns (string memory nameString) {


81              try this.decodeString(symbolBytes) returns (string memory symbolString) {


93              try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93

## [G-13] State variables only set in their definitions should be declared constant

**Issue Description**\
Avoids a Gsset (`20000 gas`) at deployment, and replaces the first access in each transaction (`Gcoldsload - 2100 gas`) and each access thereafter (Gwarmacces - 100 gas) with a PUSH32 (3 gas).

**Estimated Gas Savings**

- `Deployment 20000 gas`
- `Each Transaction  2100 gas`
- `Each access 100 gas`

**Attachments**

- **Code Snippets**

```solidity
File: system-contracts/contracts/SystemContext.sol


37          uint256 public blockGasLimit = type(uint32).max;


41          address public coinbase = BOOTLOADER_FORMAL_ADDRESS;


44          uint256 public difficulty = 2.5e15;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L44

## [G-14] `Calldata` is cheaper than `memory`

**Issue Description**\
The contract functions are currently using `memory` to load and process data. Memory is more expensive in terms of gas costs compared to calldata, especially when the data does not need to be modified within the function.

**Proposed Optimization**\
To optimize the gas costs, we can use `calldata` instead of memory for loading function inputs or data that does not require modification. Calldata is cheaper as it involves fewer operations and lower gas costs compared to memory.

**Estimated Gas Savings**\
The exact gas savings will depend on the size of the data being processed and the frequency of function calls. However, using calldata can result in significant gas savings, especially for larger data and high-frequency function calls.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 17 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  168             L2Log memory _log,


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L168

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/IBridgehub.sol


  85              L2Log memory _log,


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L85

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  200             StoredBatchInfo memory _lastCommittedBatchData,


  209             StoredBatchInfo memory _lastCommittedBatchData,


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L209

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  67              L2Log memory _log,


  57              L2Message memory _message,


  48              BridgehubL2TransactionRequest memory _request


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L48

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol


  34              L2Log memory _log,


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IMailbox.sol#L34

  ```solidity
  File: contracts/zksync/contracts/L2ContractHelper.sol


  65          function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable;


  22          function sendToL1(bytes memory _message) external returns (bytes32);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L22

  ```solidity
  File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


  114             string memory _newSymbol,


  178         function decodeString(bytes memory _input) external pure returns (string memory result) {


  183         function decodeUint8(bytes memory _input) external pure returns (uint8 result) {


  50          function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {


  113             string memory _newName,


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L113

  ```solidity
  File: system-contracts/contracts/L2BaseToken.sol


  85          function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable override {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L85

    </details>

## [G-15] Internal functions only called once can be `inlined` to save gas

**Issue Description**\
The issue is related to the gas cost associated with function calls in contracts. When a function is not inlined, it requires additional instructions and stack operations, resulting in higher gas consumption.

**Proposed Optimization**\
To optimize gas usage, it is recommended to inline small functions whenever possible. Inlining a function eliminates the need for additional instructions and stack operations associated with function calls, leading to gas savings.

**Estimated Gas Savings**\
Not inlining a function costs approximately 20 to 40 gas due to the following factors:

- Two extra JUMP instructions (one for the function call and one for the return)
- Additional stack operations needed for function calls

By inlining small functions, the estimated gas savings range from 20 to 40 gas per function call.
**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 79 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  160         function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  254         function _getERC20Getters(address _token) internal view returns (bytes memory) {


  458         function _checkWithdrawal(


  487         function _parseL2WithdrawalMessage(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L487

  ```solidity
  File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


  49          function bytecodeLen(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L49

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  177         function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  130         function _processL2Logs(


  625         function _verifyBlobInformation(


  103         function _verifyBatchTimestamp(


  500         function _createBatchCommitment(


  592         function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) {


  597         function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) {


  253         function _commitBatchesWithoutSystemContractsUpgrade(


  273         function _commitBatchesWithSystemContractsUpgrade(


  308         function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash) {


  321         function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {


  453         function _getBatchProofPublicInput(


  515         function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory) {


  525         function _batchMetaParameters() internal view returns (bytes memory) {


  537         function _batchAuxiliaryOutput(


  561         function _encodeBlobAuxilaryOutput(


  605         function _pointEvaluationPrecompile(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  130         function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory) {


  258         function _requestL2Transaction(


  316         function _writePriorityOp(


  353         function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) {


  289         function _serializeL2Transaction(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol


  109         function getTransactionBodyGasLimit(


  69          function getMinimalPriorityTransactionGasLimit(


  128         function getOverheadForTransaction(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L128

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  236         function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {


  163         function _upgradeVerifier(address _newVerifier, VerifierParams calldata _verifierParams) internal {


  171         function _setBaseSystemContracts(bytes32 _bootloaderHash, bytes32 _defaultAccountHash) internal {


  180         function _setL2SystemContractUpgrade(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


  20          function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20

  ```solidity
  File: contracts/zksync/contracts/SystemContractsCaller.sol


  95          function getFarCallABI(


  37          function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {


  121         function getFarCallABIWithEmptyFatPointer(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L121

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  109         function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {


  164         function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {


  138         function _getL1WithdrawMessage(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L138

  ```solidity
  File: system-contracts/contracts/BootloaderUtilities.sol


  44          function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {


  229         function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {


  139         function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L139

  ```solidity
  File: system-contracts/contracts/Compressor.sol


  197         function _decodeRawBytecode(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L197

  ```solidity
  File: system-contracts/contracts/ContractDeployer.sol


  283         function _performDeployOnAddress(


  309         function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L309

  ```solidity
  File: system-contracts/contracts/DefaultAccount.sol


  78          function _validateTransaction(


  159         function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {


  131         function _execute(Transaction calldata _transaction) internal {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L131

  ```solidity
  File: system-contracts/contracts/KnownCodesStorage.sol


  74          function _validateBytecode(bytes32 _bytecodeHash) internal pure {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L74

  ```solidity
  File: system-contracts/contracts/L1Messenger.sol


  61          function sha256GasCost(uint256 _length) internal pure returns (uint256) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L61

  ```solidity
  File: system-contracts/contracts/L2BaseToken.sol


  112         function _getL1WithdrawMessage(address _to, uint256 _amount) internal pure returns (bytes memory) {


  117         function _getExtendedWithdrawMessage(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L117

  ```solidity
  File: system-contracts/contracts/MsgValueSimulator.sol


  25          function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L25

  ```solidity
  File: system-contracts/contracts/SystemContext.sol


  233         function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) {


  241         function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {


  221         function _calculateL2BlockHash(


  263         function _setVirtualBlock(


  427         function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L427

  ```solidity
  File: system-contracts/contracts/libraries/EfficientCall.sol


  124         function rawCall(


  159         function rawStaticCall(uint256 _gas, address _address, bytes calldata _data) internal view returns (bool success) {


  173         function rawDelegateCall(uint256 _gas, address _address, bytes calldata _data) internal returns (bool success) {


  191         function rawMimicCall(


  232         function propagateRevert() internal pure {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L232

  ```solidity
  File: system-contracts/contracts/libraries/SystemContractHelper.sol


  203         function getZkSyncMetaBytes() internal view returns (uint256 meta) {


  227         function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) {


  237         function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) {


  246         function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) {


  254         function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) {


  263         function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) {


  272         function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) {


  296         function getCallFlags() internal view returns (uint256 callFlags) {


  148         function unsafePrecompileCall(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L148

  ```solidity
  File: system-contracts/contracts/libraries/SystemContractsCaller.sol


  76          function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {


  123         function systemCallWithReturndata(


  250         function getFarCallABIWithEmptyFatPointer(


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L250

  ```solidity
  File: system-contracts/contracts/libraries/Utils.sol


  44          function bytecodeLenInWords(bytes32 _bytecodeHash) internal pure returns (uint256 codeLengthInWords) {


  71          function constructedBytecodeHash(bytes32 _bytecodeHash) internal pure returns (bytes32) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L71

    </details>

## [G-16] Multiple `address/ID` mappings can be combined into a single mapping of an `address/ID` to a struct

**Issue Description**\
Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset `20000 gas` per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save `~42` gas per access due to not having to recalculate the key's keccak256 hash `Gkeccak256 - 30 gas` and that calculation's associated stack operations.

**Proposed Optimization**\
To optimize the gas costs, we can combine multiple address/ID mappings into a single mapping of an address/ID to a struct, where appropriate. This can save a storage slot for the mapping and avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, this can save ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 14 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  32          mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount)))

  45          mapping(address => uint256) private __DEPRECATED_lastWithdrawalLimitReset;

  48          mapping(address => uint256) private __DEPRECATED_withdrawnAmountInWindow;

  51          mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L45

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  48          mapping(uint256 chainId => address l2Bridge) public override l2BridgeAddress;

  52          mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash))

  57          mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)))

  61          mapping(uint256 chainId => bool enabled) internal hyperbridgingEnabled;

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  26          mapping(uint256 _chainId => address) public stateTransitionManager;

  29          mapping(uint256 _chainId => address) public baseToken;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L26

  ```solidity
  File: system-contracts/contracts/ImmutableSimulator.sol


  21          mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21

  ```solidity
  File: system-contracts/contracts/NonceHolder.sol


  36          mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;

  41          mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36

    </details>

## [G-17] Using storage instead of `memory` for structs/arrays saves gas

**Issue Description**\
When fetching data from a storage location, assigning the data to a memory variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (`2100 gas`) for each field of the `struct/array`. If the fields are read from the new memory variable, they incur an additional MLOAD rather than a cheap stack read. Instead of declearing the variable with the memory keyword, declaring the variable with the storage keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a memory variable, is if the full struct/array is being returned by the function, is being passed to a function that requires memory, or if the array/struct is being read from another memory array/struct

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 15 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


  27              Diamond.SelectorToFacet memory facet = diamondStorage.selectorToFacet[msg.sig];


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L27

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


  72              FeeParams memory oldFeeParams = s.feeParams;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L72

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  396             VerifierParams memory verifierParams = s.verifierParams;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L396

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


  210                 Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  157             FeeParams memory feeParams = s.feeParams;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L157

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


  140                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];


  160                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];


  180                 SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L180

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  155             VerifierParams memory oldVerifierParams = s.verifierParams;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155

  ```solidity
  File: system-contracts/contracts/ContractDeployer.sol


  41              AccountInfo memory info = accountInfo[_address];


  75              AccountInfo memory currentInfo = accountInfo[msg.sender];


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L75

  ```solidity
  File: system-contracts/contracts/SystemContext.sol


  135             VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo;


  173             BlockInfo memory batchInfo = currentBatchInfo;


  181             BlockInfo memory blockInfo = currentL2BlockInfo;


  275             BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L275

    </details>

## [G-18] Multiple accesses of a `mapping/array` should use a local variable cache

**Issue Description**\
The instances below point to the second+ access of a value inside a mapping/array, within a function. Caching a mapping's value in a local storage or calldata variable when the value is accessed multiple times, saves ~42 gas per access due to not having to recalculate the key's keccak256 hash (Gkeccak256 - 30 gas) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into memory/calldata

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 49 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  187             delete depositAmount[_depositSender][_l1Token][_l2TxHash];


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  123                     chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +


  133                 chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;


  221                     l2Contract: l2BridgeAddress[_chainId],


  238             depositHappened[_chainId][_txHash] = _txDataHash;


  343                     delete depositHappened[_chainId][_l2TxHash];


  350                 chainBalance[_chainId][_l1Token] -= _amount;


  418             isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;


  440                 chainBalance[_chainId][l1Token] -= amount;


  586                     l2Contract: l2BridgeAddress[ERA_CHAIN_ID],


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L586

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  87              stateTransitionManagerIsRegistered[_stateTransitionManager] = true;


  97              stateTransitionManagerIsRegistered[_stateTransitionManager] = false;


  103             tokenIsRegistered[_token] = true;


  134             stateTransitionManager[_chainId] = _stateTransitionManager;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  226                 (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  282             stateTransition[_chainId] = stateTransitionAddress;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L282

  ```solidity
  File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


  82              validators[_chainId][_newValidator] = true;


  91              validators[_chainId][_validator] = false;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  66                  blobHashes[0] = logOutput.blob1Hash;


  333             s.l2LogsRootHashes[currentBatchNumber] = _storedBatch.l2LogsTreeRoot;


  353                 emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);


  408                     _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],


  412                 bytes32 currentBatchCommitment = _committedBatches[i].commitment;


  670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),


  670                         (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L670

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


  170                 bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];


  184             return ds.selectorToFacet[_selector].isFreezable;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L184

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


  105                 bytes4[] memory selectors = facetCuts[i].selectors;


  195                 ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();


  223             ds.facetToSelectors[_facet].selectors.push(_selector);


  247             delete ds.selectorToFacet[_selector];


  244             ds.facetToSelectors[_facet].selectors.pop();


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L244

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


  61                  _map.map[mapIndex] = (newValueXorOldValue << bitOffset) ^ mapValue;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L61

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Merkle.sol


  32                      : _efficientHash(_path[i], currentHash);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L32

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol


  79              delete _queue.data[head];


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L79

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  99                  l1TokenAddress[expectedL2Token] = _l1Token;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L99

  ```solidity
  File: system-contracts/contracts/BootloaderUtilities.sol


  96                  if (_transaction.reserved[0] != 0) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L96

  ```solidity
  File: system-contracts/contracts/Compressor.sol


  174                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L174

  ```solidity
  File: system-contracts/contracts/ContractDeployer.sol


  254                 this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254

  ```solidity
  File: system-contracts/contracts/ImmutableSimulator.sol


  40                      bytes32 value = _immutables[i].value;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L40

  ```solidity
  File: system-contracts/contracts/L1Messenger.sol


  225                     l2ToL1LogsTreeArray[i] = keccak256(


  289             uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L289

  ```solidity
  File: system-contracts/contracts/L2BaseToken.sol


  43                  balance[_from] = fromBalance - _amount;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L43

  ```solidity
  File: system-contracts/contracts/NonceHolder.sol


  72                  rawNonces[addressAsKey] = (oldRawNonce + _value);


  118                 rawNonces[addressAsKey] = oldRawNonce + 1;


  144                 rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L144

  ```solidity
  File: system-contracts/contracts/libraries/RLPEncoder.sol


  34                      encoded[0] = bytes1(uint8(hbs + 0x81));


  69                      encoded[0] = bytes1(uint8(_offset + hbs + 56));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L69

  ```solidity
  File: system-contracts/contracts/libraries/TransactionHelper.sol


  184             if (_transaction.reserved[0] != 0) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L184

    </details>

## [G-19] `Stack variable` used as a cheaper cache for a state variable is only used once

**Issue Description**\
If the variable is only accessed once, it's cheaper to use the state variable directly that one time, and save the 3 gas the extra stack assignment would spend.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 13 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  342                     require(dataHash == txDataHash, "ShB: d.it not hap");


  325                 require(proofValid, "yn");


  484             require(success, "ShB withd w proof"); // withdrawal wrong proof


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  56              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);


  69              emit NewAdmin(previousAdmin, pendingAdmin);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  115             emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);


  128             emit NewAdmin(previousAdmin, pendingAdmin);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L128

  ```solidity
  File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


  195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


  195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


  217                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


  217                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217

  ```solidity
  File: system-contracts/contracts/SystemContext.sol


  352                     _l2BlockTimestamp >= currentBatchTimestamp,


  430                 _newTimestamp > currentBlockTimestamp,


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L430

    </details>

## [G-20] `require()` statements that check input arguments should be at the top of the function

**Issue Description**\
Checks that involve constants should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting a Gcoldsload (2100 gas\*) in a function that may ultimately revert in the unhappy case.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 6 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


  25              require(msg.data.length >= 4 || msg.data.length == 0, "Ut");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  631             require(_pubdataCommitments.length > 0, "pl");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


  155             require(_facet.code.length > 0, "K");


  132             require(_facet.code.length > 0, "G");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  205             require(
  206                 _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
  207                 "The new protocol version should be included in the L2 system upgrade tx"
  208             );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205

  ```solidity
  File: system-contracts/contracts/NonceHolder.sol


  85              require(_value != 0, "Nonce value cannot be set to 0");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/contracts/NonceHolder.sol#L85

    </details>

## [G-21] Use solidity version `0.8.20` or above to improve gas performance

Upgrade to the latest solidity version 0.8.20 to get additional gas savings. See the latest release for reference: https://blog.soliditylang.org/2023/05/10/solidity-0.8.20-release-announcement/

**All Contracts**

## [G-22] Expression `is cheaper than`new bytes(0)

**Issue Description**\
The expression `new bytes(0)` is used, which consumes more gas than necessary. This expression creates a new byte array of length 0, which is then stored in memory or storage, depending on the context.

**Proposed Optimization**\
Replace the expression `new bytes(0)` with "" (an empty string) to save gas.

An empty string is equivalent to a byte array of length 0. However, the expression "" is cheaper in terms of gas compared to new bytes(0). This is because new bytes(0) is a dynamic array, and its creation involves more opcodes and therefore consumes more gas. In contrast, "" is a static array and requires fewer opcodes to create.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 8 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  196                 signature: new bytes(0),


  198                 paymasterInput: new bytes(0),


  199                 reservedDynamic: new bytes(0)


  213                 l1ContractsUpgradeCalldata: new bytes(0),


  214                 postUpgradeCalldata: new bytes(0),


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L214

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  308                 signature: new bytes(0),


  310                 paymasterInput: new bytes(0),


  311                 reservedDynamic: new bytes(0)


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L311

    </details>

## [G-23] Initializers can be marked `payable`

**Issue Description**\
`Payable` functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. An initializer can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 8 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  60          function initialize() external reentrancyGuardInitializer {}


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  104         function initialize(
  105             address _owner,
  106             uint256 _eraFirstPostUpgradeBatch
  107         ) external reentrancyGuardInitializer initializer {

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L104

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  41          function initialize(address _owner) external reentrancyGuardInitializer {
  42              _transferOwnership(_owner);
  43          }


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L41

  ```solidity
  File: contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol


  65          function initialize(StateTransitionManagerInitializeData calldata _initalizeData) external;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/IStateTransitionManager.sol#L65

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  79          function initialize(
  80              StateTransitionManagerInitializeData calldata _initializeData
  81          ) external reentrancyGuardInitializer {

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L79

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


  24          function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32) {

  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L24

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol


  62          function initialize(InitializeData calldata _initData) external returns (bytes32);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L62

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  49          function initialize(
  50              address _l1Bridge,
  51              address _l1LegecyBridge,
  52              bytes32 _l2TokenProxyBytecodeHash,
  53              address _aliasedOwner
  54          ) external reinitializer(2) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L49

    </details>

## [G-24] Use assembly to `emit` events

**Issue Description**\
Using the [scratch space](https://github.com/Vectorized/solady/blob/30558f5402f02351b96eeb6eaf32bcea29773841/src/tokens/ERC1155.sol#L501-L504) for event arguments (two words or fewer) will save gas over needing Solidity's full abi memory expansion used for emitting normally.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 77 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  155             emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);


  199             emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);


  225             emit WithdrawalFinalized(l1Receiver, l1Token, amount);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  168             emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);


  227             emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);


  239             emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);


  367             emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);


  454             emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);


  602             emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  56              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);


  68              emit NewPendingAdmin(currentPendingAdmin, address(0));


  69              emit NewAdmin(previousAdmin, pendingAdmin);


  145             emit NewChain(_chainId, _stateTransitionManager, _admin);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  47              emit ChangeSecurityCouncil(address(0), _securityCouncil);


  50              emit ChangeMinDelay(0, _minDelay);


  132             emit TransparentOperationScheduled(id, _delay, _operation);


  144             emit ShadowOperationScheduled(_id, _delay);


  157             emit OperationCancelled(_id);


  180             emit OperationExecuted(id);


  199             emit OperationExecuted(id);


  250             emit ChangeMinDelay(minDelay, _newDelay);


  257             emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  115             emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);


  127             emit NewPendingAdmin(currentPendingAdmin, address(0));


  128             emit NewAdmin(previousAdmin, pendingAdmin);


  227             emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);


  235             emit StateTransitionNewChain(_chainId, _stateTransitionContract);


  287             emit StateTransitionNewChain(_chainId, stateTransitionAddress);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287

  ```solidity
  File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


  83              emit ValidatorAdded(_chainId, _newValidator);


  92              emit ValidatorRemoved(_chainId, _validator);


  98              emit NewExecutionDelay(_executionDelay);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


  28              emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);


  40              emit NewPendingAdmin(pendingAdmin, address(0));


  41              emit NewAdmin(previousAdmin, pendingAdmin);


  47              emit ValidatorStatusUpdate(_validator, _active);


  54              emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);


  63              emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);


  75              emit NewFeeParams(oldFeeParams, _newFeeParams);


  86              emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);


  92              emit ValidiumModeStatusUpdate(_validiumMode);


  115             emit ExecuteUpgrade(_diamondCut);


  125             emit ExecuteUpgrade(_diamondCut);


  139             emit Freeze();


  149             emit Unfreeze();


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  261                 emit BlockCommit(
  262                     _lastCommittedBatchData.batchNumber,
  263                     _lastCommittedBatchData.batchHash,
  264                     _lastCommittedBatchData.commitment
  265                 );


  299                 emit BlockCommit(
  300                     _lastCommittedBatchData.batchNumber,
  301                     _lastCommittedBatchData.batchHash,
  302                     _lastCommittedBatchData.commitment
  303                 );


  353                 emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);


  436             emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);


  496             emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  343             emit NewPriorityRequest(
  344                 _priorityOpParams.txId,
  345                 canonicalTxHash,
  346                 _priorityOpParams.expirationTimestamp,
  347                 transaction,
  348                 _factoryDeps
  349             );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L343

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


  121             emit DiamondCut(facetCuts, initAddress, initCalldata);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L121

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  87              emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);


  104             emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash);


  121             emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash);


  137             emit NewVerifier(address(oldVerifier), address(_newVerifier));


  157             emit NewVerifierParams(oldVerifierParams, _newVerifierParams);


  256             emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L256

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol


  40              emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);


  67              emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L67

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  105             emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);


  134             emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134

  ```solidity
  File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


  101             emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);


  126             emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);


  147             emit BridgeMint(_to, _amount);


  156             emit BridgeBurn(_from, _amount);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156

  ```solidity
  File: system-contracts/contracts/ContractDeployer.sol


  68              emit AccountVersionUpdated(msg.sender, _version);


  86              emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);


  355             emit ContractDeployed(_sender, _bytecodeHash, _newAddress);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355

  ```solidity
  File: system-contracts/contracts/KnownCodesStorage.sol


  59                  emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L59

  ```solidity
  File: system-contracts/contracts/L1Messenger.sol


  111             emit L2ToL1LogSent(_l2ToL1Log);


  156             emit L1MessageSent(msg.sender, hash, _message);


  181             emit BytecodeL1PublicationRequested(_bytecodeHash);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181

  ```solidity
  File: system-contracts/contracts/L2BaseToken.sol


  49              emit Transfer(_from, _to, _amount);


  67              emit Mint(_account, _amount);


  79              emit Withdrawal(msg.sender, _l1Receiver, amount);


  92              emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92

  ```solidity
  File: system-contracts/contracts/NonceHolder.sol


  96              emit ValueSetUnderNonce(msg.sender, _key, _value);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96

    </details>

## [G-25] Don't compare boolean expressions to `boolean` literals

**Issue Description**\
For cases of: `if (<x> == true)`, use `if (<x>)` instead. For cases of: `if (<x> == false)`, use `if (!<x>)` instead.

**Proposed Optimization**\
Replace the boolean comparison `validators[_chainId][msg.sender] == true` with `validators[_chainId][msg.sender]` to simplify the code and reduce gas consumption.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


68              require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68

## [G-26] Don't use `_msgSender()` if not supporting EIP-2771

**Issue Description**\
Use `msg.sender` if the code does not implement [EIP-2771 trusted forwarder](https://eips.ethereum.org/EIPS/eip-2771) support

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol


65              address _msgSender,


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1SharedBridge.sol#L65

## [G-27] Fewer storage slots can be used by storing timestamps in types smaller than `uint256`

**Issue Description**\
The current implementation uses `uint256` variables to store timestamps in multiple contracts. However, Ethereum's block timestamps can be stored in a type smaller than uint256, such as uint32. A uint32 variable can store a timestamp until the year 2106. Using smaller data types can help reduce gas consumption by requiring fewer storage slots.

**Proposed Optimization**\
Replace the `uint256` variables used to store timestamps with `uint32` variables to reduce the number of storage slots required.

**Estimated Gas Savings**\

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol


34          uint256 packedBatchAndL2BlockTimestamp;


90              uint256 timestamp;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L90

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


37          uint256 upgradeTimestamp;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L37

## [G-28] `keccak256()` should only need to be called on a specific string literal once:

**Issue Description**\
It should be saved to an immutable variable, and the variable used instead. If the hash is being used as a part of a function selector, the cast to `bytes4` should also only be done once.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 4 findings</summary>

  ```solidity
  File: system-contracts/contracts/libraries/TransactionHelper.sol


  85              keccak256(
  86                  "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
  87              );


  85              keccak256(
  86                  "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
  87              );


  139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)


  139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L139

    </details>

## [G-29] `Emit` Used In Loop

**Issue Description**\
`Emitting` an event inside a loop performs a LOG op N times, where N is the loop length. Consider refactoring the code to emit the event only once at the end of loop. Gas savings should be multiplied by the average loop length.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


261                 emit BlockCommit(


299                 emit BlockCommit(


353                 emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353

## [G-30] Private functions used once can be `inlined`

**Issue Description**\
Private functions that are used only once in the contract can consume more gas than necessary. This is because the EVM must perform a JUMP operation to call the function, which incurs a gas cost.

**Proposed Optimization**\
To optimize the gas usage, private functions that are used only once can be inlined. This means that the code of the function is copied directly into the calling function, eliminating the need for a JUMP operation.

**Estimated Gas Savings**\
The estimated gas savings will depend on the size and complexity of the private function being inlined. However, inlining a private function can save an estimated 20-40 gas per call.

**Attachments**

- **Code Snippets**

<details>
<summary>Click to show 15 findings</summary>

```solidity
File: contracts/ethereum/contracts/common/ReentrancyGuard.sol


46          function _initializeReentrancyGuard() private {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L46

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


126         function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {


149         function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {

172         function _removeFunctions(address _facet, bytes4[] memory _selectors) private {

257         function _removeFacet(address _facet) private {

278         function _initializeDiamondCut(address _init, bytes memory _calldata) private {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278

```solidity
File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


92          function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private {


109         function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private {

126         function _setVerifier(IVerifier _newVerifier) private {

142         function _setVerifierParams(VerifierParams calldata _newVerifierParams) private {

222         function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L222

```solidity
File: system-contracts/contracts/libraries/TransactionHelper.sol


118         function _encodeHashEIP712Transaction(Transaction calldata _transaction) private view returns (bytes32) {

147         function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32) {

219         function _encodeHashEIP2930Transaction(Transaction calldata _transaction) private view returns (bytes32) {

289         function _encodeHashEIP1559Transaction(Transaction calldata _transaction) private view returns (bytes32) {

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L289

</details>

## [G-31] `State variable` read in loops

**Issue Description**\
The state variable should be cached in and read from a local variable, or accumulated in a local variable then written to storage once outside of the loop, rather than reading/updating it on every iteration of the loop, which will replace each `Gwarmaccess` `(100 gas)` with a much cheaper stack read.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 5 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


  117                     committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);


  136                     committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);


  186                     uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(


  210                     uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210

  ```solidity
  File: system-contracts/contracts/ImmutableSimulator.sol


  41                      immutableDataStorage[uint256(uint160(_dest))][index] = value;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L41

    </details>

## [G-32] Storage `re-read` via storage pointer

**Issue Description**\
The instances below point to the second+ access of a state variable, via a storage pointer, within a function. Caching the value replaces each Gwarmaccess (`100 gas`) with a much cheaper stack read.

**Proposed Optimization**\
Cache the value of the state variable in memory the first time it is accessed, and then use the cached value for subsequent reads within the function. This replaces each Gwarmaccess (100 gas) call with a much cheaper stack read.

**Estimated Gas Savings**\
Each `Gwarmaccess` call that is replaced with a stack read can potentially save up to 99 gas. The actual gas savings will depend on the number of times the state variable is accessed within the function.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


91              return state == OperationState.Waiting || state == OperationState.Ready;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L91

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


113                 } else if (action == Action.Remove) {


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L113

## [G-33] Avoid fetching a low-level call's return data by using `assembly`

**Issue Description**\
Even if you don't assign the call's second return value, it still gets copied to memory. Use assembly instead to prevent this and save 159 gas.

**Proposed Optimization**\
Use assembly to avoid fetching the return data when it is not needed, which can save 159 gas.

**Estimated Gas Savings**\
By using assembly to avoid fetching the return data, we can potentially save 159 gas per low-level call that does not require return data.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/GasBoundCaller.sol


57              bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/GasBoundCaller.sol#L57

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


226                 (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol


63                  (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call(
64                      abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65                  );


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/contracts/MsgValueSimulator.sol#L63

## [G-34] Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead

**Issue Description**\
Usage of uints/ints smaller than 32 bytes (256 bits) in the contract can incur overhead and increase gas usage. This is because the EVM operates on 32 bytes at a time, and if the element is smaller than that, the EVM must use more operations to reduce the size of the element from 32 bytes to the desired size.

**Proposed Optimization**\
To optimize the gas usage, use a larger size (uint256 or int256) and then downcast to the desired size where needed. This can save gas as each operation involving a smaller size (e.g. uint8) can cost an extra 22-28 gas (depending on whether the other operand is also a variable of the same type) compared to operations involving uint256 or int256.

**Estimated Gas Savings**\
The estimated gas savings will depend on the number of operations involving smaller uints/ints in the contract. However, using a larger size and downcasting where needed can save an estimated `22-28` gas per operation.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 20 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


  40              uint8 version = uint8(_bytecodeHash[0]);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  39              uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39

  ```solidity
  File: contracts/ethereum/contracts/state-transition/libraries/LibMap.sol


  54                  uint32 oldValue = uint32(mapValue >> bitOffset);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L54

  ```solidity
  File: system-contracts/contracts/Compressor.sol


  65                      uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);


  66                      uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);


  161                 uint64 enumIndex = stateDiff.readUint64(84);


  174                 uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));


  177                 uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L177

  ```solidity
  File: system-contracts/contracts/KnownCodesStorage.sol


  75              uint8 version = uint8(_bytecodeHash[0]);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75

  ```solidity
  File: system-contracts/contracts/L1Messenger.sol


  200             uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));


  233             uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));


  237                 uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));


  251             uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));


  255                 uint32 currentBytecodeLength = uint32(


  286             uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L286

  ```solidity
  File: system-contracts/contracts/SystemContext.sol


  278                 uint128 currentBatchNumber = currentBatchInfo.number;


  409             (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();


  428             uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;


  450             (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();


  450             (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L450

    </details>

## [G-35] Use assembly to calculate `hashes` to save gas

**Issue Description**\
Using assembly to calculate hashes can save 80 gas per instance

**Proposed Optimization**\
Use inline assembly to perform operations on data of size 96 bytes or less, such as hashing and unindexed data in events. We can utilize Solidity's scratch space and the free memory pointer space to optimize memory operations.

**Estimated Gas Savings**\
The gas savings will depend on the specific operation and the size of the data. However, by utilizing inline assembly for operations on data of size 96 bytes or less, we can potentially save gas by avoiding memory expansion.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 60 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  76              bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


  210             bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));


  341                     bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));


  598             bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598

  ```solidity
  File: contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol


  12          bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");


  67              bytes32 data = keccak256(
  68                  bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
  69              );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L67

  ```solidity
  File: contracts/ethereum/contracts/governance/Governance.sol


  205             return keccak256(abi.encode(_operation));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  100             storedBatchZero = keccak256(abi.encode(batchZero));


  102             initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));


  138             initialCutHash = keccak256(abi.encode(_diamondCut));


  147             upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));


  156             upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));


  255             bytes32 cutHashInput = keccak256(_diamondCut);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L255

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


  104             bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


  63                          keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),


  313                 concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));


  460                     keccak256(
  461                         abi.encodePacked(
  462                             _prevBatchCommitment,
  463                             _currentBatchCommitment,
  464                             _verifierParams.recursionNodeLevelVkHash,
  465                             _verifierParams.recursionLeafLevelVkHash
  466                         )
  467                     )


  506             bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData));


  507             bytes32 metadataHash = keccak256(_batchMetaParameters());


  508             bytes32 auxiliaryOutputHash = keccak256(
  509                 _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
  510             );


  512             return keccak256(abi.encode(passThroughDataHash, metadataHash, auxiliaryOutputHash));


  545             bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);


  588             return keccak256(abi.encode(_storedBatchInfo));


  654                 blobCommitments[versionedHashIndex] = keccak256(
  655                     abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
  656                 );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654

  ```solidity
  File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


  112             bytes32 hashedLog = keccak256(
  113                 abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
  114             );


  138                     value: keccak256(_message.data)


  332             canonicalTxHash = keccak256(transactionEncoding);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L332

  ```solidity
  File: contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol


  212             bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L212

  ```solidity
  File: contracts/zksync/contracts/L2ContractHelper.sol


  85          bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2");


  108             bytes32 data = keccak256(
  109                 bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
  110             );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L108

  ```solidity
  File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


  150             bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150

  ```solidity
  File: system-contracts/contracts/BootloaderUtilities.sol


  29                  txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature)));


  120                 keccak256(
  121                     bytes.concat(
  122                         encodedListLength,
  123                         encodedNonce,
  124                         encodedGasParam,
  125                         encodedTo,
  126                         encodedValue,
  127                         encodedDataLength,
  128                         _transaction.data,
  129                         vEncoded,
  130                         rEncoded,
  131                         sEncoded
  132                     )
  133                 );


  211                 keccak256(
  212                     bytes.concat(
  213                         "\x01",
  214                         encodedListLength,
  215                         encodedFixedLengthParams,
  216                         encodedDataLength,
  217                         _transaction.data,
  218                         encodedAccessListLength,
  219                         vEncoded,
  220                         rEncoded,
  221                         sEncoded
  222                     )
  223                 );


  306                 keccak256(
  307                     bytes.concat(
  308                         "\x02",
  309                         encodedListLength,
  310                         encodedFixedLengthParams,
  311                         encodedDataLength,
  312                         _transaction.data,
  313                         encodedAccessListLength,
  314                         vEncoded,
  315                         rEncoded,
  316                         sEncoded
  317                     )
  318                 );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L306:318

  ```solidity
  File: system-contracts/contracts/ContractDeployer.sol


  105             bytes32 hash = keccak256(
  106                 bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
  107             );


  121             bytes32 hash = keccak256(
  122                 bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
  123             );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L121

  ```solidity
  File: system-contracts/contracts/L1Messenger.sol


  95              bytes32 hashedLog = keccak256(
  96                  abi.encodePacked(
  97                      _l2ToL1Log.l2ShardId,
  98                      _l2ToL1Log.isService,
  99                      _l2ToL1Log.txNumberInBlock,
  100                     _l2ToL1Log.sender,
  101                     _l2ToL1Log.key,
  102                     _l2ToL1Log.value
  103                 )
  104             );


  106             chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));


  122             chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));


  164             chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash));


  212                 reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));


  225                     l2ToL1LogsTreeArray[i] = keccak256(
  226                         abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
  227                     );


  243                 reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));


  259                 reconstructedChainedL1BytecodesRevealDataHash = keccak256(
  260                     abi.encode(
  261                         reconstructedChainedL1BytecodesRevealDataHash,
  262                         Utils.hashL2Bytecode(
  263                             _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
  264                         )
  265                     )
  266                 );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L259

  ```solidity
  File: system-contracts/contracts/SystemContext.sol


  159                 hash = keccak256(abi.encode(_block));


  227             return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));


  234             return keccak256(abi.encodePacked(uint32(_blockNumber)));


  403             currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403

  ```solidity
  File: system-contracts/contracts/libraries/TransactionHelper.sol


  82          bytes32 constant EIP712_DOMAIN_TYPEHASH = keccak256("EIP712Domain(string name,string version,uint256 chainId)");


  85              keccak256(
  86                  "Transaction(uint256 txType,uint256 from,uint256 to,uint256 gasLimit,uint256 gasPerPubdataByteLimit,uint256 maxFeePerGas,uint256 maxPriorityFeePerGas,uint256 paymaster,uint256 nonce,uint256 value,bytes data,bytes32[] factoryDeps,bytes paymasterInput)"
  87              );


  119             bytes32 structHash = keccak256(
  120                 abi.encode(
  121                     EIP712_TRANSACTION_TYPE_HASH,
  122                     _transaction.txType,
  123                     _transaction.from,
  124                     _transaction.to,
  125                     _transaction.gasLimit,
  126                     _transaction.gasPerPubdataByteLimit,
  127                     _transaction.maxFeePerGas,
  128                     _transaction.maxPriorityFeePerGas,
  129                     _transaction.paymaster,
  130                     _transaction.nonce,
  131                     _transaction.value,
  132                     EfficientCall.keccak(_transaction.data),
  133                     keccak256(abi.encodePacked(_transaction.factoryDeps)),
  134                     EfficientCall.keccak(_transaction.paymasterInput)
  135                 )
  136             );


  133                     keccak256(abi.encodePacked(_transaction.factoryDeps)),


  138             bytes32 domainSeparator = keccak256(
  139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
  140             );


  139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)


  139                 abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)


  142             return keccak256(abi.encodePacked("\x19\x01", domainSeparator, structHash));


  203                 keccak256(
  204                     bytes.concat(
  205                         encodedListLength,
  206                         encodedNonce,
  207                         encodedGasParam,
  208                         encodedTo,
  209                         encodedValue,
  210                         encodedDataLength,
  211                         _transaction.data,
  212                         encodedChainId
  213                     )
  214                 );


  275                 keccak256(
  276                     bytes.concat(
  277                         "\x01",
  278                         encodedListLength,
  279                         encodedFixedLengthParams,
  280                         encodedDataLength,
  281                         _transaction.data,
  282                         encodedAccessListLength
  283                     )
  284                 );


  347                 keccak256(
  348                     bytes.concat(
  349                         "\x02",
  350                         encodedListLength,
  351                         encodedFixedLengthParams,
  352                         encodedDataLength,
  353                         _transaction.data,
  354                         encodedAccessListLength
  355                     )
  356                 );


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L347

    </details>

## [G-36] Duplicated `require()`/`revert()` checks should be refactored to a modifier or function

**Saves deployment costs.**

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


56              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol


92                  require(vInt == 27 || vInt == 28, "Invalid v value");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L92

## [G-37] Use the `inputs/results` of assignments rather than `re-reading` state variables

**Issue Description**\
The issue relates to the inefficient `re-reading` of state variables after they have been assigned a value within the same function. Re-reading state variables incurs additional gas costs due to the need to perform a storage read operation (`Gwarmaccess`).

**Proposed Optimization**\
Instead of re-reading state variables after they have been assigned a value, it is recommended to use the assigned value directly or store it in a local variable. This optimization avoids the unnecessary storage read operation and can lead to gas savings.

**Estimated Gas Savings**\
The estimated gas savings for each instance where a state variable is `re-read` after being assigned is 100 gas (Gwarmaccess). This saving applies to each occurrence of `re-reading` the state variable within the same function or modifier.

**Attachments**

- **Code Snippets**

    <details>
    <summary>Click to show 10 findings</summary>

  ```solidity
  File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


  64              require(msg.sender == address(sharedBridge), "Not shared bridge");


  161             uint256 balanceBefore = _token.balanceOf(address(sharedBridge));


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161

  ```solidity
  File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


  69              emit NewAdmin(previousAdmin, pendingAdmin);


  130             require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130

  ```solidity
  File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


  128             emit NewAdmin(previousAdmin, pendingAdmin);


  192                 nonce: protocolVersion,


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L192

  ```solidity
  File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


  101             emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101

  ```solidity
  File: system-contracts/contracts/SystemContext.sol


  275             BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;


  275             BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;


  277             if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {


  ```

  https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277

    </details>

## [G-38] Assigning state variables directly with named struct constructors wastes gas

**Issue Description**\
Using named arguments for struct means that the compiler needs to organize the fields in memory before doing the assignment, which wastes gas. Set each field directly in storage (use dot-notation), or use the unnamed version of the constructor.

**Proposed Optimization**\
To optimize gas usage, set each field directly in storage using dot-notation, or use the unnamed version of the constructor. This will avoid the need for the compiler to organize the fields in memory before doing the assignment, resulting in gas savings.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/ethereum/contracts/state-transition/libraries/Diamond.sol


218             ds.selectorToFacet[_selector] = SelectorToFacet({


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L218

```solidity
File:

219            request = L2TransactionRequestTwoBridgesInner({

430        MessageParams memory messageParams = MessageParams({

470            l2ToL1Message = L2Message({

584            L2TransactionRequestDirect memory request = L2TransactionRequestDirect({

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L219

```solidity
File:


239            BridgehubL2TransactionRequest({

305            BridgehubL2TransactionRequest({

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L239

```solidity
File:


182        L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({

202        ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({

208            verifierParams: VerifierParams({

220        Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L182

```solidity
File:

92        L2Log memory l2Log = L2Log({

132            L2Log({


208            BridgehubL2TransactionRequest({

294        transaction = L2CanonicalTransaction({

335            PriorityOperation({
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L92

## [G-39] Do not calculate constants

Due to how constant variables are implemented (replacements at compile-time), an expression assigned to a constant variable is recomputed each time that the variable is used, which wastes some gas.

```solidity
File: system-contracts/contracts/NonceHolder.sol


28          uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128;


31          uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32;


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L28

## [G-40] Consider using alternatives to `OpenZeppelin`

**Issue Description**\
OpenZeppelin is a great and popular smart contract library, but there are other alternatives that are worth considering. These alternatives offer better gas efficiency and have been tested and recommended by developers.

Two examples of such alternatives are [Solmate](https://github.com/transmissions11/solmate) and [Solady](https://github.com/Vectorized/solady).

Solmate is a library that provides a number of `gas-efficient` implementations of common smart contract patterns. Solady is another `gas-efficient` library that places a strong emphasis on using assembly.

**Attachments**

- **Code Snippets**

```solidity

import "@openzeppelin/contracts/";

```

## [G-41] Use assembly to write address/contract type storage values

**Issue Description**\
Using assembly { sstore(state.slot, addr) instead of state = addr can save gas.

**Attachments**

- **Code Snippets**

```solidity
File: contracts/governance/Governance.sol

26    address public securityCouncil;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L26

```solidity
File: contracts/bridge/L1ERC20Bridge.sol

46    address public l2Bridge;

49    address public l2TokenBeacon;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L46

```solidity
File: contracts/bridge/L1WethBridge.sol

53    address public l2Bridge;

56    address public l2WethAddress;
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1WethBridge.sol#L53

## [G-42] Use fallback or receive instead of deposit() when transferring Ether

**Issue Description**\
Similar to above, you can “just transfer” ether to a contract and have it respond to the transfer instead of using a payable function. This of course, depends on the rest of the contract’s architecture.

**Proposed Optimization**\
Example Deposit in AAVE

```solidity
contract AddLiquidity{

    receive() external payable {
      IWETH(weth).deposit{msg.value}();
      AAVE.deposit(weth, msg.value, msg.sender, REFERRAL_CODE)
    }

}
```

The fallback function is capable of receiving bytes data which can be parsed with abi.decode. This servers as an alternative to supplying arguments to a deposit function.

**Attachments**

- **Code Snippets**

```solidity
File: ethereum/contracts/bridge/L1ERC20Bridge.sol


98    function deposit(

133    function deposit(
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L98

```solidity
File: contracts/bridge/interfaces/IL1ERC20Bridge.sol

26    function deposit(

35    function deposit(

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol#L26

```solidity
File: ethereum/contracts/bridge/interfaces/IWETH9.sol

5    function deposit() external payable;
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IWETH9.sol#L5

```solidity
File: zksync/contracts/bridge/L2WrappedBaseToken.sol

90    function deposit() external payable override {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2WrappedBaseToken.sol

## [G-43] Using assembly to revert with an error message

**Issue Description**\
When reverting in solidity code, it is common practice to use a require or revert statement to revert execution with an error message. This can in most cases be further optimized by using assembly to revert with the error message.

**Proposed Optimization**\
Here’s an example;

```solidity
/// calling restrictedAction(2) with a non-owner address: 24042
contract SolidityRevert {
    address owner;
    uint256 specialNumber = 1;

    constructor() {
        owner = msg.sender;
    }

    function restrictedAction(uint256 num) external {
        require(owner == msg.sender, "caller is not owner");
        specialNumber = num;
    }
}

/// calling restrictedAction(2) with a non-owner address: 23734
contract AssemblyRevert {
    address owner;
    uint256 specialNumber = 1;

    constructor() {
        owner = msg.sender;
    }

    function restrictedAction(uint256 num) external {
        assembly {
            if sub(caller(), sload(owner.slot)) {
                mstore(0x00, 0x20) // store offset to where length of revert message is stored
                mstore(0x20, 0x13) // store length (19)
                mstore(
                    0x40,
                    0x63616c6c6572206973206e6f74206f776e657200000000000000000000000000
                ) // store hex representation of message
                revert(0x00, 0x60) // revert with data
            }
        }
        specialNumber = num;
    }
}

```

**Estimated Gas Savings**\
From the example above we can see that we get a gas saving of over 300 gas when reverting wth the same error message with assembly against doing so in solidity. This gas savings come from the memory expansion costs and extra type checks the solidity compiler does under the hood.

**Attachments**

- **Code Snippets**

<details>
<summary>Click to show 255 findings</summary>

```solidity
File: contracts/GasBoundCaller.sol


46              require(_maxTotalGas >= gasleft(), "Gas limit is too low");


76                  require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L76

```solidity
File: contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol


64              require(msg.sender == address(sharedBridge), "Not shared bridge");


66              require(amount == _amount, "Incorrect amount");


141             require(_amount != 0, "0T"); // empty deposit


143             require(amount == _amount, "3T"); // The token has non-standard transfer logic


186             require(amount != 0, "2T"); // empty deposit


215             require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215

```solidity
File: contracts/ethereum/contracts/bridge/L1SharedBridge.sol


69              require(msg.sender == address(bridgehub), "ShB not BH");


75              require(


84              require(msg.sender == address(legacyBridge), "ShB not legacy bridge");


108             require(_owner != address(0), "ShB owner 0");


121                 require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");


129                 require(amount > 0, "ShB: 0 amount to transfer");


132                 require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");


138             require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition");


155                 require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");


158                 require(msg.value == 0, "ShB m.v > 0 b d.it");


161                 require(amount == _amount, "3T"); // The token has non-standard transfer logic


188             require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");


194             require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");


195             require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");


200                 require(_depositAmount == 0, "ShB wrong withdraw amount");


202                 require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");


206                 require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic


208             require(amount != 0, "6T"); // empty deposit amount


237             require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap");


325                 require(proofValid, "yn");


327             require(_amount > 0, "y1");


342                     require(dataHash == txDataHash, "ShB: d.it not hap");


349                 require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");


360                 require(callSuccess, "ShB: claimFailedDeposit failed");


396                 require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");


417             require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");


427                 require(!alreadyFinalized, "Withdrawal is already finalized 2");


439                 require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); // not enought funds


449                 require(callSuccess, "ShB: withdraw failed");


484             require(success, "ShB withd w proof"); // withdrawal wrong proof


501             require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length


517                 require(_l2ToL1message.length == 76, "ShB wrong msg len 2");


563             require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");


564             require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564

```solidity
File: contracts/ethereum/contracts/bridgehub/Bridgehub.sol


46              require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");


62              require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights


83              require(


93              require(


102             require(!tokenIsRegistered[_token], "Bridgehub: token already registered");


122             require(_chainId != 0, "Bridgehub: chainId cannot be 0");


123             require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");


125             require(


129             require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");


130             require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");


132             require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");


223                     require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");


225                     require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");


269                     require(


275                     require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");


296             require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");


300             require(


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300

```solidity
File: contracts/ethereum/contracts/governance/Governance.sol


42              require(_admin != address(0), "Admin should be non zero address");


59              require(msg.sender == address(this), "Only governance contract itself is allowed to call this function");


65              require(msg.sender == securityCouncil, "Only security council is allowed to call this function");


71              require(


155             require(isOperationPending(_id), "Operation must be pending");


172             require(isOperationReady(id), "Operation must be ready before execution");


177             require(isOperationReady(id), "Operation must be ready after execution");


191             require(isOperationPending(id), "Operation must be pending before execution");


196             require(isOperationPending(id), "Operation must be pending after execution");


216             require(!isOperation(_id), "Operation with this proposal id already exists");


217             require(_delay >= minDelay, "Proposed delay is less than minimum delay");


240             require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240

```solidity
File: contracts/ethereum/contracts/state-transition/StateTransitionManager.sol


64              require(msg.sender == bridgehub, "StateTransition: only bridgehub");


70              require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");


82              require(_initializeData.governor != address(0), "StateTransition: governor zero");


121             require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights


256             require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256

```solidity
File: contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol


62              require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin");


68              require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator");


195                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


217                     require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol


25              require(address(_initializeData.verifier) != address(0), "vt");


26              require(_initializeData.admin != address(0), "vy");


27              require(_initializeData.validatorTimelock != address(0), "hc");


28              require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol


14              require(_chainId == block.chainid, "pr");


25              require(msg.data.length >= 4 || msg.data.length == 0, "Ut");


30              require(facetAddress != address(0), "F"); // Proxy has no facet for this selector


31              require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol


34              require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights


59              require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");


70              require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");


90              require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); // Validium mode can be set only before the first batch is committed


105             require(


110             require(


116             require(


136             require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already


146             require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol


37              require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); // only commit next batch


40              require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");


50                  require(logOutput.pubdataHash == 0x00, "v0h");


51                  require(_newBatch.pubdataCommitments.length == 1);


61                  require(


74              require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");


76              require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");


78              require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");


110             require(batchTimestamp == _expectedBatchTimestamp, "tb");


114             require(_previousBatchTimestamp < batchTimestamp, "h3");


122             require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); // New batch timestamp is too small


123             require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); // The last L2 block timestamp is too big


149                 require(!_checkBit(processedLogs, uint8(logKey)), "kp");


154                     require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");


157                     require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");


160                     require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");


163                     require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");


166                     require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");


169                     require(logSender == L2_BOOTLOADER_ADDRESS, "bl");


172                     require(logSender == L2_BOOTLOADER_ADDRESS, "bk");


175                     require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");


178                     require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");


181                     require(logSender == L2_BOOTLOADER_ADDRESS, "bu");


182                     require(_expectedSystemContractUpgradeTxHash == logValue, "ut");


192                 require(processedLogs == 511, "b7");


194                 require(processedLogs == 1023, "b8");


226             require(


231             require(_newBatchesData.length == 1, "e4");


233             require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data


284             require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik");


323             require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k"); // Execute batches in order


324             require(


330             require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x"); // priority operations hash does not match to expected


358             require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.


402             require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1");


407                 require(


421             require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");


442             require(proofPublicInput.length == 1, "t4");


449             require(successVerifyProof, "p"); // Proof verification fail


482             require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch


483             require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted


543             require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu");


567             require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10");


568             require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11");


616             require(success, "failed to call point evaluation precompile");


618             require(result == BLS_MODULUS, "precompile unexpected output");


631             require(_pubdataCommitments.length > 0, "pl");


632             require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");


633             require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");


639                 require(blobVersionedHash != bytes32(0), "vh");


663             require(versionedHash == bytes32(0), "lh");


668                 require(


681             require(success, "vc");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol


183             require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol


39              require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox");


110             require(_batchNumber <= s.totalBatchesExecuted, "xx");


117             require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");


158             require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set");


185             require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");


206             require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");


243             require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp");


264             require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");


272             require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L272

```solidity
File: contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol


16              require(msg.sender == s.admin, "StateTransition Chain: not admin");


22              require(s.validators[msg.sender], "StateTransition Chain: not validator");


27              require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager");


32              require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub");


37              require(


45              require(


53              require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53

```solidity
File: contracts/zksync/contracts/bridge/L2SharedBridge.sol


55              require(_l1Bridge != address(0), "bf");


56              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");


57              require(_aliasedOwner != address(0), "sf");


58              require(_l2TokenProxyBytecodeHash != bytes32(0), "df");


68                  require(_l1LegecyBridge != address(0), "bf2");


87              require(


92              require(msg.value == 0, "Value should be 0 for ERC20 bridge");


98                  require(deployedToken == expectedL2Token, "mt");


101                 require(currentL1Token == _l1Token, "gg"); // Double check that the expected value equal to real one


124             require(_amount > 0, "Amount cannot be zero");


129             require(l1Token != address(0), "yh");


176             require(success, "mk");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L176

```solidity
File: contracts/zksync/contracts/bridge/L2StandardERC20.sol


51              require(_l1Address != address(0), "in6"); // Should be non-zero address


120             require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");


130             require(msg.sender == l2Bridge, "xnt"); // Only L2 bridge can call this method


137             require(_version == _getInitializedVersion() + 1, "v");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L137

```solidity
File: system-contracts/contracts/AccountCodeStorage.sol


26              require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");


37              require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor");


48              require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract");


57              require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57

```solidity
File: system-contracts/contracts/BootloaderUtilities.sol


92                  require(vInt == 27 || vInt == 28, "Invalid v value");


191                 require(vInt == 27 || vInt == 28, "Invalid v value");


286                 require(vInt == 27 || vInt == 28, "Invalid v value");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L286

```solidity
File: system-contracts/contracts/ComplexUpgrader.sol


22              require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER");


24              require(_delegateTo.code.length > 0, "Delegatee is an EOA");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24

```solidity
File: system-contracts/contracts/Compressor.sol


51                  require(


56                  require(


63                      require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");


68                      require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");


119             require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");


140                 require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");


156             require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");


171                 require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");


187             require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");


230                     require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch");


232                     require(


237                     require(


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L237

```solidity
File: system-contracts/contracts/ContractDeployer.sol


29              require(msg.sender == address(this), "Callable only by self");


77              require(


239             require(


251             require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");


264             require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");


265             require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");


268             require(


273             require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");


303             require(knownCodeMarker > 0, "The code hash is not known");


350                 require(value == 0, "The value must be zero if we do not call the constructor");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350

```solidity
File: system-contracts/contracts/DefaultAccount.sol


100             require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");


160             require(_signature.length == 65, "Signature length is incorrect");


173             require(v == 27 || v == 28, "v is neither 27 nor 28");


184             require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s");


202             require(success, "Failed to pay the fee to the operator");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202

```solidity
File: system-contracts/contracts/ImmutableSimulator.sol


35              require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35

```solidity
File: system-contracts/contracts/KnownCodesStorage.sol


20              require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");


76              require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");


78              require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L78

```solidity
File: system-contracts/contracts/L1Messenger.sol


201             require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");


214             require(


245             require(


269             require(


279             require(


298             require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");


315             require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315

```solidity
File: system-contracts/contracts/L2BaseToken.sol


33              require(


41              require(fromBalance >= _amount, "Transfer amount exceeds balance");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L41

```solidity
File: system-contracts/contracts/MsgValueSimulator.sol


60              require(to != address(this), "MsgValueSimulator calls itself");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60

```solidity
File: system-contracts/contracts/NonceHolder.sol


66              require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high");


85              require(_value != 0, "Nonce value cannot be set to 0");


89                  require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");


115             require(oldMinNonce == _expectedNonce, "Incorrect nonce");


136             require(


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L136

```solidity
File: system-contracts/contracts/PubdataChunkPublisher.sol


22              require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22

```solidity
File: system-contracts/contracts/SystemContext.sol


242             require(_isFirstInBatch, "Upgrade transaction must be first");


245             require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");


249                 require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");


287                 require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");


351                 require(


355                 require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");


367                 require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");


368                 require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");


369                 require(


373                 require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");


385                 require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");


386                 require(


413             require(currentBatchNumber > 0, "The current batch number must be greater than 0");


429             require(


451             require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");


452             require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");


```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452

</details>

## [G-44] Test if a number is even or odd by checking the last bit instead of using a modulo operator

**Issue Description**\
The conventional way to check if a number is even or odd is to do `x % 2 == 0` where x is the number in question. You can instead check if x & uint256(1) == 0. where x is assumed to be a uint256. Bitwise and is cheaper than the modulo op code. In binary, the rightmost bit represents "1" whereas all the bits to the are multiples of 2, which are even. Adding "1" to an even number causes it to be odd.

```solidity
file:  contracts/zksync/libraries/Merkle.sol

30            currentHash = (_index % 2 == 0)
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30
**Attachments**

- **Code Snippets**

## [G-45] Use Clones for Cheap Contract Deployments

**Issue Description**\
Use clones or metaproxies when deploying very similar smart contracts that are not called frequently
When deploying multiple similar smart contracts, the gas costs can be high. To reduce these costs, you can use minimal clones or metaproxies which store the address of the implementation contract in their bytecode and interact with it as a proxy.

However, there is a trade-off between the runtime cost and deployment cost of clones. Clones are more expensive to interact with than normal contracts due to the delegatecall they use, so they should only be used when you don’t need to interact with them frequently. For example, the Gnosis Safe contract uses clones to reduce deployment costs.

Learn more about how to use clones and metaproxies to reduce the gas costs of deploying smart contracts:

EIP-1167: Minimal Proxy Standard
EIP-3448 Metaproxy Clone

**Attachments**

- **Code Snippets**

```solidity
File: ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol

10  contract DiamondProxy {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L10

```solidity
File: interfaces/IL2ContractDeployer.sol

9   interface IL2ContractDeployer {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/interfaces/IL2ContractDeployer.sol#L10

## [G-46] Admin functions no uses of the nonReentrant modifier

**Issue Description**\
Admin functions are trusted there is no use of nonReentrant modifier to save significant amount of Gas.

**Attachments**

- **Code Snippets**

```solidity
File: ethereum/contracts/bridgehub/Bridgehub.sol

114    function createNewChain(
115        uint256 _chainId,
116        address _stateTransitionManager,
117        address _baseToken,
118        uint256, //_salt
119        address _admin,
120        bytes calldata _initData
121    ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114

```solidity
File: ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

199    function commitBatches(StoredBatchInfo memory _lastCommittedBatchData, CommitBatchInfo[] calldata _newBatchesData)
201        external
202        override
203        nonReentrant
204        onlyValidator
205    {


207    function commitBatchesSharedBridge(
208        uint256, // _chainId
209        StoredBatchInfo memory _lastCommittedBatchData,
210        CommitBatchInfo[] calldata _newBatchesData
211    ) external nonReentrant onlyValidator {


337    function executeBatchesSharedBridge(
338        uint256,
339        StoredBatchInfo[] calldata _batchesData
340    ) external nonReentrant onlyValidator {
341        _executeBatches(_batchesData);
342    }


345    function executeBatches(StoredBatchInfo[] calldata _batchesData) external nonReentrant onlyValidator {


372    ) external nonReentrant onlyValidator {

382     ) external nonReentrant onlyValidator {

472    function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {

477    function revertBatchesSharedBridge(uint256, uint256 _newLastBatch) external nonReentrant onlyValidator {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol

```solidity
File: ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol

178    function finalizeEthWithdrawal(
179        uint256 _l2BatchNumber,
180        uint256 _l2MessageIndex,
181        uint16 _l2TxNumberInBatch,
182        bytes calldata _message,
183        bytes32[] calldata _merkleProof
184    ) external nonReentrant {

228    function _requestL2TransactionSender(
229        BridgehubL2TransactionRequest memory _request
230    ) internal nonReentrant returns (bytes32 canonicalTxHash) {
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L184

## [G-47] Use Mappings instead of arrays

**Issue Description**\

Using mappings instead of arrays to avoid length checks
When storing a list or group of items that you wish to organize in a specific order and fetch with a fixed key/index, it’s common practice to use an array data structure. This works well, but did you know that a trick can be implemented to save 2,000+ gas on each read using a mapping?

**Proposed Optimization**\
See the example below

```solidity
/// get(0) gas cost: 4860
contract Array {
    uint256[] a;

    constructor() {
        a.push() = 1;
        a.push() = 2;
        a.push() = 3;
    }

    function get(uint256 index) external view returns (uint256) {
        return a[index];
    }
}

/// get(0) gas cost: 2758
contract Mapping {
    mapping(uint256 => uint256) a;

    constructor() {
        a[0] = 1;
        a[1] = 2;
        a[2] = 3;
    }

    function get(uint256 index) external view returns (uint256) {
        return a[index];
    }
}
```

Just by using a mapping, we get a gas saving of 2102 gas. Why? Under the hood when you read the value of an index of an array, solidity adds bytecode that checks that you are reading from a valid index (i.e an index strictly less than the length of the array) else it reverts with a panic error (Panic(0x32) to be precise). This prevents from reading unallocated or worse, allocated storage/memory locations.

**Estimated Gas Savings**\
Due to the way mappings are (simply a key => value pair), no check like that exists and we are able to read from the a storage slot directly. It’s important to note that when using mappings in this manner, your code should ensure that you are not reading an out of bound index of your canonical array.

**Attachments**

- **Code Snippets**

```solidity
File: ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol

30        bytes[] factoryDeps;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L30

```solidity
File: ethereum/contracts/state-transition/libraries/Diamond.sol

40        bytes4[] selectors;

53        address[] facets;

66        bytes4[] selectors;

73        FacetCut[] facetCuts;

97        FacetCut[] memory facetCuts = _diamondCut.facetCuts;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L40

## [G-48] array[index] += amount is cheaper than array[index] = array[index] + amount

```solidity
File:  ethereum/contracts/governance/Governance.sol

219        timestamps[_id] = block.timestamp + _delay;

```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L219
