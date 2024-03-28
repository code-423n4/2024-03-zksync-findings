## LightChaser-V3

### Generated for: Code4rena : ZkSync

### Generated on: 2024-03-28

## Total findings: 89

### Total Gas findings: 89

# Summary for Gas findings

| Number | Details | Instances | Gas |
|----------|----------|----------|----------|
| [Gas-1] | State variables used within a function more than once should be cached to save gas  | 2 | 1000 |
| [Gas-2] | Avoid updating storage when the value hasn't changed  | 3 | 7200 |
| [Gas-3] | State variable can be updated more than once in a function  | 1 | 800 |
| [Gas-4] | Multiple accesses of the same mapping/array key/index should be cached  | 2 | 2604 |
| [Gas-5] | bytes.concat() can be used in place of abi.encodePacked  | 1 | 0.0 |
| [Gas-6] | Shortcircuit rules can be be used to optimize some gas usage  | 2 | 29400 |
| [Gas-7] | x + y is more efficient than using += for state variables (likewise for -=) | 3 | 75 |
| [Gas-8] | There is a 32 byte length threshold for error strings, strings longer than this consume more gas | 55 | 42350 |
| [Gas-9] | Public functions not used internally can be marked as external to save gas | 8 | 0.0 |
| [Gas-10] | Calldata should be used in place of memory function parameters when not mutated | 1 | 13 |
| [Gas-11] | Usage of smaller uint/int types causes overhead | 77 | 326095 |
| [Gas-12] | Use != 0 instead of > 0 | 26 | 2028 |
| [Gas-13] | Integer increments by one can be unchecked to save on gas fees | 9 | 9720 |
| [Gas-14] | Use byte32 in place of string | 10 | 0.0 |
| [Gas-15] | Default bool values are manually reset | 3 | 0.0 |
| [Gas-16] | Default int values are manually reset | 33 | 0.0 |
| [Gas-17] | Use assembly to check for the zero address | 25 | 0.0 |
| [Gas-18] | Some error strings are not descriptive | 54 | 0.0 |
| [Gas-19] | Divisions which do not divide by -X cannot overflow or underflow so such operations can be unchecked to save gas | 4 | 0.0 |
| [Gas-20] | State variables which are not modified within functions should be set as constants or immutable for values set at deployment | 4 | 0.0 |
| [Gas-21] | Divisions of powers of 2 can be replaced by a right shift operation to save gas | 3 | 0.0 |
| [Gas-22] | multiplications of powers of 2 can be replaced by a left shift operation to save gas | 14 | 0.0 |
| [Gas-23] | Structs can be packed into fewer storage slots | 12 | 360000 |
| [Gas-24] | Expression ("") is cheaper than new bytes(0) | 3 | 2331 |
| [Gas-25] | Private functions used once can be inlined | 15 | 0.0 |
| [Gas-26] | Use bitmap to save gas | 13 | 11830 |
| [Gas-27] | Use assembly hashing | 38 | 0.0 |
| [Gas-28] | Consider using OZ EnumerateSet in place of nested mappings | 9 | 81000 |
| [Gas-29] | Using this.<fn>() wastes gas | 4 | 1600 |
| [Gas-30] | Use selfBalance() in place of address(this).balance | 4 | 12800 |
| [Gas-31] | Use assembly to emit events | 67 | 170582 |
| [Gas-32] | Shorten the array rather than copying to a new one | 8 | 0.0 |
| [Gas-33] | Use assembly in place of abi.decode to extract calldata values more efficiently | 11 | 0.0 |
| [Gas-34] | Counting down in for statements is more gas efficient | 8 | 0.0 |
| [Gas-35] | Struct variables can be packed into fewer storage slots by truncating timestamp bytes | 3 | 22500 |
| [Gas-36] | Using private rather than public for constants and immutables, saves gas | 5 | 0.0 |
| [Gas-37] | Modulus operations that could be unchecked | 3 | 765 |
| [Gas-38] | Mark Functions That Revert For Normal Users As payable | 36 | 32400 |
| [Gas-39] | Lack of unchecked in loops | 21 | 44100 |
| [Gas-40] | Consider migrating require statements to custom errors | 312 | 1362816 |
| [Gas-41] | Where a value is casted more than once, consider caching the result to save gas | 2 | 0.0 |
| [Gas-42] | Assembly let var only used on once | 4 | 0.0 |
| [Gas-43] | Assembly let var never used | 1 | 0.0 |
| [Gas-44] | Use assembly to validate msg.sender | 31 | 0.0 |
| [Gas-45] | Use += for mappings | 1 | 0.0 |
| [Gas-46] | Simple checks for zero uint can be done using assembly to save gas | 58 | 20184 |
| [Gas-47] | Use Unchecked for Divisions on Constant or Immutable Values | 3 | 0.0 |
| [Gas-48] | Using nested if to save gas | 20 | 2400 |
| [Gas-49] | Consider splitting complex if statements into multiple steps | 14 | 0.0 |
| [Gas-50] | Optimize Storage with Byte Truncation for Time Related State Variables | 1 | 2000 |
| [Gas-51] | Stack variable cost less than state variables while used in emiting event | 7 | 441 |
| [Gas-52] | Avoid emitting event on every iteration | 3 | 3375 |
| [Gas-53] | Low level call can be optimized with assembly | 7 | 12152 |
| [Gas-54] | Inline modifiers used only once | 9 | 0.0 |
| [Gas-55] | Use s.x = s.x + y instead of s.x += y for state variable structs | 1 | 0.0 |
| [Gas-56] | Use s.x = s.x + y instead of s.x += y for memory structs (same for -= etc) | 1 | 100 |
| [Gas-57] | Time state variables can be truncated to uint32 | 1 | 20000 |
| [Gas-58] | Constants are cheaper than Enums | 13 | 3380000 |
| [Gas-59] | ++X costs slightly less gas than X++ (same with --) | 7 | 245 |
| [Gas-60] | Variables that can be set to immutable | 1 | 0.0 |
| [Gas-61] | Variable declared within iteration | 9 | 0.0 |
| [Gas-62] | Calling .length in a for loop wastes gas | 11 | 11737 |
| [Gas-63] | Internal functions only used once can be inlined to save gas | 82 | 201720 |
| [Gas-64] | Constructors can be marked as payable to save deployment gas | 10 | 0.0 |
| [Gas-65] | Merge events to save gas | 3 | 3375 |
| [Gas-66] | Use assembly scratch space to build calldata for external calls | 9 | 17820 |
| [Gas-67] | Same cast is done multiple times | 8 | 0.0 |
| [Gas-68] | Assigning to structs can be more efficient | 16 | 33280 |
| [Gas-69] | An inefficient way of checking if a integer is even is being used (X % 2 == 0) | 1 | 0.0 |
| [Gas-70] | Internal functions never used once can be removed | 8 | 0.0 |
| [Gas-71] | Empty functions should be removed to save gas | 1 | 0.0 |
| [Gas-72] | There are comparisons to boolean literals (true and false), these can be simplified to save gas | 1 | 18 |
| [Gas-73] | Only emit event in setter function if the state variable was changed | 13 | 0.0 |
| [Gas-74] | It is a waste of GAS to emit variable literals | 4 | 128 |
| [Gas-75] | Short circuit before external calls | 2 | 0.0 |
| [Gas-76] | Use OZ Array.unsafeAccess() to avoid repeated array length checks | 156 | 51105600 |
| [Gas-77] | State variable written in a loop | 4 | 92704 |
| [Gas-78] | State variable read in a loop | 7 | 365022 |
| [Gas-79] | Use uint256(1)/uint256(2) instead of true/false to save gas for changes | 13 | 2873000 |
| [Gas-80] | Avoid emitting events in loops | 3 | 3375 |
| [Gas-81] | Call msg.XYZ directly rather than caching the value to save gas | 5 | 0.0 |
| [Gas-82] | Consider pre-calculating the address of address(this) to save gas | 21 | 0.0 |
| [Gas-83] | Use of memory instead of storage for struct/array state variables | 6 | 75600 |
| [Gas-84] | Mappings are cheaper than arrays for state variable iteration | 1 | 0.0 |
| [Gas-85] | Public functions not called internally | 8 | 0.0 |
| [Gas-86] | do-while is cheaper than for-loops when the initial check can be skipped | 21 | 128625 |
| [Gas-87] | Empty blocks should be removed or emit something | 4 | 0.0 |
| [Gas-88] | Use assembly to write address/contract storage values | 73 | 0.0 |
| [Gas-89] | Use constants instead of type(uint<n>).max | 18 | 0.0 |
## [Gas-1] State variables used within a function more than once should be cached to save gas 

### Resolution 
Cache such variables and perform operations on them, if operations include modifications to the state variable(s) then remember to equate the state variable to it's cached counterpart at the end

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[409](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L409-L418)']
```solidity
409:     function _finalizeWithdrawal( // <= FOUND 'function _finalizeWithdrawal'
410:         uint256 _chainId,
411:         uint256 _l2BatchNumber,
412:         uint256 _l2MessageIndex,
413:         uint16 _l2TxNumberInBatch,
414:         bytes calldata _message,
415:         bytes32[] calldata _merkleProof
416:     ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized"); // <= FOUND 'isWithdrawalFinalized'
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true; // <= FOUND 'isWithdrawalFinalized'
419: 
420:         
421:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
422:             
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");
428:         }
429: 
430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });
435:         (l1Receiver, l1Token, amount) = _checkWithdrawal(_chainId, messageParams, _message, _merkleProof);
436: 
437:         if (!hyperbridgingEnabled[_chainId]) {
438:             
439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); 
440:             chainBalance[_chainId][l1Token] -= amount;
441:         }
442: 
443:         if (l1Token == ETH_TOKEN_ADDRESS) {
444:             bool callSuccess;
445:             
446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }
449:             require(callSuccess, "ShB: withdraw failed");
450:         } else {
451:             
452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
453:         }
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
455:     }

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L32-L41)']
```solidity
32:     function acceptAdmin() external { // <= FOUND 'function acceptAdmin'
33:         address pendingAdmin = s.pendingAdmin; // <= FOUND 'pendingAdmin'
34:         require(msg.sender == pendingAdmin, "n4");  // <= FOUND 'pendingAdmin'
35: 
36:         address previousAdmin = s.admin; // <= FOUND 'admin'
37:         s.admin = pendingAdmin; // <= FOUND 'admin'
38:         delete s.pendingAdmin; // <= FOUND 'pendingAdmin'
39: 
40:         emit NewPendingAdmin(pendingAdmin, address(0)); // <= FOUND 'pendingAdmin'
41:         emit NewAdmin(previousAdmin, pendingAdmin); // <= FOUND 'pendingAdmin'
42:     }

```


</details>

## [Gas-2] Avoid updating storage when the value hasn't changed 

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L38-L61)']
```solidity
38:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal { // <= FOUND
39:         unchecked {
40:             
41:             
42:             
43:             uint256 mapIndex = _index / 8;
44:             uint256 mapValue = _map.map[mapIndex];
45: 
46:             
47:             
48:             uint256 bitOffset = (_index & 7) * 32;
49: 
50:             
51:             
52: 
53:             
54:             uint32 oldValue = uint32(mapValue >> bitOffset);
55: 
56:             
57:             uint256 newValueXorOldValue = uint256(oldValue ^ _value);
58: 
59:             
60:             
61:             _map.map[mapIndex] = (newValueXorOldValue << bitOffset) ^ mapValue; // <= FOUND
62:         }
63:     }

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55-L59)']
```solidity
55:     function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal { // <= FOUND
56:         
57:         uint256 tail = _queue.tail;
58: 
59:         _queue.data[tail] = _operation; // <= FOUND
60:         _queue.tail = tail + 1;
61:     }

```
['[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L72-L78)']
```solidity
72:     function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) { // <= FOUND
73:         require(!_queue.isEmpty(), "s"); 
74: 
75:         
76:         uint256 head = _queue.head;
77: 
78:         priorityOperation = _queue.data[head]; // <= FOUND
79:         delete _queue.data[head];
80:         _queue.head = head + 1;
81:     }

```


</details>

## [Gas-3] State variable can be updated more than once in a function 

### Resolution 
Updating a state variable multiple times within a function can lead to inefficiencies and unintended behaviors. Every state change in Ethereum consumes gas, increasing the transaction cost. Moreover, frequent state changes can introduce vulnerabilities if interim values can be externally observed or acted upon. To address this, one should consolidate updates to occur only once, at the end of the function. This minimizes gas usage and ensures consistent state. 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L263-L307)']
```solidity
263:     function _setVirtualBlock(
264:         uint128 _l2BlockNumber,
265:         uint128 _maxVirtualBlocksToCreate,
266:         uint128 _newTimestamp
267:     ) internal {
268:         if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
269:             
270:             
271:             currentVirtualL2BlockInfo = currentL2BlockInfo; // <= FOUND
272:             return;
273:         }
274: 
275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
276: 
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
278:             uint128 currentBatchNumber = currentBatchInfo.number;
279: 
280:             
281:             
282:             
283:             virtualBlockInfo.number = currentBatchNumber;
284:             
285:             virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
286: 
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
288:             _maxVirtualBlocksToCreate -= 1;
289:         } else if (_maxVirtualBlocksToCreate == 0) {
290:             
291:             
292:             return;
293:         }
294: 
295:         virtualBlockInfo.number += _maxVirtualBlocksToCreate;
296:         virtualBlockInfo.timestamp = _newTimestamp;
297: 
298:         
299:         
300:         
301:         
302:         if (virtualBlockInfo.number >= _l2BlockNumber) {
303:             virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
304:             virtualBlockInfo.number = _l2BlockNumber;
305:         }
306: 
307:         currentVirtualL2BlockInfo = virtualBlockInfo; // <= FOUND
308:     }

```


</details>

## [Gas-4] Multiple accesses of the same mapping/array key/index should be cached 

### Resolution 
Caching repeated accesses to the same mapping or array key/index in smart contracts can lead to significant gas savings. In Solidity, each read operation from storage (like accessing a value in a mapping or array using a key or index) costs gas. By storing the accessed value in a local variable and reusing it within the function, you avoid multiple expensive storage read operations. This practice is particularly beneficial in loops or functions with multiple reads of the same data. Implementing this caching approach enhances efficiency and reduces transaction costs, which is crucial for optimizing smart contract performance and user experience on the blockchain.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116-L133)']
```solidity
116:     function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
117:         if (_token == ETH_TOKEN_ADDRESS) {
118:             uint256 balanceBefore = address(this).balance;
119:             IMailbox(_target).transferEthToSharedBridge();
120:             uint256 balanceAfter = address(this).balance;
121:             require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
122:             chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] = // <= FOUND
123:                 chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] + // <= FOUND
124:                 balanceAfter -
125:                 balanceBefore;
126:         } else {
127:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
128:             uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
129:             require(amount > 0, "ShB: 0 amount to transfer");
130:             IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
131:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
132:             require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount; // <= FOUND
134:         }
135:     }

```
['[205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L205-L223)']
```solidity
205:     function _addOneFunction(address _facet, bytes4 _selector, bool _isSelectorFreezable) private {
206:         DiamondStorage storage ds = getDiamondStorage();
207: 
208:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16(); // <= FOUND
209: 
210:         
211:         
212:         
213:         if (selectorPosition != 0) {
214:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0]; // <= FOUND
215:             require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");
216:         }
217: 
218:         ds.selectorToFacet[_selector] = SelectorToFacet({ // <= FOUND
219:             facetAddress: _facet,
220:             selectorPosition: selectorPosition,
221:             isFreezable: _isSelectorFreezable
222:         });
223:         ds.facetToSelectors[_facet].selectors.push(_selector); // <= FOUND
224:     }

```


</details>

## [Gas-5] bytes.concat() can be used in place of abi.encodePacked 

### Resolution 
Given concatenation is not going to be used for hashing bytes.concat is the preferred method to use as its more gas efficient when used with bytes variables

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[610](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L610-L610)']
```solidity
610:         bytes memory precompileInput = abi.encodePacked(_versionedHash, _openingPoint, _openingValueCommitmentProof); // <= FOUND

```


</details>

## [Gas-6] Shortcircuit rules can be be used to optimize some gas usage 

### Resolution 
Reading state variables takes alot of gas to do, so if you have a conditional statement regarding a state varaible alongide others which are not related to state vars, it is advisable to have conditions which do not involve state vars be declared first in the overall conditional so unnecessary state variable lookups can be avoided.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[375](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L375-L375)']
```solidity
375:         return (_chainId == ERA_CHAIN_ID) && (_l2BatchNumber < eraFirstPostUpgradeBatch); // <= FOUND

```
['[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L88-L90)']
```solidity
88:         
89:         
90:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) { // <= FOUND

```


</details>

## [Gas-7] x + y is more efficient than using += for state variables (likewise for -=)

### Resolution 
In instances found where either += or -= are used against state variables use x = x + y instead

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L65-L65)']
```solidity
64:     function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
65:         totalSupply += _amount; // <= FOUND
66:         balance[_account] += _amount;
67:         emit Mint(_account, _amount);
68:     }

```
['[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L107-L107)']
```solidity
99:     function _burnMsgValue() internal returns (uint256 amount) {
100:         amount = msg.value;
101: 
102:         
103:         unchecked {
104:             
105:             
106:             balance[address(this)] -= amount;
107:             totalSupply -= amount; // <= FOUND
108:         }
109:     }

```
['[483](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L483-L483)']
```solidity
482:     function incrementTxNumberInBatch() external onlyCallFromBootloader {
483:         txNumberInBlock += 1; // <= FOUND
484:     }

```


</details>

## [Gas-8] There is a 32 byte length threshold for error strings, strings longer than this consume more gas

### Resolution 
In require statements found which are longer than 32 characters, shorten these to 32 character or less

Num of instances: 55

### Findings 


<details><summary>Click to show findings</summary>

['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155-L155)']
```solidity
148:     function bridgehubDepositBaseToken(
149:         uint256 _chainId,
150:         address _prevMsgSender,
151:         address _l1Token,
152:         uint256 _amount
153:     ) external payable virtual onlyBridgehubOrEra(_chainId) {
154:         if (_l1Token == ETH_TOKEN_ADDRESS) {
155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount"); // <= FOUND
156:         } else {
157:             
158:             require(msg.value == 0, "ShB m.v > 0 b d.it");
159: 
160:             uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount); 
161:             require(amount == _amount, "3T"); 
162:         }
163: 
164:         if (!hyperbridgingEnabled[_chainId]) {
165:             chainBalance[_chainId][_l1Token] += _amount;
166:         }
167:         
168:         emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);
169:     }

```
['[195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195-L195)']
```solidity
182:     function bridgehubDeposit(
183:         uint256 _chainId,
184:         address _prevMsgSender,
185:         uint256, 
186:         bytes calldata _data
187:     ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
189: 
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
191:             _data,
192:             (address, uint256, address)
193:         );
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported"); // <= FOUND
196: 
197:         uint256 amount;
198:         if (_l1Token == ETH_TOKEN_ADDRESS) {
199:             amount = msg.value;
200:             require(_depositAmount == 0, "ShB wrong withdraw amount");
201:         } else {
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
203:             amount = _depositAmount;
204: 
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); 
207:         }
208:         require(amount != 0, "6T"); 
209: 
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
211:         if (!hyperbridgingEnabled[_chainId]) {
212:             chainBalance[_chainId][_l1Token] += amount;
213:         }
214: 
215:         {
216:             
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);
218: 
219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });
226:         }
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
228:     }

```
['[427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427-L427)']
```solidity
409:     function _finalizeWithdrawal(
410:         uint256 _chainId,
411:         uint256 _l2BatchNumber,
412:         uint256 _l2MessageIndex,
413:         uint16 _l2TxNumberInBatch,
414:         bytes calldata _message,
415:         bytes32[] calldata _merkleProof
416:     ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;
419: 
420:         
421:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
422:             
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2"); // <= FOUND
428:         }
429: 
430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });
435:         (l1Receiver, l1Token, amount) = _checkWithdrawal(_chainId, messageParams, _message, _merkleProof);
436: 
437:         if (!hyperbridgingEnabled[_chainId]) {
438:             
439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); 
440:             chainBalance[_chainId][l1Token] -= amount;
441:         }
442: 
443:         if (l1Token == ETH_TOKEN_ADDRESS) {
444:             bool callSuccess;
445:             
446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }
449:             require(callSuccess, "ShB: withdraw failed");
450:         } else {
451:             
452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
453:         }
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
455:     }

```
['[564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564-L564)']
```solidity
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2"); // <= FOUND
565: 
566:         
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             
575:             
576:             
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, 
588:                 l2Value: 0, 
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

```
[]
```solidity
82:     function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {
83:         require(
84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],
85:             "Bridgehub: state transition already registered"
86:         );
87:         stateTransitionManagerIsRegistered[_stateTransitionManager] = true;
88:     }

```
[]
```solidity
92:     function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
93:         require(
94:             stateTransitionManagerIsRegistered[_stateTransitionManager],
95:             "Bridgehub: state transition not registered yet"
96:         );
97:         stateTransitionManagerIsRegistered[_stateTransitionManager] = false;
98:     }

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102-L102)']
```solidity
101:     function addToken(address _token) external onlyOwner {
102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered"); // <= FOUND
103:         tokenIsRegistered[_token] = true;
104:     }

```
[]
```solidity
114:     function createNewChain(
115:         uint256 _chainId,
116:         address _stateTransitionManager,
117:         address _baseToken,
118:         uint256, 
119:         address _admin,
120:         bytes calldata _initData
121:     ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");
123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
124: 
125:         require(
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         );
129:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
131: 
132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
133: 
134:         stateTransitionManager[_chainId] = _stateTransitionManager;
135:         baseToken[_chainId] = _baseToken;
136: 
137:         IStateTransitionManager(_stateTransitionManager).createNewChain(
138:             _chainId,
139:             _baseToken,
140:             address(sharedBridge),
141:             _admin,
142:             _initData
143:         );
144: 
145:         emit NewChain(_chainId, _stateTransitionManager, _admin);
146:         return _chainId;
147:     }

```
['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225-L225)']
```solidity
217:     function requestL2TransactionDirect(
218:         L2TransactionRequestDirect calldata _request
219:     ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
220:         {
221:             address token = baseToken[_request.chainId];
222:             if (token == ETH_TOKEN_ADDRESS) {
223:                 require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");
224:             } else {
225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value"); // <= FOUND
226:             }
227: 
228:             sharedBridge.bridgehubDepositBaseToken{value: msg.value}(
229:                 _request.chainId,
230:                 msg.sender,
231:                 token,
232:                 _request.mintValue
233:             );
234:         }
235: 
236:         address stateTransition = getStateTransition(_request.chainId);
237:         address refundRecipient = _actualRefundRecipient(_request.refundRecipient);
238:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
239:             BridgehubL2TransactionRequest({
240:                 sender: msg.sender,
241:                 contractL2: _request.l2Contract,
242:                 mintValue: _request.mintValue,
243:                 l2Value: _request.l2Value,
244:                 l2Calldata: _request.l2Calldata,
245:                 l2GasLimit: _request.l2GasLimit,
246:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
247:                 factoryDeps: _request.factoryDeps,
248:                 refundRecipient: refundRecipient
249:             })
250:         );
251:     }

```
[]
```solidity
262:     function requestL2TransactionTwoBridges(
263:         L2TransactionRequestTwoBridgesOuter calldata _request
264:     ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
265:         {
266:             address token = baseToken[_request.chainId];
267:             uint256 baseTokenMsgValue;
268:             if (token == ETH_TOKEN_ADDRESS) {
269:                 require(
270:                     msg.value == _request.mintValue + _request.secondBridgeValue,
271:                     "Bridgehub: msg.value mismatch 2"
272:                 );
273:                 baseTokenMsgValue = _request.mintValue;
274:             } else {
275:                 require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");
276:                 baseTokenMsgValue = 0;
277:             }
278:             sharedBridge.bridgehubDepositBaseToken{value: baseTokenMsgValue}(
279:                 _request.chainId,
280:                 msg.sender,
281:                 token,
282:                 _request.mintValue
283:             );
284:         }
285: 
286:         address stateTransition = getStateTransition(_request.chainId);
287: 
288:         L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)
289:             .bridgehubDeposit{value: _request.secondBridgeValue}(
290:             _request.chainId,
291:             msg.sender,
292:             _request.l2Value,
293:             _request.secondBridgeCalldata
294:         );
295: 
296:         require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");
297: 
298:         address refundRecipient = _actualRefundRecipient(_request.refundRecipient);
299: 
300:         require(
301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302:             "Bridgehub: second bridge address too low"
303:         ); 
304:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
305:             BridgehubL2TransactionRequest({
306:                 sender: _request.secondBridgeAddress,
307:                 contractL2: outputRequest.l2Contract,
308:                 mintValue: _request.mintValue,
309:                 l2Value: _request.l2Value,
310:                 l2Calldata: outputRequest.l2Calldata,
311:                 l2GasLimit: _request.l2GasLimit,
312:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
313:                 factoryDeps: outputRequest.factoryDeps,
314:                 refundRecipient: refundRecipient
315:             })
316:         );
317: 
318:         IL1SharedBridge(_request.secondBridgeAddress).bridgehubConfirmL2Transaction(
319:             _request.chainId,
320:             outputRequest.txDataHash,
321:             canonicalTxHash
322:         );
323:     }

```
['[172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L172-L172)']
```solidity
167:     function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
168:         bytes32 id = hashOperation(_operation);
169:         
170:         _checkPredecessorDone(_operation.predecessor);
171:         
172:         require(isOperationReady(id), "Operation must be ready before execution"); // <= FOUND
173:         
174:         _execute(_operation.calls);
175:         
176:         
177:         require(isOperationReady(id), "Operation must be ready after execution");
178:         
179:         timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
180:         emit OperationExecuted(id);
181:     }

```
['[191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L191-L191)']
```solidity
186:     function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
187:         bytes32 id = hashOperation(_operation);
188:         
189:         _checkPredecessorDone(_operation.predecessor);
190:         
191:         require(isOperationPending(id), "Operation must be pending before execution"); // <= FOUND
192:         
193:         _execute(_operation.calls);
194:         
195:         
196:         require(isOperationPending(id), "Operation must be pending after execution");
197:         
198:         timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
199:         emit OperationExecuted(id);
200:     }

```
['[216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L216-L216)']
```solidity
215:     function _schedule(bytes32 _id, uint256 _delay) internal {
216:         require(!isOperation(_id), "Operation with this proposal id already exists"); // <= FOUND
217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay");
218: 
219:         timestamps[_id] = block.timestamp + _delay;
220:     }

```
['[240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240-L240)']
```solidity
239:     function _checkPredecessorDone(bytes32 _predecessorId) internal view {
240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed"); // <= FOUND
241:     }

```
['[256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256-L256)']
```solidity
239:     function createNewChain(
240:         uint256 _chainId,
241:         address _baseToken,
242:         address _sharedBridge,
243:         address _admin,
244:         bytes calldata _diamondCut
245:     ) external onlyBridgehub {
246:         if (stateTransition[_chainId] != address(0)) {
247:             
248:             return;
249:         }
250: 
251:         
252:         Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));
253: 
254:         
255:         bytes32 cutHashInput = keccak256(_diamondCut);
256:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch"); // <= FOUND
257: 
258:         
259:         bytes memory initData;
260:         
261:         initData = bytes.concat(
262:             IDiamondInit.initialize.selector,
263:             bytes32(_chainId),
264:             bytes32(uint256(uint160(bridgehub))),
265:             bytes32(uint256(uint160(address(this)))),
266:             bytes32(uint256(protocolVersion)),
267:             bytes32(uint256(uint160(_admin))),
268:             bytes32(uint256(uint160(validatorTimelock))),
269:             bytes32(uint256(uint160(_baseToken))),
270:             bytes32(uint256(uint160(_sharedBridge))),
271:             bytes32(storedBatchZero),
272:             diamondCut.initCalldata
273:         );
274: 
275:         diamondCut.initCalldata = initData;
276:         
277:         DiamondProxy stateTransitionContract = new DiamondProxy{salt: bytes32(0)}(block.chainid, diamondCut);
278: 
279:         
280:         address stateTransitionAddress = address(stateTransitionContract);
281: 
282:         stateTransition[_chainId] = stateTransitionAddress;
283: 
284:         
285:         _setChainIdUpgrade(_chainId, stateTransitionAddress);
286: 
287:         emit StateTransitionNewChain(_chainId, stateTransitionAddress);
288:     }

```
['[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90-L90)']
```solidity
89:     function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis");  // <= FOUND
91:         s.feeParams.pubdataPricingMode = _validiumMode;
92:         emit ValidiumModeStatusUpdate(_validiumMode);
93:     }

```
[]
```solidity
100:     function upgradeChainFromVersion(
101:         uint256 _oldProtocolVersion,
102:         Diamond.DiamondCutData calldata _diamondCut
103:     ) external onlyAdminOrStateTransitionManager {
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
110:         require(
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         );
114:         Diamond.diamondCut(_diamondCut);
115:         emit ExecuteUpgrade(_diamondCut);
116:         require(
117:             s.protocolVersion > _oldProtocolVersion,
118:             "StateTransition: protocolVersion mismatch in STC after upgrading"
119:         );
120:     }

```
[]
```solidity
215:     function _commitBatches(
216:         StoredBatchInfo memory _lastCommittedBatchData,
217:         CommitBatchInfo[] calldata _newBatchesData
218:     ) internal {
219:         
220:         
221:         
222:         
223:         
224:         
225:         
226:         require(
227:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:             "Executor facet: wrong protocol version"
229:         );
230:         
231:         require(_newBatchesData.length == 1, "e4");
232:         
233:         require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); 
234: 
235:         bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
236:         
237:         if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
238:             _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
239:         } else {
240:             _commitBatchesWithSystemContractsUpgrade(
241:                 _lastCommittedBatchData,
242:                 _newBatchesData,
243:                 systemContractsUpgradeTxHash
244:             );
245:         }
246: 
247:         s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
248:     }

```
['[616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616-L616)']
```solidity
605:     function _pointEvaluationPrecompile(
606:         bytes32 _versionedHash,
607:         bytes32 _openingPoint,
608:         bytes calldata _openingValueCommitmentProof
609:     ) internal view {
610:         bytes memory precompileInput = abi.encodePacked(_versionedHash, _openingPoint, _openingValueCommitmentProof);
611: 
612:         (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput);
613: 
614:         
615:         
616:         require(success, "failed to call point evaluation precompile"); // <= FOUND
617:         (, uint256 result) = abi.decode(data, (uint256, uint256));
618:         require(result == BLS_MODULUS, "precompile unexpected output");
619:     }

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L39)']
```solidity
38:     function transferEthToSharedBridge() external onlyBaseTokenBridge {
39:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox"); // <= FOUND
40: 
41:         uint256 amount = address(this).balance;
42:         address sharedBridgeAddress = s.baseTokenBridge;
43:         IL1SharedBridge(sharedBridgeAddress).receiveEth{value: amount}(ERA_CHAIN_ID);
44:     }

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L158)']
```solidity
156:     function _deriveL2GasPrice(uint256 _l1GasPrice, uint256 _gasPerPubdata) internal view returns (uint256) {
157:         FeeParams memory feeParams = s.feeParams;
158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set"); // <= FOUND
159:         uint256 l1GasPriceConverted = (_l1GasPrice * s.baseTokenGasPriceMultiplierNominator) /
160:             s.baseTokenGasPriceMultiplierDenominator;
161:         uint256 pubdataPriceBaseToken;
162:         if (feeParams.pubdataPricingMode == PubdataPricingMode.Rollup) {
163:             pubdataPriceBaseToken = L1_GAS_PER_PUBDATA_BYTE * l1GasPriceConverted;
164:         }
165: 
166:         uint256 batchOverheadBaseToken = uint256(feeParams.batchOverheadL1Gas) * l1GasPriceConverted;
167:         uint256 fullPubdataPriceBaseToken = pubdataPriceBaseToken +
168:             batchOverheadBaseToken /
169:             uint256(feeParams.maxPubdataPerBatch);
170: 
171:         uint256 l2GasPrice = feeParams.minimalL2GasPrice + batchOverheadBaseToken / uint256(feeParams.maxL2GasPerBatch);
172:         uint256 minL2GasPriceBaseToken = (fullPubdataPriceBaseToken + _gasPerPubdata - 1) / _gasPerPubdata;
173: 
174:         return Math.max(l2GasPrice, minL2GasPriceBaseToken);
175:     }

```
['[185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185-L185)']
```solidity
178:     function finalizeEthWithdrawal(
179:         uint256 _l2BatchNumber,
180:         uint256 _l2MessageIndex,
181:         uint16 _l2TxNumberInBatch,
182:         bytes calldata _message,
183:         bytes32[] calldata _merkleProof
184:     ) external nonReentrant {
185:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox"); // <= FOUND
186:         IL1SharedBridge(s.baseTokenBridge).finalizeWithdrawal(
187:             ERA_CHAIN_ID,
188:             _l2BatchNumber,
189:             _l2MessageIndex,
190:             _l2TxNumberInBatch,
191:             _message,
192:             _merkleProof
193:         );
194:     }

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206-L206)']
```solidity
197:     function requestL2Transaction(
198:         address _contractL2,
199:         uint256 _l2Value,
200:         bytes calldata _calldata,
201:         uint256 _l2GasLimit,
202:         uint256 _l2GasPerPubdataByteLimit,
203:         bytes[] calldata _factoryDeps,
204:         address _refundRecipient
205:     ) external payable returns (bytes32 canonicalTxHash) {
206:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token"); // <= FOUND
207:         canonicalTxHash = _requestL2TransactionSender(
208:             BridgehubL2TransactionRequest({
209:                 sender: msg.sender,
210:                 contractL2: _contractL2,
211:                 mintValue: msg.value,
212:                 l2Value: _l2Value,
213:                 l2GasLimit: _l2GasLimit,
214:                 l2Calldata: _calldata,
215:                 l2GasPerPubdataByteLimit: _l2GasPerPubdataByteLimit,
216:                 factoryDeps: _factoryDeps,
217:                 refundRecipient: _refundRecipient
218:             })
219:         );
220:         IL1SharedBridge(s.baseTokenBridge).bridgehubDepositBaseToken{value: msg.value}(
221:             s.chainId,
222:             msg.sender,
223:             ETH_TOKEN_ADDRESS,
224:             msg.value
225:         );
226:     }

```
['[190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190-L190)']
```solidity
180:     function _setL2SystemContractUpgrade(
181:         L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
182:         bytes[] calldata _factoryDeps,
183:         uint256 _newProtocolVersion
184:     ) internal returns (bytes32) {
185:         
186:         if (_l2ProtocolUpgradeTx.txType == 0) {
187:             return bytes32(0);
188:         }
189: 
190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong"); // <= FOUND
191: 
192:         bytes memory encodedTransaction = abi.encode(_l2ProtocolUpgradeTx);
193: 
194:         TransactionValidator.validateL1ToL2Transaction(
195:             _l2ProtocolUpgradeTx,
196:             encodedTransaction,
197:             s.priorityTxMaxGasLimit,
198:             s.feeParams.priorityTxMaxPubdata
199:         );
200: 
201:         TransactionValidator.validateUpgradeTransaction(_l2ProtocolUpgradeTx);
202: 
203:         
204:         
205:         require(
206:             _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
207:             "The new protocol version should be included in the L2 system upgrade tx"
208:         );
209: 
210:         _verifyFactoryDeps(_factoryDeps, _l2ProtocolUpgradeTx.factoryDeps);
211: 
212:         bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction);
213: 
214:         s.l2SystemContractsUpgradeTxHash = l2ProtocolUpgradeTxHash;
215: 
216:         return l2ProtocolUpgradeTxHash;
217:     }

```
[]
```solidity
236:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal virtual {
237:         uint256 previousProtocolVersion = s.protocolVersion;
238:         require(
239:             _newProtocolVersion > previousProtocolVersion,
240:             "New protocol version is not greater than the current one"
241:         );
242:         require(
243:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
244:             "Too big protocol version difference"
245:         );
246: 
247:         
248:         
249:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
250:         require(
251:             s.l2SystemContractsUpgradeBatchNumber == 0,
252:             "The batch number of the previous upgrade has not been cleaned"
253:         );
254: 
255:         s.protocolVersion = _newProtocolVersion;
256:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
257:     }

```
[]
```solidity
20:     function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
21:         uint256 previousProtocolVersion = s.protocolVersion;
22:         require(
23:             
24:             _newProtocolVersion >= previousProtocolVersion,
25:             "New protocol version is not greater than the current one"
26:         );
27:         require(
28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:             "Too big protocol version difference"
30:         );
31: 
32:         
33:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
34:         require(
35:             s.l2SystemContractsUpgradeBatchNumber == 0,
36:             "The batch number of the previous upgrade has not been cleaned"
37:         );
38: 
39:         s.protocolVersion = _newProtocolVersion;
40:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
41:     }

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35-L35)']
```solidity
34:     function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract"); // <= FOUND
36:         unchecked {
37:             uint256 immutablesLength = _immutables.length;
38:             for (uint256 i = 0; i < immutablesLength; ++i) {
39:                 uint256 index = _immutables[i].index;
40:                 bytes32 value = _immutables[i].value;
41:                 immutableDataStorage[uint256(uint160(_dest))][index] = value;
42:             }
43:         }
44:     }

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L37-L37)']
```solidity
35:     function storeAccountConstructingCodeHash(address _address, bytes32 _hash) external override onlyDeployer {
36:         
37:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor"); // <= FOUND
38:         _storeCodeHash(_address, _hash);
39:     }

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L48-L48)']
```solidity
46:     function storeAccountConstructedCodeHash(address _address, bytes32 _hash) external override onlyDeployer {
47:         
48:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract"); // <= FOUND
49:         _storeCodeHash(_address, _hash);
50:     }

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57-L57)']
```solidity
54:     function markAccountCodeHashAsConstructed(address _address) external override onlyDeployer {
55:         bytes32 codeHash = getRawCodeHash(_address);
56: 
57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor"); // <= FOUND
58: 
59:         
60:         bytes32 constructedBytecodeHash = Utils.constructedBytecodeHash(codeHash);
61: 
62:         _storeCodeHash(_address, constructedBytecodeHash);
63:     }

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22-L22)']
```solidity
21:     function upgrade(address _delegateTo, bytes calldata _calldata) external payable {
22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER"); // <= FOUND
23: 
24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA");
25:         (bool success, bytes memory returnData) = _delegateTo.delegatecall(_calldata);
26:         assembly {
27:             if iszero(success) {
28:                 revert(add(returnData, 0x20), mload(returnData))
29:             }
30:         }
31:     }

```
[]
```solidity
44:     function publishCompressedBytecode(
45:         bytes calldata _bytecode,
46:         bytes calldata _rawCompressedData
47:     ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
48:         unchecked {
49:             (bytes calldata dictionary, bytes calldata encodedData) = _decodeRawBytecode(_rawCompressedData);
50: 
51:             require(
52:                 encodedData.length * 4 == _bytecode.length,
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             );
55: 
56:             require(
57:                 dictionary.length / 8 <= encodedData.length / 2,
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             );
60: 
61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
64: 
65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
67: 
68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
69:             }
70:         }
71: 
72:         bytecodeHash = Utils.hashL2Bytecode(_bytecode);
73:         L1_MESSENGER_CONTRACT.sendToL1(_rawCompressedData);
74:         KNOWN_CODE_STORAGE_CONTRACT.markBytecodeAsPublished(bytecodeHash);
75:     }

```
['[119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L119-L119)']
```solidity
110:     function verifyCompressedStateDiffs(
111:         uint256 _numberOfStateDiffs,
112:         uint256 _enumerationIndexSize,
113:         bytes calldata _stateDiffs,
114:         bytes calldata _compressedStateDiffs
115:     ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
116:         
117:         
118:         
119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large"); // <= FOUND
120: 
121:         uint256 numberOfInitialWrites = uint256(_compressedStateDiffs.readUint16(0));
122: 
123:         uint256 stateDiffPtr = 2;
124:         uint256 numInitialWritesProcessed = 0;
125: 
126:         
127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84);
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++;
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92);
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144:             stateDiffPtr++;
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }
155: 
156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
157: 
158:         
159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
160:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
161:             uint64 enumIndex = stateDiff.readUint64(84);
162:             if (enumIndex == 0) {
163:                 continue;
164:             }
165: 
166:             uint256 initValue = stateDiff.readUint256(92);
167:             uint256 finalValue = stateDiff.readUint256(124);
168:             uint256 compressedEnumIndex = _sliceToUint256(

```
['[230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230-L230)']
```solidity
220:     function _verifyValueCompression(
221:         uint256 _initialValue,
222:         uint256 _finalValue,
223:         uint256 _operation,
224:         bytes calldata _compressedValue
225:     ) internal pure {
226:         uint256 convertedValue = _sliceToUint256(_compressedValue);
227: 
228:         unchecked {
229:             if (_operation == 0 || _operation == 3) {
230:                 require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch"); // <= FOUND
231:             } else if (_operation == 1) {
232:                 require(
233:                     _initialValue + convertedValue == _finalValue,
234:                     "add: initial plus converted not equal to final"
235:                 );
236:             } else if (_operation == 2) {
237:                 require(
238:                     _initialValue - convertedValue == _finalValue,
239:                     "sub: initial minus converted not equal to final"
240:                 );
241:             } else {
242:                 revert("unsupported operation");
243:             }
244:         }
245:     }

```
[]
```solidity
74:     function updateNonceOrdering(AccountNonceOrdering _nonceOrdering) external onlySystemCall {
75:         AccountInfo memory currentInfo = accountInfo[msg.sender];
76: 
77:         require(
78:             _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79:                 currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80:             "It is only possible to change from sequential to arbitrary ordering"
81:         );
82: 
83:         currentInfo.nonceOrdering = _nonceOrdering;
84:         _storeAccountInfo(msg.sender, currentInfo);
85: 
86:         emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering);
87:     }

```
[]
```solidity
238:     function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
239:         require(
240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241:             "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:         );
243: 
244:         uint256 deploymentsLength = _deployments.length;
245:         
246:         
247:         uint256 sumOfValues = 0;
248:         for (uint256 i = 0; i < deploymentsLength; ++i) {
249:             sumOfValues += _deployments[i].value;
250:         }
251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
252: 
253:         for (uint256 i = 0; i < deploymentsLength; ++i) {
254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
255:         }
256:     }

```
['[265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L265-L265)']
```solidity
258:     function _nonSystemDeployOnAddress(
259:         bytes32 _bytecodeHash,
260:         address _newAddress,
261:         AccountAbstractionVersion _aaVersion,
262:         bytes calldata _input
263:     ) internal {
264:         require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");
265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space"); // <= FOUND
266: 
267:         
268:         require(
269:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
270:             "Code hash is non-zero"
271:         );
272:         
273:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");
274: 
275:         _performDeployOnAddress(_bytecodeHash, _newAddress, _aaVersion, _input);
276:     }

```
['[350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350-L350)']
```solidity
321:     function _constructContract(
322:         address _sender,
323:         address _newAddress,
324:         bytes32 _bytecodeHash,
325:         bytes calldata _input,
326:         bool _isSystem,
327:         bool _callConstructor
328:     ) internal {
329:         uint256 value = msg.value;
330:         if (_callConstructor) {
331:             
332:             if (value > 0) {
333:                 BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
334:             }
335:             
336:             _storeConstructingByteCodeHashOnAddress(_newAddress, _bytecodeHash);
337: 
338:             
339:             if (value > 0) {
340:                 
341:                 SystemContractHelper.setValueForNextFarCall(uint128(value));
342:             }
343:             bytes memory returnData = EfficientCall.mimicCall(gasleft(), _newAddress, _input, _sender, true, _isSystem);
344:             
345:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.markAccountCodeHashAsConstructed(_newAddress);
346:             
347:             ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[]));
348:             IMMUTABLE_SIMULATOR_SYSTEM_CONTRACT.setImmutables(_newAddress, immutables);
349:         } else {
350:             require(value == 0, "The value must be zero if we do not call the constructor"); // <= FOUND
351:             
352:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructedCodeHash(_newAddress, _bytecodeHash);
353:         }
354: 
355:         emit ContractDeployed(_sender, _bytecodeHash, _newAddress);
356:     }

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100-L100)']
```solidity
78:     function _validateTransaction(
79:         bytes32 _suggestedSignedHash,
80:         Transaction calldata _transaction
81:     ) internal returns (bytes4 magic) {
82:         
83:         SystemContractsCaller.systemCallWithPropagatedRevert(
84:             uint32(gasleft()),
85:             address(NONCE_HOLDER_SYSTEM_CONTRACT),
86:             0,
87:             abi.encodeCall(INonceHolder.incrementMinNonceIfEquals, (_transaction.nonce))
88:         );
89: 
90:         
91:         
92:         
93:         
94:         bytes32 txHash = _suggestedSignedHash != bytes32(0) ? _suggestedSignedHash : _transaction.encodeHash();
95: 
96:         
97:         
98:         
99:         uint256 totalRequiredBalance = _transaction.totalRequiredBalance();
100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value"); // <= FOUND
101: 
102:         if (_isValidSignature(txHash, _transaction.signature)) {
103:             magic = ACCOUNT_VALIDATION_SUCCESS_MAGIC;
104:         }
105:     }

```
['[202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202-L202)']
```solidity
196:     function payForTransaction(
197:         bytes32, 
198:         bytes32, 
199:         Transaction calldata _transaction
200:     ) external payable ignoreNonBootloader ignoreInDelegateCall {
201:         bool success = _transaction.payToTheBootloader();
202:         require(success, "Failed to pay the fee to the operator"); // <= FOUND
203:     }

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76-L76)']
```solidity
74:     function _validateBytecode(bytes32 _bytecodeHash) internal pure {
75:         uint8 version = uint8(_bytecodeHash[0]);
76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash"); // <= FOUND
77: 
78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");
79:     }

```
[]
```solidity
194:     function publishPubdataAndClearState(
195:         bytes calldata _totalL2ToL1PubdataAndStateDiffs
196:     ) external onlyCallFromBootloader {
197:         uint256 calldataPtr = 0;
198: 
199:         
200:         uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
201:         require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");
202:         calldataPtr += 4;
203: 
204:         bytes32[] memory l2ToL1LogsTreeArray = new bytes32[](L2_TO_L1_LOGS_MERKLE_TREE_LEAVES);
205:         bytes32 reconstructedChainedLogsHash;
206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }
214:         require(
215:             reconstructedChainedLogsHash == chainedLogsHash,
216:             "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217:         );
218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;
220:         }
221:         uint256 nodesOnCurrentLevel = L2_TO_L1_LOGS_MERKLE_TREE_LEAVES;
222:         while (nodesOnCurrentLevel > 1) {
223:             nodesOnCurrentLevel /= 2;
224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
225:                 l2ToL1LogsTreeArray[i] = keccak256(
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );
228:             }
229:         }
230:         bytes32 l2ToL1LogsTreeRoot = l2ToL1LogsTreeArray[0];
231: 
232:         
233:         uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
234:         calldataPtr += 4;
235:         bytes32 reconstructedChainedMessagesHash;
236:         for (uint256 i = 0; i < numberOfMessages; ++i) {
237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
238:             calldataPtr += 4;
239:             bytes32 hashedMessage = EfficientCall.keccak(
240:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
241:             );
242:             calldataPtr += currentMessageLength;
243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));
244:         }
245:         require(
246:             reconstructedChainedMessagesHash == chainedMessagesHash,
247:             "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248:         );
249: 
250:         
251:         uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
252:         calldataPtr += 4;
253:         bytes32 reconstructedChainedL1BytecodesRevealDataHash;
254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {
255:             uint32 currentBytecodeLength = uint32(
256:                 bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
257:             );
258:             calldataPtr += 4;
259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260:                 abi.encode(
261:                     reconstructedChainedL1BytecodesRevealDataHash,
262:                     Utils.hashL2Bytecode(
263:                         _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264:                     )
265:                 )
266:             );
267:             calldataPtr += currentBytecodeLength;
268:         }
269:         require(
270:             reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271:             "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272:         );
273: 
274:         
275:         
276:         
277:         
278:         
279:         require(
280:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281:                 STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282:             "state diff compression version mismatch"
283:         );
284:         calldataPtr++;
285: 
286:         uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));
287:         calldataPtr += 3;
288: 
289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
290:         calldataPtr++;
291: 
292:         bytes calldata compressedStateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
293:             compressedStateDiffSize];
294:         calldataPtr += compressedStateDiffSize;
295: 
296:         bytes calldata totalL2ToL1Pubdata = _totalL2ToL1PubdataAndStateDiffs[:calldataPtr];
297: 
298:         require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");
299: 
300:         uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
301:         calldataPtr += 4;
302: 
303:         bytes calldata stateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
304:             (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];
305:         calldataPtr += numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE;
306: 
307:         bytes32 stateDiffHash = COMPRESSOR_CONTRACT.verifyCompressedStateDiffs(
308:             numberOfStateDiffs,
309:             enumerationIndexSize,
310:             stateDiffs,
311:             compressedStateDiffs
312:         );
313: 
314:         
315:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
316: 
317:         PUBDATA_CHUNK_PUBLISHER.chunkAndPublishPubdata(totalL2ToL1Pubdata);
318: 
319:         
320:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)), l2ToL1LogsTreeRoot);
321:         SystemContractHelper.toL1(
322:             true,
323:             bytes32(uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)),
324:             EfficientCall.keccak(totalL2ToL1Pubdata)
325:         );
326:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.STATE_DIFF_HASH_KEY)), stateDiffHash);
327: 
328:         
329:         chainedLogsHash = bytes32(0);
330:         numberOfLogsToProcess = 0;
331:         chainedMessagesHash = bytes32(0);
332:         chainedL1BytecodesRevealDataHash = bytes32(0);
333:     }

```
[]
```solidity
32:     function transferFromTo(address _from, address _to, uint256 _amount) external override {
33:         require(
34:             msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35:                 msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37:             "Only system contracts with special access can call this method"
38:         );
39: 
40:         uint256 fromBalance = balance[_from];
41:         require(fromBalance >= _amount, "Transfer amount exceeds balance");
42:         unchecked {
43:             balance[_from] = fromBalance - _amount;
44:             
45:             
46:             balance[_to] += _amount;
47:         }
48: 
49:         emit Transfer(_from, _to, _amount);
50:     }

```
['[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66-L66)']
```solidity
65:     function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) {
66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high"); // <= FOUND
67: 
68:         uint256 addressAsKey = uint256(uint160(msg.sender));
69:         uint256 oldRawNonce = rawNonces[addressAsKey];
70: 
71:         unchecked {
72:             rawNonces[addressAsKey] = (oldRawNonce + _value);
73:         }
74: 
75:         (, oldMinNonce) = _splitRawNonce(oldRawNonce);
76:     }

```
['[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L89-L89)']
```solidity
82:     function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
83:         IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);
84: 
85:         require(_value != 0, "Nonce value cannot be set to 0");
86:         
87:         
88:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
89:             require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used"); // <= FOUND
90:         }
91: 
92:         uint256 addressAsKey = uint256(uint160(msg.sender));
93: 
94:         nonceValues[addressAsKey][_key] = _value;
95: 
96:         emit ValueSetUnderNonce(msg.sender, _key, _value);
97:     }

```
[]
```solidity
135:     function incrementDeploymentNonce(address _address) external returns (uint256 prevDeploymentNonce) {
136:         require(
137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138:             "Only the contract deployer can increment the deployment nonce"
139:         );
140:         uint256 addressAsKey = uint256(uint160(_address));
141:         uint256 oldRawNonce = rawNonces[addressAsKey];
142: 
143:         unchecked {
144:             rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER);
145:         }
146: 
147:         (prevDeploymentNonce, ) = _splitRawNonce(oldRawNonce);
148:     }

```
['[242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L242-L242)']
```solidity
241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal {
242:         require(_isFirstInBatch, "Upgrade transaction must be first"); // <= FOUND
243: 
244:         
245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");
246: 
247:         unchecked {
248:             bytes32 correctPrevBlockHash = _calculateLegacyL2BlockHash(_l2BlockNumber - 1);
249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");
250: 
251:             
252:             
253:             
254:             
255:             _setL2BlockHash(_l2BlockNumber - 1, correctPrevBlockHash);
256:         }
257:     }

```
['[287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287-L287)']
```solidity
263:     function _setVirtualBlock(
264:         uint128 _l2BlockNumber,
265:         uint128 _maxVirtualBlocksToCreate,
266:         uint128 _newTimestamp
267:     ) internal {
268:         if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
269:             
270:             
271:             currentVirtualL2BlockInfo = currentL2BlockInfo;
272:             return;
273:         }
274: 
275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
276: 
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
278:             uint128 currentBatchNumber = currentBatchInfo.number;
279: 
280:             
281:             
282:             
283:             virtualBlockInfo.number = currentBatchNumber;
284:             
285:             virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
286: 
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block"); // <= FOUND
288:             _maxVirtualBlocksToCreate -= 1;
289:         } else if (_maxVirtualBlocksToCreate == 0) {
290:             
291:             
292:             return;
293:         }
294: 
295:         virtualBlockInfo.number += _maxVirtualBlocksToCreate;
296:         virtualBlockInfo.timestamp = _newTimestamp;
297: 
298:         
299:         
300:         
301:         
302:         if (virtualBlockInfo.number >= _l2BlockNumber) {
303:             virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
304:             virtualBlockInfo.number = _l2BlockNumber;
305:         }
306: 
307:         currentVirtualL2BlockInfo = virtualBlockInfo;
308:     }

```
[]
```solidity
341:     function setL2Block(
342:         uint128 _l2BlockNumber,
343:         uint128 _l2BlockTimestamp,
344:         bytes32 _expectedPrevL2BlockHash,
345:         bool _isFirstInBatch,
346:         uint128 _maxVirtualBlocksToCreate
347:     ) external onlyCallFromBootloader {
348:         
349:         if (_isFirstInBatch) {
350:             uint128 currentBatchTimestamp = currentBatchInfo.timestamp;
351:             require(
352:                 _l2BlockTimestamp >= currentBatchTimestamp,
353:                 "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354:             );
355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
356:         }
357: 
358:         (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();
359: 
360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
361:             
362:             
363:             _upgradeL2Blocks(_l2BlockNumber, _expectedPrevL2BlockHash, _isFirstInBatch);
364: 
365:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
366:         } else if (currentL2BlockNumber == _l2BlockNumber) {
367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");
368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");
369:             require(
370:                 _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371:                 "The previous hash of the same L2 block must be same"
372:             );
373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
374:         } else if (currentL2BlockNumber + 1 == _l2BlockNumber) {
375:             
376:             bytes32 prevL2BlockHash = _getLatest257L2blockHash(currentL2BlockNumber - 1);
377: 
378:             bytes32 pendingL2BlockHash = _calculateL2BlockHash(
379:                 currentL2BlockNumber,
380:                 currentL2BlockTimestamp,
381:                 prevL2BlockHash,
382:                 currentL2BlockTxsRollingHash
383:             );
384: 
385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");
386:             require(
387:                 _l2BlockTimestamp > currentL2BlockTimestamp,
388:                 "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389:             );
390: 
391:             
392:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
393:         } else {
394:             revert("Invalid new L2 block number");
395:         }
396: 
397:         _setVirtualBlock(_l2BlockNumber, _maxVirtualBlocksToCreate, _l2BlockTimestamp);
398:     }

```
['[413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413-L413)']
```solidity
408:     function publishTimestampDataToL1() external onlyCallFromBootloader {
409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp();
410:         (, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp();
411: 
412:         
413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0"); // <= FOUND
414: 
415:         
416:         uint256 packedTimestamps = (uint256(currentBatchTimestamp) << 128) | currentL2BlockTimestamp;
417: 
418:         SystemContractHelper.toL1(
419:             false,
420:             bytes32(uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)),
421:             bytes32(packedTimestamps)
422:         );
423:     }

```
[]
```solidity
427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
428:         uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;
429:         require(
430:             _newTimestamp > currentBlockTimestamp,
431:             "The timestamp of the batch must be greater than the timestamp of the previous block"
432:         );
433:     }

```
['[451](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L451-L451)']
```solidity
444:     function setNewBatch(
445:         bytes32 _prevBatchHash,
446:         uint128 _newTimestamp,
447:         uint128 _expectedNewNumber,
448:         uint256 _baseFee
449:     ) external onlyCallFromBootloader {
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();
451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental"); // <= FOUND
452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453: 
454:         _ensureBatchConsistentWithL2Block(_newTimestamp);
455: 
456:         batchHashes[previousBatchNumber] = _prevBatchHash;
457: 
458:         
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
460: 
461:         currentBatchInfo = newBlockInfo;
462: 
463:         baseFee = _baseFee;
464: 
465:         
466:         SystemContractHelper.toL1(false, bytes32(uint256(SystemLogKey.PREV_BATCH_HASH_KEY)), _prevBatchHash);
467:     }

```
['[319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319-L319)']
```solidity
318:     function getExtraAbiData(uint256 index) internal view returns (uint256 extraAbiData) {
319:         require(index < 10, "There are only 10 accessible registers"); // <= FOUND
320: 
321:         address callAddr = GET_EXTRA_ABI_DATA_ADDRESS;
322:         assembly {
323:             extraAbiData := staticcall(index, callAddr, 0, 0xFFFF, 0, 0)
324:         }
325:     }

```
['[363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363-L363)']
```solidity
362:     function processPaymasterInput(Transaction calldata _transaction) internal {
363:         require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long"); // <= FOUND
364: 
365:         bytes4 paymasterInputSelector = bytes4(_transaction.paymasterInput[0:4]);
366:         if (paymasterInputSelector == IPaymasterFlow.approvalBased.selector) {
367:             require(
368:                 _transaction.paymasterInput.length >= 68,
369:                 "The approvalBased paymaster input must be at least 68 bytes long"
370:             );
371: 
372:             
373:             
374:             (address token, uint256 minAllowance) = abi.decode(_transaction.paymasterInput[4:68], (address, uint256));
375:             address paymaster = address(uint160(_transaction.paymaster));
376: 
377:             uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster);
378:             if (currentAllowance < minAllowance) {
379:                 
380:                 
381: 
382:                 IERC20(token).safeApprove(paymaster, 0);
383:                 IERC20(token).safeApprove(paymaster, minAllowance);
384:             }
385:         } else if (paymasterInputSelector == IPaymasterFlow.general.selector) {
386:             
387:         } else {
388:             revert("Unsupported paymaster flow");
389:         }
390:     }

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92-L92)']
```solidity
79:     function finalizeDeposit(
80:         address _l1Sender,
81:         address _l2Receiver,
82:         address _l1Token,
83:         uint256 _amount,
84:         bytes calldata _data
85:     ) external payable override {
86:         
87:         require(
88:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90:             "mq"
91:         );
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge"); // <= FOUND
93: 
94:         address expectedL2Token = l2TokenAddress(_l1Token);
95:         address currentL1Token = l1TokenAddress[expectedL2Token];
96:         if (currentL1Token == address(0)) {
97:             address deployedToken = _deployL2Token(_l1Token, _data);
98:             require(deployedToken == expectedL2Token, "mt");
99:             l1TokenAddress[expectedL2Token] = _l1Token;
100:         } else {
101:             require(currentL1Token == _l1Token, "gg"); 
102:         }
103: 
104:         IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);
105:         emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);
106:     }

```


</details>

## [Gas-9] Public functions not used internally can be marked as external to save gas

### Resolution 
Public functions that aren't used internally in Solidity contracts should be made external to optimize gas usage and improve contract efficiency. External functions can only be called from outside the contract, and their arguments are directly read from the calldata, which is more gas-efficient than loading them into memory, as is the case for public functions. By using external visibility, developers can reduce gas consumption for external calls and ensure that the contract operates more cost-effectively for users. Moreover, setting the appropriate visibility level for functions also enhances code readability and maintainability, promoting a more secure and well-structured contract design.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L40-L40)']
```solidity
40:     function extendedAccountVersion(address _address) public view returns (AccountAbstractionVersion) 

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L65-L65)']
```solidity
65:     function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) 

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L82-L82)']
```solidity
82:     function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall 

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L102-L102)']
```solidity
102:     function getValueUnderNonce(uint256 _key) public view returns (uint256) 

```
['[190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L190-L190)']
```solidity
190:     function getBlockNumber() public view returns (uint128) 

```
['[198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L198-L198)']
```solidity
198:     function getBlockTimestamp() public view returns (uint128) 

```
['[140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L140-L140)']
```solidity
140:     function decimals() external pure override returns (uint8) 

```
['[171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L171-L171)']
```solidity
171:     function decimals() public view override returns (uint8) 

```


</details>

## [Gas-10] Calldata should be used in place of memory function parameters when not mutated

### Resolution 
In Solidity, `calldata` should be used in place of `memory` for function parameters when the function is `external`. This is because `calldata` is a non-modifiable, non-persistent area where function arguments are stored, and it's cheaper in terms of gas than `memory`. It's especially efficient for arrays and complex data types. `calldata` provides a gas-efficient way to pass data in external function calls, whereas `memory` is a temporary space that's erased between external function calls. This distinction is crucial for optimizing smart contracts for gas usage and performance.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L50-L58)']
```solidity
50:     function bridgeInitialize(address _l1Address, bytes memory _data) external initializer { // <= FOUND
51:         require(_l1Address != address(0), "in6"); 
52:         l1Address = _l1Address;
53: 
54:         l2Bridge = msg.sender;
55: 
56:         
57:         (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(
58:             _data, // <= FOUND
59:             (bytes, bytes, bytes)
60:         );
61: 
62:         ERC20Getters memory getters;
63:         string memory decodedName;
64:         string memory decodedSymbol;
65: 
66:         
67:         
68: 
69:         
70:         
71:         
72:         
73:         
74: 
75:         try this.decodeString(nameBytes) returns (string memory nameString) {
76:             decodedName = nameString;
77:         } catch {
78:             getters.ignoreName = true;
79:         }
80: 
81:         try this.decodeString(symbolBytes) returns (string memory symbolString) {
82:             decodedSymbol = symbolString;
83:         } catch {
84:             getters.ignoreSymbol = true;
85:         }
86: 
87:         
88:         __ERC20_init_unchained(decodedName, decodedSymbol);
89: 
90:         
91:         __ERC20Permit_init(decodedName);
92: 
93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
94:             
95:             decimals_ = decimalsUint8;
96:         } catch {
97:             getters.ignoreDecimals = true;
98:         }
99: 
100:         availableGetters = getters;
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);
102:     }

```


</details>

## [Gas-11] Usage of smaller uint/int types causes overhead

### Resolution 
When using a smaller int/uint type it first needs to be converted to it's 258 bit counterpart to be operated, this increases the gass cost and thus should be avoided. However it does make sense to use smaller int/uint values within structs provided you pack the struct properly.

Num of instances: 77

### Findings 


<details><summary>Click to show findings</summary>

['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39-L39)']
```solidity
32:     function _commitOneBatch(
33:         StoredBatchInfo memory _previousBatch,
34:         CommitBatchInfo calldata _newBatch,
35:         bytes32 _expectedSystemContractUpgradeTxHash
36:     ) internal view returns (StoredBatchInfo memory) {
37:         require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); 
38: 
39:         uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0])); // <= FOUND
40:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");
41: 
42:         
43:         
44:         LogProcessingOutput memory logOutput = _processL2Logs(_newBatch, _expectedSystemContractUpgradeTxHash);
45: 
46:         bytes32[] memory blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);
47:         bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);
48:         if (s.feeParams.pubdataPricingMode == PubdataPricingMode.Validium) {
49:             
50:             require(logOutput.pubdataHash == 0x00, "v0h");
51:             require(_newBatch.pubdataCommitments.length == 1);
52:         } else if (pubdataSource == uint8(PubdataSource.Blob)) {
53:             
54:             
55:             blobHashes[0] = logOutput.blob1Hash;
56:             blobHashes[1] = logOutput.blob2Hash;
57:             
58:             blobCommitments = _verifyBlobInformation(_newBatch.pubdataCommitments[1:], blobHashes);
59:         } else if (pubdataSource == uint8(PubdataSource.Calldata)) {
60:             
61:             require(
62:                 logOutput.pubdataHash ==
63:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
64:                 "wp"
65:             );
66:             blobHashes[0] = logOutput.blob1Hash;
67:             blobCommitments[0] = bytes32(
68:                 _newBatch.pubdataCommitments[_newBatch.pubdataCommitments.length - 32:_newBatch
69:                     .pubdataCommitments
70:                     .length]
71:             );
72:         }
73: 
74:         require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");
75:         
76:         require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");
77:         
78:         require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");
79: 
80:         
81:         _verifyBatchTimestamp(logOutput.packedBatchAndL2BlockTimestamp, _newBatch.timestamp, _previousBatch.timestamp);
82: 
83:         
84:         bytes32 commitment = _createBatchCommitment(_newBatch, logOutput.stateDiffHash, blobCommitments, blobHashes);
85: 
86:         return
87:             StoredBatchInfo(
88:                 _newBatch.batchNumber,

```
['[592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592-L592)']
```solidity
592:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool) { // <= FOUND
593:         return (_bitMap & (1 << _index)) > 0;
594:     }

```
['[597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597-L597)']
```solidity
597:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256) { // <= FOUND
598:         return _bitMap | (1 << _index);
599:     }

```
['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L129-L177)']
```solidity
110:     function verifyCompressedStateDiffs(
111:         uint256 _numberOfStateDiffs,
112:         uint256 _enumerationIndexSize,
113:         bytes calldata _stateDiffs,
114:         bytes calldata _compressedStateDiffs
115:     ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
116:         
117:         
118:         
119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");
120: 
121:         uint256 numberOfInitialWrites = uint256(_compressedStateDiffs.readUint16(0));
122: 
123:         uint256 stateDiffPtr = 2;
124:         uint256 numInitialWritesProcessed = 0;
125: 
126:         
127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84); // <= FOUND
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++;
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92);
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr])); // <= FOUND
144:             stateDiffPtr++;
145:             uint8 operation = metadata & OPERATION_BITMASK; // <= FOUND
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET; // <= FOUND
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }
155: 
156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
157: 
158:         
159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
160:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
161:             uint64 enumIndex = stateDiff.readUint64(84); // <= FOUND
162:             if (enumIndex == 0) {
163:                 continue;
164:             }
165: 
166:             uint256 initValue = stateDiff.readUint256(92);
167:             uint256 finalValue = stateDiff.readUint256(124);
168:             uint256 compressedEnumIndex = _sliceToUint256(
169:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
170:             );
171:             require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");
172:             stateDiffPtr += _enumerationIndexSize;
173: 
174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr])); // <= FOUND
175:             stateDiffPtr += 1;
176:             uint8 operation = metadata & OPERATION_BITMASK; // <= FOUND
177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET; // <= FOUND
178:             _verifyValueCompression(
179:                 initValue,
180:                 finalValue,
181:                 operation,
182:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
183:             );
184:             stateDiffPtr += len;
185:         }
186: 
187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");
188: 
189:         stateDiffHash = EfficientCall.keccak(_stateDiffs);
190:     }

```
['[161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L161-L161)']
```solidity
159:     function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool) {
160:         require(_signature.length == 65, "Signature length is incorrect");
161:         uint8 v; // <= FOUND
162:         bytes32 r;
163:         bytes32 s;
164:         
165:         
166:         
167:         
168:         assembly {
169:             r := mload(add(_signature, 0x20))
170:             s := mload(add(_signature, 0x40))
171:             v := and(mload(add(_signature, 0x41)), 0xff)
172:         }
173:         require(v == 27 || v == 28, "v is neither 27 nor 28");
174: 
175:         
176:         
177:         
178:         
179:         
180:         
181:         
182:         
183:         
184:         require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s");
185: 
186:         address recoveredAddress = ecrecover(_hash, v, r, s);
187: 
188:         return recoveredAddress == address(this) && recoveredAddress != address(0);
189:     }

```
['[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75-L75)']
```solidity
74:     function _validateBytecode(bytes32 _bytecodeHash) internal pure {
75:         uint8 version = uint8(_bytecodeHash[0]); // <= FOUND
76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
77: 
78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");
79:     }

```
['[200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L200-L300)']
```solidity
194:     function publishPubdataAndClearState(
195:         bytes calldata _totalL2ToL1PubdataAndStateDiffs
196:     ) external onlyCallFromBootloader {
197:         uint256 calldataPtr = 0;
198: 
199:         
200:         uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND
201:         require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");
202:         calldataPtr += 4;
203: 
204:         bytes32[] memory l2ToL1LogsTreeArray = new bytes32[](L2_TO_L1_LOGS_MERKLE_TREE_LEAVES);
205:         bytes32 reconstructedChainedLogsHash;
206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }
214:         require(
215:             reconstructedChainedLogsHash == chainedLogsHash,
216:             "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217:         );
218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) {
219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;
220:         }
221:         uint256 nodesOnCurrentLevel = L2_TO_L1_LOGS_MERKLE_TREE_LEAVES;
222:         while (nodesOnCurrentLevel > 1) {
223:             nodesOnCurrentLevel /= 2;
224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
225:                 l2ToL1LogsTreeArray[i] = keccak256(
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );
228:             }
229:         }
230:         bytes32 l2ToL1LogsTreeRoot = l2ToL1LogsTreeArray[0];
231: 
232:         
233:         uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND
234:         calldataPtr += 4;
235:         bytes32 reconstructedChainedMessagesHash;
236:         for (uint256 i = 0; i < numberOfMessages; ++i) {
237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND
238:             calldataPtr += 4;
239:             bytes32 hashedMessage = EfficientCall.keccak(
240:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
241:             );
242:             calldataPtr += currentMessageLength;
243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));
244:         }
245:         require(
246:             reconstructedChainedMessagesHash == chainedMessagesHash,
247:             "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248:         );
249: 
250:         
251:         uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND
252:         calldataPtr += 4;
253:         bytes32 reconstructedChainedL1BytecodesRevealDataHash;
254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) {
255:             uint32 currentBytecodeLength = uint32( // <= FOUND
256:                 bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
257:             );
258:             calldataPtr += 4;
259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260:                 abi.encode(
261:                     reconstructedChainedL1BytecodesRevealDataHash,
262:                     Utils.hashL2Bytecode(
263:                         _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264:                     )
265:                 )
266:             );
267:             calldataPtr += currentBytecodeLength;
268:         }
269:         require(
270:             reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271:             "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272:         );
273: 
274:         
275:         
276:         
277:         
278:         
279:         require(
280:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281:                 STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282:             "state diff compression version mismatch"
283:         );
284:         calldataPtr++;
285: 
286:         uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));
287:         calldataPtr += 3;
288: 
289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr])); // <= FOUND
290:         calldataPtr++;
291: 
292:         bytes calldata compressedStateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
293:             compressedStateDiffSize];
294:         calldataPtr += compressedStateDiffSize;
295: 
296:         bytes calldata totalL2ToL1Pubdata = _totalL2ToL1PubdataAndStateDiffs[:calldataPtr];
297: 
298:         require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");
299: 
300:         uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND
301:         calldataPtr += 4;
302: 
303:         bytes calldata stateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
304:             (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];
305:         calldataPtr += numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE;
306: 
307:         bytes32 stateDiffHash = COMPRESSOR_CONTRACT.verifyCompressedStateDiffs(
308:             numberOfStateDiffs,
309:             enumerationIndexSize,
310:             stateDiffs,
311:             compressedStateDiffs
312:         );
313: 
314:         
315:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
316: 
317:         PUBDATA_CHUNK_PUBLISHER.chunkAndPublishPubdata(totalL2ToL1Pubdata);
318: 
319:         
320:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)), l2ToL1LogsTreeRoot);
321:         SystemContractHelper.toL1(
322:             true,
323:             bytes32(uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)),
324:             EfficientCall.keccak(totalL2ToL1Pubdata)
325:         );
326:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.STATE_DIFF_HASH_KEY)), stateDiffHash);
327: 
328:         
329:         chainedLogsHash = bytes32(0);
330:         numberOfLogsToProcess = 0;
331:         chainedMessagesHash = bytes32(0);
332:         chainedL1BytecodesRevealDataHash = bytes32(0);
333:     }

```
['[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L254-L254)']
```solidity
254:     function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId) { // <= FOUND
255:         shardId = uint8(extractNumberFromMeta(meta, META_SHARD_ID_OFFSET, 8));
256:     }

```
['[263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L263-L263)']
```solidity
263:     function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId) { // <= FOUND
264:         callerShardId = uint8(extractNumberFromMeta(meta, META_CALLER_SHARD_ID_OFFSET, 8));
265:     }

```
['[272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L272-L272)']
```solidity
272:     function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId) { // <= FOUND
273:         codeShardId = uint8(extractNumberFromMeta(meta, META_CODE_SHARD_ID_OFFSET, 8));
274:     }

```
['[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L96-L101)']
```solidity
95:     function getFarCallABI(
96:         uint32 dataOffset, // <= FOUND
97:         uint32 memoryPage, // <= FOUND
98:         uint32 dataStart, // <= FOUND
99:         uint32 dataLength, // <= FOUND
100:         uint32 gasPassed, // <= FOUND
101:         uint8 shardId, // <= FOUND
102:         CalldataForwardingMode forwardingMode,
103:         bool isConstructorCall,
104:         bool isSystemCall
105:     ) internal pure returns (uint256 farCallAbi) {
106:         
107:         farCallAbi = getFarCallABIWithEmptyFatPointer(
108:             gasPassed,
109:             shardId,
110:             forwardingMode,
111:             isConstructorCall,
112:             isSystemCall
113:         );
114:         
115:         farCallAbi |= dataOffset;
116:         farCallAbi |= (uint256(memoryPage) << 32);
117:         farCallAbi |= (uint256(dataStart) << 64);
118:         farCallAbi |= (uint256(dataLength) << 96);
119:     }

```
['[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L122-L123)']
```solidity
121:     function getFarCallABIWithEmptyFatPointer(
122:         uint32 gasPassed, // <= FOUND
123:         uint8 shardId, // <= FOUND
124:         CalldataForwardingMode forwardingMode,
125:         bool isConstructorCall,
126:         bool isSystemCall
127:     ) internal pure returns (uint256 farCallAbiWithEmptyFatPtr) {
128:         farCallAbiWithEmptyFatPtr |= (uint256(gasPassed) << 192);
129:         farCallAbiWithEmptyFatPtr |= (uint256(forwardingMode) << 224);
130:         farCallAbiWithEmptyFatPtr |= (uint256(shardId) << 232);
131:         if (isConstructorCall) {
132:             farCallAbiWithEmptyFatPtr |= (1 << 240);
133:         }
134:         if (isSystemCall) {
135:             farCallAbiWithEmptyFatPtr |= (1 << 248);
136:         }
137:     }

```
['[93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93-L93)']
```solidity
50:     function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {
51:         require(_l1Address != address(0), "in6"); 
52:         l1Address = _l1Address;
53: 
54:         l2Bridge = msg.sender;
55: 
56:         
57:         (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(
58:             _data,
59:             (bytes, bytes, bytes)
60:         );
61: 
62:         ERC20Getters memory getters;
63:         string memory decodedName;
64:         string memory decodedSymbol;
65: 
66:         
67:         
68: 
69:         
70:         
71:         
72:         
73:         
74: 
75:         try this.decodeString(nameBytes) returns (string memory nameString) {
76:             decodedName = nameString;
77:         } catch {
78:             getters.ignoreName = true;
79:         }
80: 
81:         try this.decodeString(symbolBytes) returns (string memory symbolString) {
82:             decodedSymbol = symbolString;
83:         } catch {
84:             getters.ignoreSymbol = true;
85:         }
86: 
87:         
88:         __ERC20_init_unchained(decodedName, decodedSymbol);
89: 
90:         
91:         __ERC20Permit_init(decodedName);
92: 
93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) { // <= FOUND
94:             
95:             decimals_ = decimalsUint8;
96:         } catch {
97:             getters.ignoreDecimals = true;
98:         }
99: 
100:         availableGetters = getters;
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);
102:     }

```
['[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L115-L115)']
```solidity
111:     function reinitializeToken(
112:         ERC20Getters calldata _availableGetters,
113:         string memory _newName,
114:         string memory _newSymbol,
115:         uint8 _version // <= FOUND
116:     ) external onlyNextVersion(_version) reinitializer(_version) {
117:         
118:         
119:         address beaconAddress = _getBeacon();
120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");
121: 
122:         __ERC20_init_unchained(_newName, _newSymbol);
123:         __ERC20Permit_init(_newName);
124:         availableGetters = _availableGetters;
125: 
126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);
127:     }

```
['[183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L183-L183)']
```solidity
183:     function decodeUint8(bytes memory _input) external pure returns (uint8 result) { // <= FOUND
184:         (result) = abi.decode(_input, (uint8));
185:     }

```
['[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L31-L31)']
```solidity
31: uint8 private decimals_; // <= FOUND

```
['[182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L182-L182)']
```solidity
176:     function claimFailedDeposit(
177:         address _depositSender,
178:         address _l1Token,
179:         bytes32 _l2TxHash,
180:         uint256 _l2BatchNumber,
181:         uint256 _l2MessageIndex,
182:         uint16 _l2TxNumberInBatch, // <= FOUND
183:         bytes32[] calldata _merkleProof
184:     ) external nonReentrant {
185:         uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
186:         require(amount != 0, "2T"); 
187:         delete depositAmount[_depositSender][_l1Token][_l2TxHash];
188: 
189:         sharedBridge.claimFailedDepositLegacyErc20Bridge(
190:             _depositSender,
191:             _l1Token,
192:             amount,
193:             _l2TxHash,
194:             _l2BatchNumber,
195:             _l2MessageIndex,
196:             _l2TxNumberInBatch,
197:             _merkleProof
198:         );
199:         emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);
200:     }

```
['[211](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L211-L211)']
```solidity
208:     function finalizeWithdrawal(
209:         uint256 _l2BatchNumber,
210:         uint256 _l2MessageIndex,
211:         uint16 _l2TxNumberInBatch, // <= FOUND
212:         bytes calldata _message,
213:         bytes32[] calldata _merkleProof
214:     ) external nonReentrant {
215:         require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw");
216:         
217: 
218:         (address l1Receiver, address l1Token, uint256 amount) = sharedBridge.finalizeWithdrawalLegacyErc20Bridge(
219:             _l2BatchNumber,
220:             _l2MessageIndex,
221:             _l2TxNumberInBatch,
222:             _message,
223:             _merkleProof
224:         );
225:         emit WithdrawalFinalized(l1Receiver, l1Token, amount);
226:     }

```
['[285](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L285-L285)']
```solidity
277:     function claimFailedDeposit(
278:         uint256 _chainId,
279:         address _depositSender,
280:         address _l1Token,
281:         uint256 _amount,
282:         bytes32 _l2TxHash,
283:         uint256 _l2BatchNumber,
284:         uint256 _l2MessageIndex,
285:         uint16 _l2TxNumberInBatch, // <= FOUND
286:         bytes32[] calldata _merkleProof
287:     ) external override {
288:         _claimFailedDeposit(
289:             false,
290:             _chainId,
291:             _depositSender,
292:             _l1Token,
293:             _amount,
294:             _l2TxHash,
295:             _l2BatchNumber,
296:             _l2MessageIndex,
297:             _l2TxNumberInBatch,
298:             _merkleProof
299:         );
300:     }

```
['[312](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L312-L312)']
```solidity
303:     function _claimFailedDeposit(
304:         bool _checkedInLegacyBridge,
305:         uint256 _chainId,
306:         address _depositSender,
307:         address _l1Token,
308:         uint256 _amount,
309:         bytes32 _l2TxHash,
310:         uint256 _l2BatchNumber,
311:         uint256 _l2MessageIndex,
312:         uint16 _l2TxNumberInBatch, // <= FOUND
313:         bytes32[] calldata _merkleProof
314:     ) internal nonReentrant {
315:         {
316:             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                 _chainId,
318:                 _l2TxHash,
319:                 _l2BatchNumber,
320:                 _l2MessageIndex,
321:                 _l2TxNumberInBatch,
322:                 _merkleProof,
323:                 TxStatus.Failure
324:             );
325:             require(proofValid, "yn");
326:         }
327:         require(_amount > 0, "y1");
328: 
329:         {
330:             bool notCheckedInLegacyBridgeOrWeCanCheckDeposit;
331:             {
332:                 
333:                 bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);
334:                 
335:                 
336:                 
337:                 notCheckedInLegacyBridgeOrWeCanCheckDeposit = (!_checkedInLegacyBridge) || weCanCheckDepositHere;
338:             }
339:             if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
342:                 require(dataHash == txDataHash, "ShB: d.it not hap");
343:                 delete depositHappened[_chainId][_l2TxHash];
344:             }
345:         }
346: 
347:         if (!hyperbridgingEnabled[_chainId]) {
348:             
349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
350:             chainBalance[_chainId][_l1Token] -= _amount;
351:         }
352: 
353:         
354:         if (_l1Token == ETH_TOKEN_ADDRESS) {
355:             bool callSuccess;
356:             
357:             assembly {
358:                 callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)
359:             }
360:             require(callSuccess, "ShB: claimFailedDeposit failed");
361:         } else {

```
['[389](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L389-L389)']
```solidity
385:     function finalizeWithdrawal(
386:         uint256 _chainId,
387:         uint256 _l2BatchNumber,
388:         uint256 _l2MessageIndex,
389:         uint16 _l2TxNumberInBatch, // <= FOUND
390:         bytes calldata _message,
391:         bytes32[] calldata _merkleProof
392:     ) external override {
393:         
394:         
395:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
396:             require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");
397:         }
398:         _finalizeWithdrawal(_chainId, _l2BatchNumber, _l2MessageIndex, _l2TxNumberInBatch, _message, _merkleProof);
399:     }

```
['[413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L413-L413)']
```solidity
409:     function _finalizeWithdrawal(
410:         uint256 _chainId,
411:         uint256 _l2BatchNumber,
412:         uint256 _l2MessageIndex,
413:         uint16 _l2TxNumberInBatch, // <= FOUND
414:         bytes calldata _message,
415:         bytes32[] calldata _merkleProof
416:     ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;
419: 
420:         
421:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
422:             
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");
428:         }
429: 
430:         MessageParams memory messageParams = MessageParams({
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });
435:         (l1Receiver, l1Token, amount) = _checkWithdrawal(_chainId, messageParams, _message, _merkleProof);
436: 
437:         if (!hyperbridgingEnabled[_chainId]) {
438:             
439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); 
440:             chainBalance[_chainId][l1Token] -= amount;
441:         }
442: 
443:         if (l1Token == ETH_TOKEN_ADDRESS) {
444:             bool callSuccess;
445:             
446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }
449:             require(callSuccess, "ShB: withdraw failed");
450:         } else {
451:             
452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
453:         }
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
455:     }

```
['[618](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L618-L618)']
```solidity
615:     function finalizeWithdrawalLegacyErc20Bridge(
616:         uint256 _l2BatchNumber,
617:         uint256 _l2MessageIndex,
618:         uint16 _l2TxNumberInBatch, // <= FOUND
619:         bytes calldata _message,
620:         bytes32[] calldata _merkleProof
621:     ) external override onlyLegacyBridge returns (address l1Receiver, address l1Token, uint256 amount) {
622:         (l1Receiver, l1Token, amount) = _finalizeWithdrawal(
623:             ERA_CHAIN_ID,
624:             _l2BatchNumber,
625:             _l2MessageIndex,
626:             _l2TxNumberInBatch,
627:             _message,
628:             _merkleProof
629:         );
630:     }

```
['[651](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L651-L651)']
```solidity
644:     function claimFailedDepositLegacyErc20Bridge(
645:         address _depositSender,
646:         address _l1Token,
647:         uint256 _amount,
648:         bytes32 _l2TxHash,
649:         uint256 _l2BatchNumber,
650:         uint256 _l2MessageIndex,
651:         uint16 _l2TxNumberInBatch, // <= FOUND
652:         bytes32[] calldata _merkleProof
653:     ) external override onlyLegacyBridge {
654:         _claimFailedDeposit(
655:             true,
656:             ERA_CHAIN_ID,
657:             _depositSender,
658:             _l1Token,
659:             _amount,
660:             _l2TxHash,
661:             _l2BatchNumber,
662:             _l2MessageIndex,
663:             _l2TxNumberInBatch,
664:             _merkleProof
665:         );
666:     }

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L181-L181)']
```solidity
176:     function proveL1ToL2TransactionStatus(
177:         uint256 _chainId,
178:         bytes32 _l2TxHash,
179:         uint256 _l2BatchNumber,
180:         uint256 _l2MessageIndex,
181:         uint16 _l2TxNumberInBatch, // <= FOUND
182:         bytes32[] calldata _merkleProof,
183:         TxStatus _status
184:     ) external view override returns (bool) {
185:         address stateTransition = getStateTransition(_chainId);
186:         return
187:             IZkSyncStateTransition(stateTransition).proveL1ToL2TransactionStatus(
188:                 _l2TxHash,
189:                 _l2BatchNumber,
190:                 _l2MessageIndex,
191:                 _l2TxNumberInBatch,
192:                 _merkleProof,
193:                 _status
194:             );
195:     }

```
['[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L78-L78)']
```solidity
74:     function proveL1ToL2TransactionStatus(
75:         bytes32 _l2TxHash,
76:         uint256 _l2BatchNumber,
77:         uint256 _l2MessageIndex,
78:         uint16 _l2TxNumberInBatch, // <= FOUND
79:         bytes32[] calldata _merkleProof,
80:         TxStatus _status
81:     ) public view returns (bool) {
82:         
83:         
84:         
85:         
86:         
87:         
88:         
89:         
90:         
91:         
92:         L2Log memory l2Log = L2Log({
93:             l2ShardId: 0,
94:             isService: true,
95:             txNumberInBatch: _l2TxNumberInBatch,
96:             sender: L2_BOOTLOADER_ADDRESS,
97:             key: _l2TxHash,
98:             value: bytes32(uint256(_status))
99:         });
100:         return _proveL2LogInclusion(_l2BatchNumber, _l2MessageIndex, l2Log, _merkleProof);
101:     }

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L181-L181)']
```solidity
178:     function finalizeEthWithdrawal(
179:         uint256 _l2BatchNumber,
180:         uint256 _l2MessageIndex,
181:         uint16 _l2TxNumberInBatch, // <= FOUND
182:         bytes calldata _message,
183:         bytes32[] calldata _merkleProof
184:     ) external nonReentrant {
185:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox");
186:         IL1SharedBridge(s.baseTokenBridge).finalizeWithdrawal(
187:             ERA_CHAIN_ID,
188:             _l2BatchNumber,
189:             _l2MessageIndex,
190:             _l2TxNumberInBatch,
191:             _message,
192:             _merkleProof
193:         );
194:     }

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208-L208)']
```solidity
205:     function _addOneFunction(address _facet, bytes4 _selector, bool _isSelectorFreezable) private {
206:         DiamondStorage storage ds = getDiamondStorage();
207: 
208:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16(); // <= FOUND
209: 
210:         
211:         
212:         
213:         if (selectorPosition != 0) {
214:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
215:             require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");
216:         }
217: 
218:         ds.selectorToFacet[_selector] = SelectorToFacet({
219:             facetAddress: _facet,
220:             selectorPosition: selectorPosition,
221:             isFreezable: _isSelectorFreezable
222:         });
223:         ds.facetToSelectors[_facet].selectors.push(_selector);
224:     }

```
['[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L19-L19)']
```solidity
19:     function readUint16(bytes calldata _bytes, uint256 _start) internal pure returns (uint16 result) { // <= FOUND
20:         assembly {
21:             let offset := sub(_bytes.offset, 30)
22:             result := calldataload(add(offset, _start))
23:         }
24:     }

```
['[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L89-L89)']
```solidity
89: uint16 public txNumberInBlock; // <= FOUND

```
['[503](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L503-L503)']
```solidity
487:     function _parseL2WithdrawalMessage(
488:         uint256 _chainId,
489:         bytes memory _l2ToL1message
490:     ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
491:         
492:         
493:         
494:         
495:         
496:         
497:         
498:         
499: 
500:         
501:         require(_l2ToL1message.length >= 56, "ShB wrong msg len"); 
502: 
503:         (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0); // <= FOUND
504:         if (bytes4(functionSignature) == IMailbox.finalizeEthWithdrawal.selector) {
505:             
506:             (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
507:             (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
508:             l1Token = bridgehub.baseToken(_chainId);
509:         } else if (bytes4(functionSignature) == IL1ERC20Bridge.finalizeWithdrawal.selector) {
510:             
511: 
512:             
513: 
514:             
515:             
516:             
517:             require(_l2ToL1message.length == 76, "ShB wrong msg len 2");
518:             (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
519:             (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
520:             (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
521:         } else {
522:             revert("ShB Incorrect message function selector");
523:         }
524:     }

```
['[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96-L96)']
```solidity
96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner { // <= FOUND
97:         executionDelay = _executionDelay;
98:         emit NewExecutionDelay(_executionDelay);
99:     }

```
['[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L115-L115)']
```solidity
108:     function commitBatches(
109:         StoredBatchInfo calldata,
110:         CommitBatchInfo[] calldata _newBatchesData
111:     ) external onlyValidator(ERA_CHAIN_ID) {
112:         unchecked {
113:             
114:             
115:             uint32 timestamp = uint32(block.timestamp); // <= FOUND
116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
117:                 committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
118:             }
119:         }
120: 
121:         _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
122:     }

```
['[134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L134-L134)']
```solidity
126:     function commitBatchesSharedBridge(
127:         uint256 _chainId,
128:         StoredBatchInfo calldata,
129:         CommitBatchInfo[] calldata _newBatchesData
130:     ) external onlyValidator(_chainId) {
131:         unchecked {
132:             
133:             
134:             uint32 timestamp = uint32(block.timestamp); // <= FOUND
135:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
136:                 committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
137:             }
138:         }
139: 
140:         _propagateToZkSyncStateTransition(_chainId);
141:     }

```
['[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19-L19)']
```solidity
19:     function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset) { // <= FOUND
20:         assembly {
21:             offset := add(_start, 4)
22:             result := mload(add(_bytes, offset))
23:         }
24:     }

```
['[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L18-L18)']
```solidity
18:     function get(Uint32Map storage _map, uint256 _index) internal view returns (uint32 result) { // <= FOUND
19:         unchecked {
20:             
21:             
22:             
23:             uint256 mapValue = _map.map[_index / 8];
24: 
25:             
26:             
27:             uint256 bitOffset = (_index & 7) * 32;
28: 
29:             
30:             result = uint32(mapValue >> bitOffset);
31:         }
32:     }

```
['[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L38-L54)']
```solidity
38:     function set(Uint32Map storage _map, uint256 _index, uint32 _value) internal { // <= FOUND
39:         unchecked {
40:             
41:             
42:             
43:             uint256 mapIndex = _index / 8;
44:             uint256 mapValue = _map.map[mapIndex];
45: 
46:             
47:             
48:             uint256 bitOffset = (_index & 7) * 32;
49: 
50:             
51:             
52: 
53:             
54:             uint32 oldValue = uint32(mapValue >> bitOffset); // <= FOUND
55: 
56:             
57:             uint256 newValueXorOldValue = uint256(oldValue ^ _value);
58: 
59:             
60:             
61:             _map.map[mapIndex] = (newValueXorOldValue << bitOffset) ^ mapValue;
62:         }
63:     }

```
['[133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L133-L135)']
```solidity
131:     function _execute(Transaction calldata _transaction) internal {
132:         address to = address(uint160(_transaction.to));
133:         uint128 value = Utils.safeCastToU128(_transaction.value); // <= FOUND
134:         bytes calldata data = _transaction.data;
135:         uint32 gas = Utils.safeCastToU32(gasleft()); // <= FOUND
136: 
137:         
138:         bool isSystemCall;
139:         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) {
140:             bytes4 selector = bytes4(data[:4]);
141:             
142:             
143:             isSystemCall =
144:                 selector == DEPLOYER_SYSTEM_CONTRACT.create.selector ||
145:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2.selector ||
146:                 selector == DEPLOYER_SYSTEM_CONTRACT.createAccount.selector ||
147:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2Account.selector;
148:         }
149:         bool success = EfficientCall.rawCall(gas, to, value, data, isSystemCall);
150:         if (!success) {
151:             EfficientCall.propagateRevert();
152:         }
153:     }

```
['[261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L261-L264)']
```solidity
245:     function _loadFarCallABIIntoActivePtr(
246:         uint256 _gas,
247:         bytes calldata _data,
248:         bool _isConstructor,
249:         bool _isSystem
250:     ) private view {
251:         SystemContractHelper.loadCalldataIntoActivePtr();
252: 
253:         uint256 dataOffset;
254:         assembly {
255:             dataOffset := _data.offset
256:         }
257: 
258:         
259:         SystemContractHelper.ptrAddIntoActive(uint32(dataOffset));
260:         
261:         uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset)); // <= FOUND
262:         SystemContractHelper.ptrShrinkIntoActive(shrinkTo);
263: 
264:         uint32 gas = Utils.safeCastToU32(_gas); // <= FOUND
265:         uint256 farCallAbi = SystemContractsCaller.getFarCallABIWithEmptyFatPointer(
266:             gas,
267:             
268:             0,
269:             CalldataForwardingMode.ForwardFatPointer,
270:             _isConstructor,
271:             _isSystem
272:         );
273:         SystemContractHelper.ptrPackIntoActivePtr(farCallAbi);
274:     }

```
['[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L94-L94)']
```solidity
94:     function ptrAddIntoActive(uint32 _value) internal view { // <= FOUND
95:         address callAddr = PTR_ADD_INTO_ACTIVE_CALL_ADDRESS;
96:         uint256 cleanupMask = UINT32_MASK;
97:         assembly {
98:             
99:             _value := and(_value, cleanupMask)
100:             pop(staticcall(_value, callAddr, 0, 0xFFFF, 0, 0))
101:         }
102:     }

```
['[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L106-L106)']
```solidity
106:     function ptrShrinkIntoActive(uint32 _shrink) internal view { // <= FOUND
107:         address callAddr = PTR_SHRINK_INTO_ACTIVE_CALL_ADDRESS;
108:         uint256 cleanupMask = UINT32_MASK;
109:         assembly {
110:             
111:             _shrink := and(_shrink, cleanupMask)
112:             pop(staticcall(_shrink, callAddr, 0, 0xFFFF, 0, 0))
113:         }
114:     }

```
['[125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L125-L129)']
```solidity
124:     function packPrecompileParams(
125:         uint32 _inputMemoryOffset, // <= FOUND
126:         uint32 _inputMemoryLength, // <= FOUND
127:         uint32 _outputMemoryOffset, // <= FOUND
128:         uint32 _outputMemoryLength, // <= FOUND
129:         uint64 _perPrecompileInterpreted // <= FOUND
130:     ) internal pure returns (uint256 rawParams) {
131:         rawParams = _inputMemoryOffset;
132:         rawParams |= uint256(_inputMemoryLength) << 32;
133:         rawParams |= uint256(_outputMemoryOffset) << 64;
134:         rawParams |= uint256(_outputMemoryLength) << 96;
135:         rawParams |= uint256(_perPrecompileInterpreted) << 192;
136:     }

```
['[150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L150-L151)']
```solidity
148:     function unsafePrecompileCall(
149:         uint256 _rawParams,
150:         uint32 _gasToBurn, // <= FOUND
151:         uint32 _pubdataToSpend // <= FOUND
152:     ) internal view returns (bool success) {
153:         address callAddr = PRECOMPILE_CALL_ADDRESS;
154: 
155:         uint256 params = uint256(_gasToBurn) + (uint256(_pubdataToSpend) << 32);
156: 
157:         uint256 cleanupMask = UINT64_MASK;
158:         assembly {
159:             
160:             params := and(params, cleanupMask)
161:             success := staticcall(_rawParams, callAddr, params, 0xFFFF, 0, 0)
162:         }
163:     }

```
['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L227-L227)']
```solidity
227:     function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished) { // <= FOUND
228:         pubdataPublished = uint32(extractNumberFromMeta(meta, META_GAS_PER_PUBDATA_BYTE_OFFSET, 32));
229:     }

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L237-L237)']
```solidity
237:     function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize) { // <= FOUND
238:         heapSize = uint32(extractNumberFromMeta(meta, META_HEAP_SIZE_OFFSET, 32));
239:     }

```
['[246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L246-L246)']
```solidity
246:     function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize) { // <= FOUND
247:         auxHeapSize = uint32(extractNumberFromMeta(meta, META_AUX_HEAP_SIZE_OFFSET, 32));
248:     }

```
['[344](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L344-L344)']
```solidity
344:     function burnGas(uint32 _gasToPay, uint32 _pubdataToSpend) internal view { // <= FOUND
345:         bool precompileCallSuccess = unsafePrecompileCall(
346:             0, 
347:             _gasToPay,
348:             _pubdataToSpend
349:         );
350:         require(precompileCallSuccess, "Failed to charge gas");
351:     }

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L37-L44)']
```solidity
37:     function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) { // <= FOUND
38:         address callAddr = SYSTEM_CALL_CALL_ADDRESS;
39: 
40:         uint32 dataStart; // <= FOUND
41:         assembly {
42:             dataStart := add(data, 0x20)
43:         }
44:         uint32 dataLength = uint32(Utils.safeCastToU32(data.length)); // <= FOUND
45: 
46:         uint256 farCallAbi = getFarCallABI(
47:             0,
48:             0,
49:             dataStart,
50:             dataLength,
51:             gasLimit,
52:             
53:             0,
54:             CalldataForwardingMode.UseHeap,
55:             false,
56:             true
57:         );
58: 
59:         if (value == 0) {
60:             
61:             assembly {
62:                 success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)
63:             }
64:         } else {
65:             address msgValueSimulator = MSG_VALUE_SYSTEM_CONTRACT;
66:             
67:             
68:             uint256 forwardMask = MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT;
69: 
70:             assembly {
71:                 success := call(msgValueSimulator, callAddr, value, to, farCallAbi, forwardMask, 0)
72:             }
73:         }
74:     }

```
['[77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L77-L79)']
```solidity
76:     function systemCallWithReturndata(
77:         uint32 gasLimit, // <= FOUND
78:         address to,
79:         uint128 value, // <= FOUND
80:         bytes memory data
81:     ) internal returns (bool success, bytes memory returnData) {
82:         success = systemCall(gasLimit, to, value, data);
83: 
84:         uint256 size;
85:         assembly {
86:             size := returndatasize()
87:         }
88: 
89:         returnData = new bytes(size);
90:         assembly {
91:             returndatacopy(add(returnData, 0x20), 0, size)
92:         }
93:     }

```
['[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L26-L26)']
```solidity
26:     function readUint32(bytes calldata _bytes, uint256 _start) internal pure returns (uint32 result) { // <= FOUND
27:         assembly {
28:             let offset := sub(_bytes.offset, 28)
29:             result := calldataload(add(offset, _start))
30:         }
31:     }

```
['[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L53-L53)']
```solidity
53: uint32 public executionDelay; // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L68-L68)']
```solidity
44:     function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash) {
45:         
46:         
47:         
48:         
49:         
50:         
51: 
52:         bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
53:         
54:         bytes memory encodedGasParam;
55:         {
56:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
57:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
58:             encodedGasParam = bytes.concat(encodedGasPrice, encodedGasLimit);
59:         }
60: 
61:         bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
62:         bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
63:         
64:         
65:         bytes memory encodedDataLength;
66:         {
67:             
68:             uint64 txDataLen = uint64(_transaction.data.length); // <= FOUND
69:             if (txDataLen != 1) {
70:                 
71:                 encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);
72:             } else if (_transaction.data[0] >= 0x80) {
73:                 
74:                 encodedDataLength = hex"81";
75:             }
76:             
77:         }
78: 
79:         bytes memory rEncoded;
80:         {
81:             uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));
82:             rEncoded = RLPEncoder.encodeUint256(rInt);
83:         }
84:         bytes memory sEncoded;
85:         {
86:             uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));
87:             sEncoded = RLPEncoder.encodeUint256(sInt);
88:         }
89:         bytes memory vEncoded;
90:         {
91:             uint256 vInt = uint256(uint8(_transaction.signature[64]));
92:             require(vInt == 27 || vInt == 28, "Invalid v value");
93: 
94:             
95:             
96:             if (_transaction.reserved[0] != 0) {
97:                 vInt += 8 + block.chainid * 2;
98:             }
99: 
100:             vEncoded = RLPEncoder.encodeUint256(vInt);
101:         }
102: 
103:         bytes memory encodedListLength;
104:         unchecked {
105:             uint256 listLength = encodedNonce.length +
106:                 encodedGasParam.length +
107:                 encodedTo.length +
108:                 encodedValue.length +
109:                 encodedDataLength.length +
110:                 _transaction.data.length +
111:                 rEncoded.length +
112:                 sEncoded.length +
113:                 vEncoded.length;
114: 
115:             
116:             encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
117:         }

```
['[164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L164-L164)']
```solidity
139:     function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
140:         
141:         bytes memory encodedFixedLengthParams;
142:         {
143:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);
144:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
145:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
146:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
147:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
148:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
149:             encodedFixedLengthParams = bytes.concat(
150:                 encodedChainId,
151:                 encodedNonce,
152:                 encodedGasPrice,
153:                 encodedGasLimit,
154:                 encodedTo,
155:                 encodedValue
156:             );
157:         }
158: 
159:         
160:         
161:         bytes memory encodedDataLength;
162:         {
163:             
164:             uint64 txDataLen = uint64(_transaction.data.length); // <= FOUND
165:             if (txDataLen != 1) {
166:                 
167:                 encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);
168:             } else if (_transaction.data[0] >= 0x80) {
169:                 
170:                 encodedDataLength = hex"81";
171:             }
172:             
173:         }
174: 
175:         
176:         bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);
177: 
178:         bytes memory rEncoded;
179:         {
180:             uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));
181:             rEncoded = RLPEncoder.encodeUint256(rInt);
182:         }
183:         bytes memory sEncoded;
184:         {
185:             uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));
186:             sEncoded = RLPEncoder.encodeUint256(sInt);
187:         }
188:         bytes memory vEncoded;
189:         {
190:             uint256 vInt = uint256(uint8(_transaction.signature[64]));
191:             require(vInt == 27 || vInt == 28, "Invalid v value");
192: 
193:             vEncoded = RLPEncoder.encodeUint256(vInt - 27);
194:         }
195: 
196:         bytes memory encodedListLength;
197:         unchecked {
198:             uint256 listLength = encodedFixedLengthParams.length +
199:                 encodedDataLength.length +
200:                 _transaction.data.length +
201:                 encodedAccessListLength.length +
202:                 rEncoded.length +
203:                 sEncoded.length +
204:                 vEncoded.length;
205: 
206:             
207:             encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
208:         }
209: 
210:         return
211:             keccak256(
212:                 bytes.concat(
213:                     "\x01",

```
['[259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L259-L259)']
```solidity
229:     function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32) {
230:         
231:         
232: 
233:         
234:         bytes memory encodedFixedLengthParams;
235:         {
236:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);
237:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
238:             bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas);
239:             bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
240:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
241:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
242:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
243:             encodedFixedLengthParams = bytes.concat(
244:                 encodedChainId,
245:                 encodedNonce,
246:                 encodedMaxPriorityFeePerGas,
247:                 encodedMaxFeePerGas,
248:                 encodedGasLimit,
249:                 encodedTo,
250:                 encodedValue
251:             );
252:         }
253: 
254:         
255:         
256:         bytes memory encodedDataLength;
257:         {
258:             
259:             uint64 txDataLen = uint64(_transaction.data.length); // <= FOUND
260:             if (txDataLen != 1) {
261:                 
262:                 encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);
263:             } else if (_transaction.data[0] >= 0x80) {
264:                 
265:                 encodedDataLength = hex"81";
266:             }
267:             
268:         }
269: 
270:         
271:         bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);
272: 
273:         bytes memory rEncoded;
274:         {
275:             uint256 rInt = uint256(bytes32(_transaction.signature[0:32]));
276:             rEncoded = RLPEncoder.encodeUint256(rInt);
277:         }
278:         bytes memory sEncoded;
279:         {
280:             uint256 sInt = uint256(bytes32(_transaction.signature[32:64]));
281:             sEncoded = RLPEncoder.encodeUint256(sInt);
282:         }
283:         bytes memory vEncoded;
284:         {
285:             uint256 vInt = uint256(uint8(_transaction.signature[64]));
286:             require(vInt == 27 || vInt == 28, "Invalid v value");
287: 
288:             vEncoded = RLPEncoder.encodeUint256(vInt - 27);
289:         }
290: 
291:         bytes memory encodedListLength;
292:         unchecked {
293:             uint256 listLength = encodedFixedLengthParams.length +
294:                 encodedDataLength.length +
295:                 _transaction.data.length +
296:                 encodedAccessListLength.length +
297:                 rEncoded.length +
298:                 sEncoded.length +
299:                 vEncoded.length;
300: 
301:             
302:             encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
303:         }
304: 
305:         return
306:             keccak256(
307:                 bytes.concat(
308:                     "\x02",

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L65-L66)']
```solidity
44:     function publishCompressedBytecode(
45:         bytes calldata _bytecode,
46:         bytes calldata _rawCompressedData
47:     ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
48:         unchecked {
49:             (bytes calldata dictionary, bytes calldata encodedData) = _decodeRawBytecode(_rawCompressedData);
50: 
51:             require(
52:                 encodedData.length * 4 == _bytecode.length,
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             );
55: 
56:             require(
57:                 dictionary.length / 8 <= encodedData.length / 2,
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             );
60: 
61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
64: 
65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk); // <= FOUND
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4); // <= FOUND
67: 
68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
69:             }
70:         }
71: 
72:         bytecodeHash = Utils.hashL2Bytecode(_bytecode);
73:         L1_MESSENGER_CONTRACT.sendToL1(_rawCompressedData);
74:         KNOWN_CODE_STORAGE_CONTRACT.markBytecodeAsPublished(bytecodeHash);
75:     }

```
['[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L49-L49)']
```solidity
49:     function encodeNonSingleBytesLen(uint64 _len) internal pure returns (bytes memory) { // <= FOUND
50:         assert(_len != 1);
51:         return _encodeLength(_len, 0x80);
52:     }

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L56-L56)']
```solidity
56:     function encodeListLen(uint64 _len) internal pure returns (bytes memory) { // <= FOUND
57:         return _encodeLength(_len, 0xc0);
58:     }

```
['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L60-L60)']
```solidity
60:     function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) { // <= FOUND
61:         unchecked {
62:             if (_len < 56) {
63:                 encoded = new bytes(1);
64:                 encoded[0] = bytes1(uint8(_len + _offset));
65:             } else {
66:                 uint256 hbs = _highestByteSet(uint256(_len));
67: 
68:                 encoded = new bytes(hbs + 2);
69:                 encoded[0] = bytes1(uint8(_offset + hbs + 56));
70: 
71:                 uint256 lbs = 31 - hbs;
72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8);
73: 
74:                 assembly {
75:                     mstore(add(encoded, 0x21), shiftedVal)
76:                 }
77:             }
78:         }
79:     }

```
['[171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L171-L171)']
```solidity
147:     function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32) {
148:         
149:         
150:         
151:         
152:         
153:         
154: 
155:         bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
156:         
157:         bytes memory encodedGasParam;
158:         {
159:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
160:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
161:             encodedGasParam = bytes.concat(encodedGasPrice, encodedGasLimit);
162:         }
163: 
164:         bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
165:         bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
166:         
167:         
168:         bytes memory encodedDataLength;
169:         {
170:             
171:             uint64 txDataLen = uint64(_transaction.data.length); // <= FOUND
172:             if (txDataLen != 1) {
173:                 
174:                 encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);
175:             } else if (_transaction.data[0] >= 0x80) {
176:                 
177:                 encodedDataLength = hex"81";
178:             }
179:             
180:         }
181: 
182:         
183:         bytes memory encodedChainId;
184:         if (_transaction.reserved[0] != 0) {
185:             encodedChainId = bytes.concat(RLPEncoder.encodeUint256(block.chainid), hex"80_80");
186:         }
187: 
188:         bytes memory encodedListLength;
189:         unchecked {
190:             uint256 listLength = encodedNonce.length +
191:                 encodedGasParam.length +
192:                 encodedTo.length +
193:                 encodedValue.length +
194:                 encodedDataLength.length +
195:                 _transaction.data.length +
196:                 encodedChainId.length;
197: 
198:             
199:             encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
200:         }
201: 
202:         return
203:             keccak256(
204:                 bytes.concat(
205:                     encodedListLength,
206:                     encodedNonce,
207:                     encodedGasParam,
208:                     encodedTo,
209:                     encodedValue,
210:                     encodedDataLength,
211:                     _transaction.data,
212:                     encodedChainId
213:                 )
214:             );
215:     }

```
['[249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L249-L249)']
```solidity
219:     function _encodeHashEIP2930Transaction(Transaction calldata _transaction) private view returns (bytes32) {
220:         
221:         
222:         
223:         
224: 
225:         
226:         bytes memory encodedFixedLengthParams;
227:         {
228:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);
229:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
230:             bytes memory encodedGasPrice = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
231:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
232:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
233:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
234:             encodedFixedLengthParams = bytes.concat(
235:                 encodedChainId,
236:                 encodedNonce,
237:                 encodedGasPrice,
238:                 encodedGasLimit,
239:                 encodedTo,
240:                 encodedValue
241:             );
242:         }
243: 
244:         
245:         
246:         bytes memory encodedDataLength;
247:         {
248:             
249:             uint64 txDataLen = uint64(_transaction.data.length); // <= FOUND
250:             if (txDataLen != 1) {
251:                 
252:                 encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);
253:             } else if (_transaction.data[0] >= 0x80) {
254:                 
255:                 encodedDataLength = hex"81";
256:             }
257:             
258:         }
259: 
260:         
261:         bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);
262: 
263:         bytes memory encodedListLength;
264:         unchecked {
265:             uint256 listLength = encodedFixedLengthParams.length +
266:                 encodedDataLength.length +
267:                 _transaction.data.length +
268:                 encodedAccessListLength.length;
269: 
270:             
271:             encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
272:         }
273: 
274:         return
275:             keccak256(
276:                 bytes.concat(
277:                     "\x01",
278:                     encodedListLength,
279:                     encodedFixedLengthParams,
280:                     encodedDataLength,
281:                     _transaction.data,
282:                     encodedAccessListLength
283:                 )
284:             );
285:     }

```
['[321](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L321-L321)']
```solidity
289:     function _encodeHashEIP1559Transaction(Transaction calldata _transaction) private view returns (bytes32) {
290:         
291:         
292:         
293:         
294: 
295:         
296:         bytes memory encodedFixedLengthParams;
297:         {
298:             bytes memory encodedChainId = RLPEncoder.encodeUint256(block.chainid);
299:             bytes memory encodedNonce = RLPEncoder.encodeUint256(_transaction.nonce);
300:             bytes memory encodedMaxPriorityFeePerGas = RLPEncoder.encodeUint256(_transaction.maxPriorityFeePerGas);
301:             bytes memory encodedMaxFeePerGas = RLPEncoder.encodeUint256(_transaction.maxFeePerGas);
302:             bytes memory encodedGasLimit = RLPEncoder.encodeUint256(_transaction.gasLimit);
303:             bytes memory encodedTo = RLPEncoder.encodeAddress(address(uint160(_transaction.to)));
304:             bytes memory encodedValue = RLPEncoder.encodeUint256(_transaction.value);
305:             encodedFixedLengthParams = bytes.concat(
306:                 encodedChainId,
307:                 encodedNonce,
308:                 encodedMaxPriorityFeePerGas,
309:                 encodedMaxFeePerGas,
310:                 encodedGasLimit,
311:                 encodedTo,
312:                 encodedValue
313:             );
314:         }
315: 
316:         
317:         
318:         bytes memory encodedDataLength;
319:         {
320:             
321:             uint64 txDataLen = uint64(_transaction.data.length); // <= FOUND
322:             if (txDataLen != 1) {
323:                 
324:                 encodedDataLength = RLPEncoder.encodeNonSingleBytesLen(txDataLen);
325:             } else if (_transaction.data[0] >= 0x80) {
326:                 
327:                 encodedDataLength = hex"81";
328:             }
329:             
330:         }
331: 
332:         
333:         bytes memory encodedAccessListLength = RLPEncoder.encodeListLen(0);
334: 
335:         bytes memory encodedListLength;
336:         unchecked {
337:             uint256 listLength = encodedFixedLengthParams.length +
338:                 encodedDataLength.length +
339:                 _transaction.data.length +
340:                 encodedAccessListLength.length;
341: 
342:             
343:             encodedListLength = RLPEncoder.encodeListLen(uint64(listLength));
344:         }
345: 
346:         return
347:             keccak256(
348:                 bytes.concat(
349:                     "\x02",
350:                     encodedListLength,
351:                     encodedFixedLengthParams,
352:                     encodedDataLength,
353:                     _transaction.data,
354:                     encodedAccessListLength
355:                 )
356:             );
357:     }

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L33-L33)']
```solidity
33:     function readUint64(bytes calldata _bytes, uint256 _start) internal pure returns (uint64 result) { // <= FOUND
34:         assembly {
35:             let offset := sub(_bytes.offset, 24)
36:             result := calldataload(add(offset, _start))
37:         }
38:     }

```
['[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79-L81)']
```solidity
79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager { // <= FOUND
80:         uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator; // <= FOUND
81:         uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator; // <= FOUND
82: 
83:         s.baseTokenGasPriceMultiplierNominator = _nominator;
84:         s.baseTokenGasPriceMultiplierDenominator = _denominator;
85: 
86:         emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);
87:     }

```
['[133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L133-L133)']
```solidity
132:     function getBlockHashEVM(uint256 _block) external view returns (bytes32 hash) {
133:         uint128 blockNumber = currentVirtualL2BlockInfo.number; // <= FOUND
134: 
135:         VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo;
136: 
137:         
138:         
139:         
140:         
141:         
142:         
143:         
144:         if (blockNumber <= _block || blockNumber - _block > 256) {
145:             hash = bytes32(0);
146:         } else if (_block < currentVirtualBlockUpgradeInfo.virtualBlockStartBatch) {
147:             
148:             
149:             hash = batchHashes[_block];
150:         } else if (
151:             _block >= currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block &&
152:             currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0
153:         ) {
154:             hash = _getLatest257L2blockHash(_block);
155:         } else {
156:             
157:             
158:             
159:             hash = keccak256(abi.encode(_block));
160:         }
161:     }

```
['[172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L172-L172)']
```solidity
172:     function getBatchNumberAndTimestamp() public view returns (uint128 batchNumber, uint128 batchTimestamp) { // <= FOUND
173:         BlockInfo memory batchInfo = currentBatchInfo;
174:         batchNumber = batchInfo.number;
175:         batchTimestamp = batchInfo.timestamp;
176:     }

```
['[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L180-L180)']
```solidity
180:     function getL2BlockNumberAndTimestamp() public view returns (uint128 blockNumber, uint128 blockTimestamp) { // <= FOUND
181:         BlockInfo memory blockInfo = currentL2BlockInfo;
182:         blockNumber = blockInfo.number;
183:         blockTimestamp = blockInfo.timestamp;
184:     }

```
['[222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L222-L223)']
```solidity
221:     function _calculateL2BlockHash(
222:         uint128 _blockNumber, // <= FOUND
223:         uint128 _blockTimestamp, // <= FOUND
224:         bytes32 _prevL2BlockHash,
225:         bytes32 _blockTxsRollingHash
226:     ) internal pure returns (bytes32) {
227:         return keccak256(abi.encode(_blockNumber, _blockTimestamp, _prevL2BlockHash, _blockTxsRollingHash));
228:     }

```
['[233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L233-L233)']
```solidity
233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32) { // <= FOUND
234:         return keccak256(abi.encodePacked(uint32(_blockNumber)));
235:     }

```
['[241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L241-L241)']
```solidity
241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal { // <= FOUND
242:         require(_isFirstInBatch, "Upgrade transaction must be first");
243: 
244:         
245:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero");
246: 
247:         unchecked {
248:             bytes32 correctPrevBlockHash = _calculateLegacyL2BlockHash(_l2BlockNumber - 1);
249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect");
250: 
251:             
252:             
253:             
254:             
255:             _setL2BlockHash(_l2BlockNumber - 1, correctPrevBlockHash);
256:         }
257:     }

```
['[264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L264-L278)']
```solidity
263:     function _setVirtualBlock(
264:         uint128 _l2BlockNumber, // <= FOUND
265:         uint128 _maxVirtualBlocksToCreate, // <= FOUND
266:         uint128 _newTimestamp // <= FOUND
267:     ) internal {
268:         if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
269:             
270:             
271:             currentVirtualL2BlockInfo = currentL2BlockInfo;
272:             return;
273:         }
274: 
275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
276: 
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) {
278:             uint128 currentBatchNumber = currentBatchInfo.number; // <= FOUND
279: 
280:             
281:             
282:             
283:             virtualBlockInfo.number = currentBatchNumber;
284:             
285:             virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
286: 
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
288:             _maxVirtualBlocksToCreate -= 1;
289:         } else if (_maxVirtualBlocksToCreate == 0) {
290:             
291:             
292:             return;
293:         }
294: 
295:         virtualBlockInfo.number += _maxVirtualBlocksToCreate;
296:         virtualBlockInfo.timestamp = _newTimestamp;
297: 
298:         
299:         
300:         
301:         
302:         if (virtualBlockInfo.number >= _l2BlockNumber) {
303:             virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
304:             virtualBlockInfo.number = _l2BlockNumber;
305:         }
306: 
307:         currentVirtualL2BlockInfo = virtualBlockInfo;
308:     }

```
['[314](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L314-L314)']
```solidity
314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal { // <= FOUND
315:         
316:         currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp});
317: 
318:         
319:         _setL2BlockHash(_l2BlockNumber - 1, _prevL2BlockHash);
320: 
321:         
322:         currentL2BlockTxsRollingHash = bytes32(0);
323:     }

```
['[342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L342-L358)']
```solidity
341:     function setL2Block(
342:         uint128 _l2BlockNumber, // <= FOUND
343:         uint128 _l2BlockTimestamp, // <= FOUND
344:         bytes32 _expectedPrevL2BlockHash,
345:         bool _isFirstInBatch,
346:         uint128 _maxVirtualBlocksToCreate // <= FOUND
347:     ) external onlyCallFromBootloader {
348:         
349:         if (_isFirstInBatch) {
350:             uint128 currentBatchTimestamp = currentBatchInfo.timestamp; // <= FOUND
351:             require(
352:                 _l2BlockTimestamp >= currentBatchTimestamp,
353:                 "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354:             );
355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch");
356:         }
357: 
358:         (uint128 currentL2BlockNumber, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp(); // <= FOUND
359: 
360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) {
361:             
362:             
363:             _upgradeL2Blocks(_l2BlockNumber, _expectedPrevL2BlockHash, _isFirstInBatch);
364: 
365:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
366:         } else if (currentL2BlockNumber == _l2BlockNumber) {
367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch");
368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same");
369:             require(
370:                 _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371:                 "The previous hash of the same L2 block must be same"
372:             );
373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock");
374:         } else if (currentL2BlockNumber + 1 == _l2BlockNumber) {
375:             
376:             bytes32 prevL2BlockHash = _getLatest257L2blockHash(currentL2BlockNumber - 1);
377: 
378:             bytes32 pendingL2BlockHash = _calculateL2BlockHash(
379:                 currentL2BlockNumber,
380:                 currentL2BlockTimestamp,
381:                 prevL2BlockHash,
382:                 currentL2BlockTxsRollingHash
383:             );
384: 
385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect");
386:             require(
387:                 _l2BlockTimestamp > currentL2BlockTimestamp,
388:                 "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389:             );
390: 
391:             
392:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
393:         } else {
394:             revert("Invalid new L2 block number");
395:         }
396: 
397:         _setVirtualBlock(_l2BlockNumber, _maxVirtualBlocksToCreate, _l2BlockTimestamp);
398:     }

```
['[409](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L409-L410)']
```solidity
408:     function publishTimestampDataToL1() external onlyCallFromBootloader {
409:         (uint128 currentBatchNumber, uint128 currentBatchTimestamp) = getBatchNumberAndTimestamp(); // <= FOUND
410:         (, uint128 currentL2BlockTimestamp) = getL2BlockNumberAndTimestamp(); // <= FOUND
411: 
412:         
413:         require(currentBatchNumber > 0, "The current batch number must be greater than 0");
414: 
415:         
416:         uint256 packedTimestamps = (uint256(currentBatchTimestamp) << 128) | currentL2BlockTimestamp;
417: 
418:         SystemContractHelper.toL1(
419:             false,
420:             bytes32(uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)),
421:             bytes32(packedTimestamps)
422:         );
423:     }

```
['[427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L427-L428)']
```solidity
427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view { // <= FOUND
428:         uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp; // <= FOUND
429:         require(
430:             _newTimestamp > currentBlockTimestamp,
431:             "The timestamp of the batch must be greater than the timestamp of the previous block"
432:         );
433:     }

```
['[446](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L446-L450)']
```solidity
444:     function setNewBatch(
445:         bytes32 _prevBatchHash,
446:         uint128 _newTimestamp, // <= FOUND
447:         uint128 _expectedNewNumber, // <= FOUND
448:         uint256 _baseFee
449:     ) external onlyCallFromBootloader {
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp(); // <= FOUND
451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");
452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453: 
454:         _ensureBatchConsistentWithL2Block(_newTimestamp);
455: 
456:         batchHashes[previousBatchNumber] = _prevBatchHash;
457: 
458:         
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
460: 
461:         currentBatchInfo = newBlockInfo;
462: 
463:         baseFee = _baseFee;
464: 
465:         
466:         SystemContractHelper.toL1(false, bytes32(uint256(SystemLogKey.PREV_BATCH_HASH_KEY)), _prevBatchHash);
467:     }

```
['[497](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L497-L497)']
```solidity
496:     function currentBlockInfo() external view returns (uint256 blockInfo) {
497:         (uint128 blockNumber, uint128 blockTimestamp) = getBatchNumberAndTimestamp(); // <= FOUND
498:         blockInfo = (uint256(blockNumber) << 128) | uint256(blockTimestamp);
499:     }

```
['[168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L168-L168)']
```solidity
168:     function setValueForNextFarCall(uint128 _value) internal returns (bool success) { // <= FOUND
169:         uint256 cleanupMask = UINT128_MASK;
170:         address callAddr = SET_CONTEXT_VALUE_CALL_ADDRESS;
171:         assembly {
172:             
173:             _value := and(_value, cleanupMask)
174:             success := call(0, callAddr, _value, 0, 0xFFFF, 0, 0)
175:         }
176:     }

```


</details>

## [Gas-12] Use != 0 instead of > 0

### Resolution 
Replace spotted instances with != 0 for uints as this uses less gas

Num of instances: 26

### Findings 


<details><summary>Click to show findings</summary>

['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129-L129)']
```solidity
129:             require(amount > 0, "ShB: 0 amount to transfer"); // <= FOUND

```
['[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L159-L159)']
```solidity
158:             
159:             require(msg.value == 0, "ShB m.v > 0 b d.it"); // <= FOUND

```
['[202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202-L202)']
```solidity
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2"); // <= FOUND

```
['[327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327-L327)']
```solidity
327:         require(_amount > 0, "y1"); // <= FOUND

```
['[329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L329-L329)']
```solidity
329:         } else if (_refundRecipient.code.length > 0) { // <= FOUND

```
['[431](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L431-L431)']
```solidity
429:         
430:         
431:         if (_proof.serializedProof.length > 0) { // <= FOUND

```
['[593](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593-L593)']
```solidity
593:         return (_bitMap & (1 << _index)) > 0; // <= FOUND

```
['[631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631-L631)']
```solidity
631:         require(_pubdataCommitments.length > 0, "pl"); // <= FOUND

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L158)']
```solidity
158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set"); // <= FOUND

```
['[278](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L278-L278)']
```solidity
277:         
278:         if (refundRecipient.code.length > 0) { // <= FOUND

```
['[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107-L107)']
```solidity
107:             require(selectors.length > 0, "B");  // <= FOUND

```
['[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L135-L135)']
```solidity
132:         
133:         
134:         
135:         require(_facet.code.length > 0, "G"); // <= FOUND

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158-L158)']
```solidity
155:         
156:         
157:         
158:         require(_facet.code.length > 0, "K"); // <= FOUND

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24-L24)']
```solidity
24:         require(pathLength > 0, "xc"); // <= FOUND

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L105-L105)']
```solidity
102:         
103:         
104:         
105:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) { // <= FOUND

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24-L24)']
```solidity
24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA"); // <= FOUND

```
['[303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L303-L303)']
```solidity
303:         require(knownCodeMarker > 0, "The code hash is not known"); // <= FOUND

```
['[333](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L333-L333)']
```solidity
332:             
333:             if (value > 0) { // <= FOUND

```
['[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L156-L156)']
```solidity
156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0); // <= FOUND

```
['[152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L152-L152)']
```solidity
151:             _block >= currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block &&
152:             currentVirtualBlockUpgradeInfo.virtualBlockFinishL2Block > 0 // <= FOUND
153:         ) {

```
['[246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L246-L246)']
```solidity
245:         
246:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero"); // <= FOUND

```
['[287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287-L287)']
```solidity
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block"); // <= FOUND

```
['[355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355-L355)']
```solidity
355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch"); // <= FOUND

```
['[414](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L414-L414)']
```solidity
413:         
414:         require(currentBatchNumber > 0, "The current batch number must be greater than 0"); // <= FOUND

```
['[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124-L124)']
```solidity
124:         require(_amount > 0, "Amount cannot be zero"); // <= FOUND

```
['[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L72-L72)']
```solidity
72:             } else if (_transaction.data[0] >= 0x80) { // <= FOUND

```


</details>

## [Gas-13] Integer increments by one can be unchecked to save on gas fees

### Resolution 
Using unchecked increments in Solidity can save on gas fees by bypassing built-in overflow checks, thus optimizing gas usage, but requires careful assessment of potential risks and edge cases to avoid unintended consequences.

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L225)']
```solidity
224:     function _execute(Call[] calldata _calls) internal {
225:         for (uint256 i = 0; i < _calls.length; ++i) { // <= FOUND
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
227:             if (!success) {
228:                 
229:                 assembly {
230:                     revert(add(returnData, 0x20), mload(returnData))
231:                 }
232:             }
233:         }
234:     }

```
['[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580)']
```solidity
561:     function _encodeBlobAuxilaryOutput(
562:         bytes32[] memory _blobCommitments,
563:         bytes32[] memory _blobHashes
564:     ) internal pure returns (bytes32[] memory blobAuxOutputWords) {
565:         
566:         
567:         require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10");
568:         require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11");
569: 
570:         
571:         
572:         
573:         
574:         
575:         
576:         
577: 
578:         blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT);
579: 
580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
583:         }
584:     }

```
['[667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667)']
```solidity
625:     function _verifyBlobInformation(
626:         bytes calldata _pubdataCommitments,
627:         bytes32[] memory _blobHashes
628:     ) internal view returns (bytes32[] memory blobCommitments) {
629:         uint256 versionedHashIndex = 0;
630: 
631:         require(_pubdataCommitments.length > 0, "pl");
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
634:         blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);
635: 
636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
638: 
639:             require(blobVersionedHash != bytes32(0), "vh");
640: 
641:             
642:             
643:             bytes32 openingPoint = bytes32(
644:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645:             );
646: 
647:             _pointEvaluationPrecompile(
648:                 blobVersionedHash,
649:                 openingPoint,
650:                 _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE]
651:             );
652: 
653:             
654:             blobCommitments[versionedHashIndex] = keccak256(
655:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656:             );
657:             versionedHashIndex += 1;
658:         }
659: 
660:         
661:         
662:         bytes32 versionedHash = _getBlobVersionedHash(versionedHashIndex);
663:         require(versionedHash == bytes32(0), "lh");
664: 
665:         
666:         
667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND
668:             require(
669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
671:                 "bh"
672:             );
673:         }
674:     }

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226)']
```solidity
222:     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure {
223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
225: 
226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) { // <= FOUND
227:             require(
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229:                 "Wrong factory dep hash"
230:             );
231:         }
232:     }

```
['[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L135-L144)']
```solidity
110:     function verifyCompressedStateDiffs(
111:         uint256 _numberOfStateDiffs,
112:         uint256 _enumerationIndexSize,
113:         bytes calldata _stateDiffs,
114:         bytes calldata _compressedStateDiffs
115:     ) external payable onlyCallFrom(address(L1_MESSENGER_CONTRACT)) returns (bytes32 stateDiffHash) {
116:         
117:         
118:         
119:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large");
120: 
121:         uint256 numberOfInitialWrites = uint256(_compressedStateDiffs.readUint16(0));
122: 
123:         uint256 stateDiffPtr = 2;
124:         uint256 numInitialWritesProcessed = 0;
125: 
126:         
127:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84);
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++; // <= FOUND
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92);
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144:             stateDiffPtr++; // <= FOUND
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }
155: 
156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs");
157: 
158:         
159:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
160:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
161:             uint64 enumIndex = stateDiff.readUint64(84);
162:             if (enumIndex == 0) {
163:                 continue;
164:             }
165: 
166:             uint256 initValue = stateDiff.readUint256(92);
167:             uint256 finalValue = stateDiff.readUint256(124);
168:             uint256 compressedEnumIndex = _sliceToUint256(
169:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize]
170:             );
171:             require(enumIndex == compressedEnumIndex, "rw: enum key mismatch");
172:             stateDiffPtr += _enumerationIndexSize;
173: 
174:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
175:             stateDiffPtr += 1;
176:             uint8 operation = metadata & OPERATION_BITMASK;
177:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
178:             _verifyValueCompression(
179:                 initValue,
180:                 finalValue,
181:                 operation,
182:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
183:             );
184:             stateDiffPtr += len;
185:         }
186: 
187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs");
188: 
189:         stateDiffHash = EfficientCall.keccak(_stateDiffs);
190:     }

```
['[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248-L253)']
```solidity
238:     function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
239:         require(
240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241:             "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:         );
243: 
244:         uint256 deploymentsLength = _deployments.length;
245:         
246:         
247:         uint256 sumOfValues = 0;
248:         for (uint256 i = 0; i < deploymentsLength; ++i) { // <= FOUND
249:             sumOfValues += _deployments[i].value;
250:         }
251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");
252: 
253:         for (uint256 i = 0; i < deploymentsLength; ++i) { // <= FOUND
254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
255:         }
256:     }

```
['[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L109-L109)']
```solidity
94:     function _processL2ToL1Log(L2ToL1Log memory _l2ToL1Log) internal returns (uint256 logIdInMerkleTree) {
95:         bytes32 hashedLog = keccak256(
96:             abi.encodePacked(
97:                 _l2ToL1Log.l2ShardId,
98:                 _l2ToL1Log.isService,
99:                 _l2ToL1Log.txNumberInBlock,
100:                 _l2ToL1Log.sender,
101:                 _l2ToL1Log.key,
102:                 _l2ToL1Log.value
103:             )
104:         );
105: 
106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog));
107: 
108:         logIdInMerkleTree = numberOfLogsToProcess;
109:         numberOfLogsToProcess++; // <= FOUND
110: 
111:         emit L2ToL1LogSent(_l2ToL1Log);
112:     }

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206-L290)']
```solidity
194:     function publishPubdataAndClearState(
195:         bytes calldata _totalL2ToL1PubdataAndStateDiffs
196:     ) external onlyCallFromBootloader {
197:         uint256 calldataPtr = 0;
198: 
199:         
200:         uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
201:         require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs");
202:         calldataPtr += 4;
203: 
204:         bytes32[] memory l2ToL1LogsTreeArray = new bytes32[](L2_TO_L1_LOGS_MERKLE_TREE_LEAVES);
205:         bytes32 reconstructedChainedLogsHash;
206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) { // <= FOUND
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }
214:         require(
215:             reconstructedChainedLogsHash == chainedLogsHash,
216:             "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217:         );
218:         for (uint256 i = numberOfL2ToL1Logs; i < L2_TO_L1_LOGS_MERKLE_TREE_LEAVES; ++i) { // <= FOUND
219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH;
220:         }
221:         uint256 nodesOnCurrentLevel = L2_TO_L1_LOGS_MERKLE_TREE_LEAVES;
222:         while (nodesOnCurrentLevel > 1) {
223:             nodesOnCurrentLevel /= 2;
224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) { // <= FOUND
225:                 l2ToL1LogsTreeArray[i] = keccak256(
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );
228:             }
229:         }
230:         bytes32 l2ToL1LogsTreeRoot = l2ToL1LogsTreeArray[0];
231: 
232:         
233:         uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
234:         calldataPtr += 4;
235:         bytes32 reconstructedChainedMessagesHash;
236:         for (uint256 i = 0; i < numberOfMessages; ++i) { // <= FOUND
237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
238:             calldataPtr += 4;
239:             bytes32 hashedMessage = EfficientCall.keccak(
240:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength]
241:             );
242:             calldataPtr += currentMessageLength;
243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage));
244:         }
245:         require(
246:             reconstructedChainedMessagesHash == chainedMessagesHash,
247:             "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248:         );
249: 
250:         
251:         uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
252:         calldataPtr += 4;
253:         bytes32 reconstructedChainedL1BytecodesRevealDataHash;
254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) { // <= FOUND
255:             uint32 currentBytecodeLength = uint32(
256:                 bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])
257:             );
258:             calldataPtr += 4;
259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260:                 abi.encode(
261:                     reconstructedChainedL1BytecodesRevealDataHash,
262:                     Utils.hashL2Bytecode(
263:                         _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264:                     )
265:                 )
266:             );
267:             calldataPtr += currentBytecodeLength;
268:         }
269:         require(
270:             reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271:             "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272:         );
273: 
274:         
275:         
276:         
277:         
278:         
279:         require(
280:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
281:                 STATE_DIFF_COMPRESSION_VERSION_NUMBER,
282:             "state diff compression version mismatch"
283:         );
284:         calldataPtr++; // <= FOUND
285: 
286:         uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3]));
287:         calldataPtr += 3;
288: 
289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]));
290:         calldataPtr++; // <= FOUND
291: 
292:         bytes calldata compressedStateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
293:             compressedStateDiffSize];
294:         calldataPtr += compressedStateDiffSize;
295: 
296:         bytes calldata totalL2ToL1Pubdata = _totalL2ToL1PubdataAndStateDiffs[:calldataPtr];
297: 
298:         require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long");
299: 
300:         uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]));
301:         calldataPtr += 4;
302: 
303:         bytes calldata stateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr +
304:             (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];
305:         calldataPtr += numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE;
306: 
307:         bytes32 stateDiffHash = COMPRESSOR_CONTRACT.verifyCompressedStateDiffs(
308:             numberOfStateDiffs,
309:             enumerationIndexSize,
310:             stateDiffs,
311:             compressedStateDiffs
312:         );
313: 
314:         
315:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array");
316: 
317:         PUBDATA_CHUNK_PUBLISHER.chunkAndPublishPubdata(totalL2ToL1Pubdata);
318: 
319:         
320:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)), l2ToL1LogsTreeRoot);
321:         SystemContractHelper.toL1(
322:             true,
323:             bytes32(uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)),
324:             EfficientCall.keccak(totalL2ToL1Pubdata)
325:         );
326:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.STATE_DIFF_HASH_KEY)), stateDiffHash);
327: 
328:         
329:         chainedLogsHash = bytes32(0);
330:         numberOfLogsToProcess = 0;
331:         chainedMessagesHash = bytes32(0);
332:         chainedL1BytecodesRevealDataHash = bytes32(0);
333:     }

```
['[36](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36-L36)']
```solidity
21:     function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
22:         require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");
23: 
24:         bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);
25: 
26:         
27:         
28:         bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS);
29: 
30:         assembly {
31:             
32:             let ptr := add(totalBlobs, 0x20)
33:             calldatacopy(ptr, _pubdata.offset, _pubdata.length)
34:         }
35: 
36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND
37:             uint256 start = BLOB_SIZE_BYTES * i;
38: 
39:             
40:             
41:             if (start >= _pubdata.length) {
42:                 break;
43:             }
44: 
45:             bytes32 blobHash;
46:             assembly {
47:                 
48:                 let ptr := add(totalBlobs, 0x20)
49:                 blobHash := keccak256(add(ptr, start), BLOB_SIZE_BYTES)
50:             }
51: 
52:             blobHashes[i] = blobHash;
53:         }
54: 
55:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_ONE_HASH_KEY)), blobHashes[0]);
56:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_TWO_HASH_KEY)), blobHashes[1]);
57:     }

```


</details>

## [Gas-14] Use byte32 in place of string

### Resolution 
For strings of 32 char strings and below you can use bytes32 instead as it's more gas efficient

Num of instances: 10

### Findings 


<details><summary>Click to show findings</summary>

['[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26-L27)']
```solidity
26:     
27:     string public constant override getName = "ValidatorTimelock"; // <= FOUND

```
['[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20-L21)']
```solidity
20:     
21:     string public constant override getName = "AdminFacet"; // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27-L28)']
```solidity
27:     
28:     string public constant override getName = "ExecutorFacet"; // <= FOUND

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25-L26)']
```solidity
25:     
26:     string public constant override getName = "GettersFacet"; // <= FOUND

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35-L36)']
```solidity
35:     
36:     string public constant override getName = "MailboxFacet"; // <= FOUND

```
['[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26-L26)']
```solidity
26: string public constant override getName = "ValidatorTimelock"; // <= FOUND

```
['[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20-L20)']
```solidity
20: string public constant override getName = "AdminFacet"; // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27-L27)']
```solidity
27: string public constant override getName = "ExecutorFacet"; // <= FOUND

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25-L25)']
```solidity
25: string public constant override getName = "GettersFacet"; // <= FOUND

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35-L35)']
```solidity
35: string public constant override getName = "MailboxFacet"; // <= FOUND

```


</details>

## [Gas-15] Default bool values are manually reset

### Resolution 
Using .delete is better than resetting a Solidity variable to its default value manually because it frees up storage space on the Ethereum blockchain, resulting in gas cost savings. 

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92-L97)']
```solidity
92:     function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner { // <= FOUND
93:         require(
94:             stateTransitionManagerIsRegistered[_stateTransitionManager],
95:             "Bridgehub: state transition not registered yet"
96:         );
97:         stateTransitionManagerIsRegistered[_stateTransitionManager] = false; // <= FOUND
98:     }

```
['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L87-L91)']
```solidity
87:     function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) { // <= FOUND
88:         if (!validators[_chainId][_validator]) {
89:             revert ValidatorDoesNotExist(_chainId);
90:         }
91:         validators[_chainId][_validator] = false; // <= FOUND
92:         emit ValidatorRemoved(_chainId, _validator);
93:     }

```
['[143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L143-L147)']
```solidity
143:     function unfreezeDiamond() external onlyAdminOrStateTransitionManager { // <= FOUND
144:         Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
145: 
146:         require(diamondStorage.isFrozen, "a7"); 
147:         diamondStorage.isFrozen = false; // <= FOUND
148: 
149:         emit Unfreeze();
150:     }

```


</details>

## [Gas-16] Default int values are manually reset

### Resolution 
Using .delete is better than resetting a Solidity variable to its default value manually because it frees up storage space on the Ethereum blockchain, resulting in gas cost savings.

Num of instances: 33

### Findings 


<details><summary>Click to show findings</summary>

['[276](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L276-L276)']
```solidity
276:                 baseTokenMsgValue = 0; // <= FOUND

```
['[330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L330-L330)']
```solidity
330:         numberOfLogsToProcess = 0; // <= FOUND

```
['[487](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L487-L487)']
```solidity
487:         txNumberInBlock = 0; // <= FOUND

```
['[629](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629-L629)']
```solidity
629:         uint256 versionedHashIndex = 0; // <= FOUND

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L92-L92)']
```solidity
92:         uint256 costForPubdata = 0; // <= FOUND

```
['[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L124-L124)']
```solidity
124:         uint256 numInitialWritesProcessed = 0; // <= FOUND

```
['[247](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L247-L249)']
```solidity
247:         
248:         
249:         uint256 sumOfValues = 0; // <= FOUND

```
['[197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L197-L197)']
```solidity
197:         uint256 calldataPtr = 0; // <= FOUND

```
['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L225)']
```solidity
225:         for (uint256 i = 0; i < _calls.length; ++i) { // <= FOUND

```
['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116-L116)']
```solidity
116:             for (uint256 i = 0; i < _newBatchesData.length; ++i) { // <= FOUND

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L143)']
```solidity
142:         
143:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) { // <= FOUND

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257)']
```solidity
257:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) { // <= FOUND

```
['[311](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311-L311)']
```solidity
311:         for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) { // <= FOUND

```
['[351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351-L351)']
```solidity
351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) { // <= FOUND

```
['[405](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405-L405)']
```solidity
405:         for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) { // <= FOUND

```
['[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580)']
```solidity
580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND

```
['[636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636)']
```solidity
636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) { // <= FOUND

```
['[667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L669)']
```solidity
667:         
668:         
669:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208-L208)']
```solidity
208:         for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) { // <= FOUND

```
['[356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356-L356)']
```solidity
356:         for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) { // <= FOUND

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226)']
```solidity
226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) { // <= FOUND

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101-L101)']
```solidity
101:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) { // <= FOUND

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138-L138)']
```solidity
138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) { // <= FOUND

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61-L61)']
```solidity
61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) { // <= FOUND

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127-L128)']
```solidity
127:         
128:         for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) { // <= FOUND

```
['[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248-L248)']
```solidity
248:         for (uint256 i = 0; i < deploymentsLength; ++i) { // <= FOUND

```
['[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38-L38)']
```solidity
38:             for (uint256 i = 0; i < immutablesLength; ++i) { // <= FOUND

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L30-L30)']
```solidity
30:             for (uint256 i = 0; i < hashesLen; ++i) { // <= FOUND

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206-L206)']
```solidity
206:         for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) { // <= FOUND

```
['[224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224-L224)']
```solidity
224:             for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) { // <= FOUND

```
['[236](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L236-L236)']
```solidity
236:         for (uint256 i = 0; i < numberOfMessages; ++i) { // <= FOUND

```
['[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L254-L254)']
```solidity
254:         for (uint256 i = 0; i < numberOfBytecodes; ++i) { // <= FOUND

```
['[667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667)']
```solidity
667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND

```


</details>

## [Gas-17] Use assembly to check for the zero address

### Resolution 

Using assembly for address comparisons in Solidity can save gas because it allows for more direct access to the Ethereum Virtual Machine (EVM), reducing the overhead of higher-level operations. Solidity's high-level abstraction simplifies coding but can introduce additional gas costs. Using assembly for simple operations like address comparisons can be more gas-efficient.

Num of instances: 25

### Findings 


<details><summary>Click to show findings</summary>

['[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L104-L108)']
```solidity
104:     function initialize(
105:         address _owner,
106:         uint256 _eraFirstPostUpgradeBatch
107:     ) external reentrancyGuardInitializer initializer {
108:         require(_owner != address(0), "ShB owner 0"); // <= FOUND
109:         _transferOwnership(_owner);
110: 
111:         eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch;
112:         l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS;
113:     }

```
['[182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L182-L188)']
```solidity
182:     function bridgehubDeposit(
183:         uint256 _chainId,
184:         address _prevMsgSender,
185:         uint256, 
186:         bytes calldata _data
187:     ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed"); // <= FOUND
189: 
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
191:             _data,
192:             (address, uint256, address)
193:         );
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
196: 
197:         uint256 amount;
198:         if (_l1Token == ETH_TOKEN_ADDRESS) {
199:             amount = msg.value;
200:             require(_depositAmount == 0, "ShB wrong withdraw amount");
201:         } else {
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
203:             amount = _depositAmount;
204: 
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); 
207:         }
208:         require(amount != 0, "6T"); 
209: 
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
211:         if (!hyperbridgingEnabled[_chainId]) {
212:             chainBalance[_chainId][_l1Token] += amount;
213:         }
214: 
215:         {
216:             
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);
218: 
219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });
226:         }
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
228:     }

```
['[554](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554-L578)']
```solidity
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep"); // <= FOUND
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             
575:             
576:             
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) { // <= FOUND
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, 
588:                 l2Value: 0, 
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

```
['[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L132)']
```solidity
114:     function createNewChain(
115:         uint256 _chainId,
116:         address _stateTransitionManager,
117:         address _baseToken,
118:         uint256, 
119:         address _admin,
120:         bytes calldata _initData
121:     ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");
123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
124: 
125:         require(
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         );
129:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set"); // <= FOUND
131: 
132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered"); // <= FOUND
133: 
134:         stateTransitionManager[_chainId] = _stateTransitionManager;
135:         baseToken[_chainId] = _baseToken;
136: 
137:         IStateTransitionManager(_stateTransitionManager).createNewChain(
138:             _chainId,
139:             _baseToken,
140:             address(sharedBridge),
141:             _admin,
142:             _initData
143:         );
144: 
145:         emit NewChain(_chainId, _stateTransitionManager, _admin);
146:         return _chainId;
147:     }

```
['[325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L325-L326)']
```solidity
325:     function _actualRefundRecipient(address _refundRecipient) internal view returns (address _recipient) {
326:         if (_refundRecipient == address(0)) { // <= FOUND
327:             
328:             _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender);
329:         } else if (_refundRecipient.code.length > 0) {
330:             
331:             _recipient = AddressAliasHelper.applyL1ToL2Alias(_refundRecipient);
332:         } else {
333:             _recipient = _refundRecipient;
334:         }
335:     }

```
['[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L79-L82)']
```solidity
79:     function initialize(
80:         StateTransitionManagerInitializeData calldata _initializeData
81:     ) external reentrancyGuardInitializer {
82:         require(_initializeData.governor != address(0), "StateTransition: governor zero"); // <= FOUND
83:         _transferOwnership(_initializeData.governor);
84: 
85:         genesisUpgrade = _initializeData.genesisUpgrade;
86:         protocolVersion = _initializeData.protocolVersion;
87:         validatorTimelock = _initializeData.validatorTimelock;
88: 
89:         
90:         IExecutor.StoredBatchInfo memory batchZero = IExecutor.StoredBatchInfo(
91:             0,
92:             _initializeData.genesisBatchHash,
93:             _initializeData.genesisIndexRepeatedStorageChanges,
94:             0,
95:             EMPTY_STRING_KECCAK,
96:             DEFAULT_L2_LOGS_TREE_ROOT_HASH,
97:             0,
98:             _initializeData.genesisBatchCommitment
99:         );
100:         storedBatchZero = keccak256(abi.encode(batchZero));
101: 
102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut));
103: 
104:         
105:         
106:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
107:     }

```
['[239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L239-L246)']
```solidity
239:     function createNewChain(
240:         uint256 _chainId,
241:         address _baseToken,
242:         address _sharedBridge,
243:         address _admin,
244:         bytes calldata _diamondCut
245:     ) external onlyBridgehub {
246:         if (stateTransition[_chainId] != address(0)) { // <= FOUND
247:             
248:             return;
249:         }
250: 
251:         
252:         Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));
253: 
254:         
255:         bytes32 cutHashInput = keccak256(_diamondCut);
256:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
257: 
258:         
259:         bytes memory initData;
260:         
261:         initData = bytes.concat(
262:             IDiamondInit.initialize.selector,
263:             bytes32(_chainId),
264:             bytes32(uint256(uint160(bridgehub))),
265:             bytes32(uint256(uint160(address(this)))),
266:             bytes32(uint256(protocolVersion)),
267:             bytes32(uint256(uint160(_admin))),
268:             bytes32(uint256(uint160(validatorTimelock))),
269:             bytes32(uint256(uint160(_baseToken))),
270:             bytes32(uint256(uint160(_sharedBridge))),
271:             bytes32(storedBatchZero),
272:             diamondCut.initCalldata
273:         );
274: 
275:         diamondCut.initCalldata = initData;
276:         
277:         DiamondProxy stateTransitionContract = new DiamondProxy{salt: bytes32(0)}(block.chainid, diamondCut);
278: 
279:         
280:         address stateTransitionAddress = address(stateTransitionContract);
281: 
282:         stateTransition[_chainId] = stateTransitionAddress;
283: 
284:         
285:         _setChainIdUpgrade(_chainId, stateTransitionAddress);
286: 
287:         emit StateTransitionNewChain(_chainId, stateTransitionAddress);
288:     }

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L24-L27)']
```solidity
24:     function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32) {
25:         require(address(_initializeData.verifier) != address(0), "vt"); // <= FOUND
26:         require(_initializeData.admin != address(0), "vy"); // <= FOUND
27:         require(_initializeData.validatorTimelock != address(0), "hc"); // <= FOUND
28:         require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");
29: 
30:         s.chainId = _initializeData.chainId;
31:         s.bridgehub = _initializeData.bridgehub;
32:         s.stateTransitionManager = _initializeData.stateTransitionManager;
33:         s.baseToken = _initializeData.baseToken;
34:         s.baseTokenBridge = _initializeData.baseTokenBridge;
35:         s.protocolVersion = _initializeData.protocolVersion;
36: 
37:         s.verifier = _initializeData.verifier;
38:         s.admin = _initializeData.admin;
39:         s.validators[_initializeData.validatorTimelock] = true;
40: 
41:         s.storedBatchHashes[0] = _initializeData.storedBatchZero;
42:         s.verifierParams = _initializeData.verifierParams;
43:         s.l2BootloaderBytecodeHash = _initializeData.l2BootloaderBytecodeHash;
44:         s.l2DefaultAccountBytecodeHash = _initializeData.l2DefaultAccountBytecodeHash;
45:         s.priorityTxMaxGasLimit = _initializeData.priorityTxMaxGasLimit;
46:         s.feeParams = _initializeData.feeParams;
47:         s.blobVersionedHashRetriever = _initializeData.blobVersionedHashRetriever;
48: 
49:         
50:         
51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
52: 
53:         return Diamond.DIAMOND_INIT_SUCCESS_RETURN_VALUE;
54:     }

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L181-L183)']
```solidity
181:     function isFunctionFreezable(bytes4 _selector) external view returns (bool) {
182:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();
183:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2"); // <= FOUND
184:         return ds.selectorToFacet[_selector].isFreezable;
185:     }

```
['[258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L275)']
```solidity
258:     function _requestL2Transaction(
259:         uint256 _mintValue,
260:         WritePriorityOpParams memory _params,
261:         bytes memory _calldata,
262:         bytes[] memory _factoryDeps
263:     ) internal returns (bytes32 canonicalTxHash) {
264:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");
265:         _params.txId = s.priorityQueue.getTotalPriorityTxs();
266: 
267:         
268:         
269: 
270:         _params.l2GasPrice = _deriveL2GasPrice(tx.gasprice, _params.l2GasPricePerPubdata);
271:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
272:         require(_mintValue >= baseCost + _params.l2Value, "mv"); 
273: 
274:         
275:         address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient; // <= FOUND
276:         
277:         if (refundRecipient.code.length > 0) {
278:             refundRecipient = AddressAliasHelper.applyL1ToL2Alias(refundRecipient);
279:         }
280:         _params.refundRecipient = refundRecipient;
281: 
282:         
283:         _params.expirationTimestamp = uint64(block.timestamp + PRIORITY_EXPIRATION); 
284:         _params.valueToMint = _mintValue;
285: 
286:         canonicalTxHash = _writePriorityOp(_params, _calldata, _factoryDeps);
287:     }

```
['[126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126-L141)']
```solidity
126:     function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
127:         DiamondStorage storage ds = getDiamondStorage();
128: 
129:         
130:         
131:         
132:         require(_facet.code.length > 0, "G");
133: 
134:         
135:         _saveFacetIfNew(_facet);
136: 
137:         uint256 selectorsLength = _selectors.length;
138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
139:             bytes4 selector = _selectors[i];
140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
141:             require(oldFacet.facetAddress == address(0), "J");  // <= FOUND
142: 
143:             _addOneFunction(_facet, selector, _isFacetFreezable);
144:         }
145:     }

```
['[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149-L161)']
```solidity
149:     function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
150:         DiamondStorage storage ds = getDiamondStorage();
151: 
152:         
153:         
154:         
155:         require(_facet.code.length > 0, "K");
156: 
157:         uint256 selectorsLength = _selectors.length;
158:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
159:             bytes4 selector = _selectors[i];
160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:             require(oldFacet.facetAddress != address(0), "L");  // <= FOUND
162: 
163:             _removeOneFunction(oldFacet.facetAddress, selector);
164:             
165:             _saveFacetIfNew(_facet);
166:             _addOneFunction(_facet, selector, _isFacetFreezable);
167:         }
168:     }

```
['[172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172-L181)']
```solidity
172:     function _removeFunctions(address _facet, bytes4[] memory _selectors) private {
173:         DiamondStorage storage ds = getDiamondStorage();
174: 
175:         require(_facet == address(0), "a1");  // <= FOUND
176: 
177:         uint256 selectorsLength = _selectors.length;
178:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
179:             bytes4 selector = _selectors[i];
180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
181:             require(oldFacet.facetAddress != address(0), "a2");  // <= FOUND
182: 
183:             _removeOneFunction(oldFacet.facetAddress, selector);
184:         }
185:     }

```
['[405](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L405-L406)']
```solidity
405:     function totalRequiredBalance(Transaction calldata _transaction) internal pure returns (uint256 requiredBalance) {
406:         if (address(uint160(_transaction.paymaster)) != address(0)) { // <= FOUND
407:             
408:             requiredBalance = _transaction.value;
409:         } else {
410:             
411:             requiredBalance = _transaction.maxFeePerGas * _transaction.gasLimit + _transaction.value;
412:         }
413:     }

```
['[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L49-L68)']
```solidity
49:     function initialize(
50:         address _l1Bridge,
51:         address _l1LegecyBridge,
52:         bytes32 _l2TokenProxyBytecodeHash,
53:         address _aliasedOwner
54:     ) external reinitializer(2) {
55:         require(_l1Bridge != address(0), "bf"); // <= FOUND
56:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
57:         require(_aliasedOwner != address(0), "sf"); // <= FOUND
58:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
59: 
60:         l1Bridge = _l1Bridge;
61:         l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;
62: 
63:         if (block.chainid != ERA_CHAIN_ID) {
64:             address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
65:             l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
66:             l2TokenBeacon.transferOwnership(_aliasedOwner);
67:         } else {
68:             require(_l1LegecyBridge != address(0), "bf2"); // <= FOUND
69:             
70:         }
71:     }

```
['[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L79-L96)']
```solidity
79:     function finalizeDeposit(
80:         address _l1Sender,
81:         address _l2Receiver,
82:         address _l1Token,
83:         uint256 _amount,
84:         bytes calldata _data
85:     ) external payable override {
86:         
87:         require(
88:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90:             "mq"
91:         );
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");
93: 
94:         address expectedL2Token = l2TokenAddress(_l1Token);
95:         address currentL1Token = l1TokenAddress[expectedL2Token];
96:         if (currentL1Token == address(0)) { // <= FOUND
97:             address deployedToken = _deployL2Token(_l1Token, _data);
98:             require(deployedToken == expectedL2Token, "mt");
99:             l1TokenAddress[expectedL2Token] = _l1Token;
100:         } else {
101:             require(currentL1Token == _l1Token, "gg"); 
102:         }
103: 
104:         IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);
105:         emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);
106:     }

```
['[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L123-L129)']
```solidity
123:     function withdraw(address _l1Receiver, address _l2Token, uint256 _amount) external override {
124:         require(_amount > 0, "Amount cannot be zero");
125: 
126:         IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);
127: 
128:         address l1Token = l1TokenAddress[_l2Token];
129:         require(l1Token != address(0), "yh"); // <= FOUND
130: 
131:         bytes memory message = _getL1WithdrawMessage(_l1Receiver, l1Token, _amount);
132:         L2ContractHelper.sendMessageToL1(message);
133: 
134:         emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
135:     }

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L50-L51)']
```solidity
50:     function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {
51:         require(_l1Address != address(0), "in6");  // <= FOUND
52:         l1Address = _l1Address;
53: 
54:         l2Bridge = msg.sender;
55: 
56:         
57:         (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(
58:             _data,
59:             (bytes, bytes, bytes)
60:         );
61: 
62:         ERC20Getters memory getters;
63:         string memory decodedName;
64:         string memory decodedSymbol;
65: 
66:         
67:         
68: 
69:         
70:         
71:         
72:         
73:         
74: 
75:         try this.decodeString(nameBytes) returns (string memory nameString) {
76:             decodedName = nameString;
77:         } catch {
78:             getters.ignoreName = true;
79:         }
80: 
81:         try this.decodeString(symbolBytes) returns (string memory symbolString) {
82:             decodedSymbol = symbolString;
83:         } catch {
84:             getters.ignoreSymbol = true;
85:         }
86: 
87:         
88:         __ERC20_init_unchained(decodedName, decodedSymbol);
89: 
90:         
91:         __ERC20Permit_init(decodedName);
92: 
93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
94:             
95:             decimals_ = decimalsUint8;
96:         } catch {
97:             getters.ignoreDecimals = true;
98:         }
99: 

```
['[232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L232-L237)']
```solidity
232:     function bridgehubConfirmL2Transaction(
233:         uint256 _chainId,
234:         bytes32 _txDataHash,
235:         bytes32 _txHash
236:     ) external override onlyBridgehub {
237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap"); // <= FOUND
238:         depositHappened[_chainId][_txHash] = _txDataHash;
239:         emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash);
240:     }

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L32-L50)']
```solidity
32:     function _commitOneBatch(
33:         StoredBatchInfo memory _previousBatch,
34:         CommitBatchInfo calldata _newBatch,
35:         bytes32 _expectedSystemContractUpgradeTxHash
36:     ) internal view returns (StoredBatchInfo memory) {
37:         require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f"); 
38: 
39:         uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));
40:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");
41: 
42:         
43:         
44:         LogProcessingOutput memory logOutput = _processL2Logs(_newBatch, _expectedSystemContractUpgradeTxHash);
45: 
46:         bytes32[] memory blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);
47:         bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);
48:         if (s.feeParams.pubdataPricingMode == PubdataPricingMode.Validium) {
49:             
50:             require(logOutput.pubdataHash == 0x00, "v0h"); // <= FOUND
51:             require(_newBatch.pubdataCommitments.length == 1);
52:         } else if (pubdataSource == uint8(PubdataSource.Blob)) {
53:             
54:             
55:             blobHashes[0] = logOutput.blob1Hash;
56:             blobHashes[1] = logOutput.blob2Hash;
57:             
58:             blobCommitments = _verifyBlobInformation(_newBatch.pubdataCommitments[1:], blobHashes);
59:         } else if (pubdataSource == uint8(PubdataSource.Calldata)) {
60:             
61:             require(
62:                 logOutput.pubdataHash ==
63:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
64:                 "wp"
65:             );
66:             blobHashes[0] = logOutput.blob1Hash;
67:             blobCommitments[0] = bytes32(
68:                 _newBatch.pubdataCommitments[_newBatch.pubdataCommitments.length - 32:_newBatch
69:                     .pubdataCommitments
70:                     .length]
71:             );
72:         }
73: 
74:         require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");
75:         
76:         require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");
77:         
78:         require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");
79: 
80:         
81:         _verifyBatchTimestamp(logOutput.packedBatchAndL2BlockTimestamp, _newBatch.timestamp, _previousBatch.timestamp);

```
['[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L89-L102)']
```solidity
89:     function getCodeHash(uint256 _input) external view override returns (bytes32) {
90:         
91:         
92:         address account = address(uint160(_input));
93:         if (uint160(account) <= CURRENT_MAX_PRECOMPILE_ADDRESS) {
94:             return EMPTY_STRING_KECCAK;
95:         }
96: 
97:         bytes32 codeHash = getRawCodeHash(account);
98: 
99:         
100:         
101:         
102:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) { // <= FOUND
103:             codeHash = EMPTY_STRING_KECCAK;
104:         }
105:         
106:         
107:         else if (Utils.isContractConstructing(codeHash)) {
108:             codeHash = EMPTY_STRING_KECCAK;
109:         }
110: 
111:         return codeHash;
112:     }

```
['[117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L117-L133)']
```solidity
117:     function getCodeSize(uint256 _input) external view override returns (uint256 codeSize) {
118:         
119:         
120:         address account = address(uint160(_input));
121:         bytes32 codeHash = getRawCodeHash(account);
122: 
123:         
124:         
125:         
126:         
127:         
128:         
129:         
130:         
131:         if (
132:             uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS &&
133:             codeHash != 0x00 && // <= FOUND
134:             !Utils.isContractConstructing(codeHash)
135:         ) {
136:             codeSize = Utils.bytecodeLenInBytes(codeHash);
137:         }
138:     }

```
['[258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L258-L273)']
```solidity
258:     function _nonSystemDeployOnAddress(
259:         bytes32 _bytecodeHash,
260:         address _newAddress,
261:         AccountAbstractionVersion _aaVersion,
262:         bytes calldata _input
263:     ) internal {
264:         require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");
265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space");
266: 
267:         
268:         require(
269:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0, // <= FOUND
270:             "Code hash is non-zero"
271:         );
272:         
273:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied"); // <= FOUND
274: 
275:         _performDeployOnAddress(_bytecodeHash, _newAddress, _aaVersion, _input);
276:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L51-L52)']
```solidity
51:     function isContractConstructed(bytes32 _bytecodeHash) internal pure returns (bool) {
52:         return _bytecodeHash[1] == 0x00; // <= FOUND
53:     }

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L56-L57)']
```solidity
56:     function isContractConstructing(bytes32 _bytecodeHash) internal pure returns (bool) {
57:         return _bytecodeHash[1] == 0x01; // <= FOUND
58:     }

```


</details>

## [Gas-18] Some error strings are not descriptive

### Resolution 
Consider adding more detail to these error strings

Num of instances: 54

### Findings 


<details><summary>Click to show findings</summary>

['[141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141-L143)']
```solidity
133:     function deposit(
134:         address _l2Receiver,
135:         address _l1Token,
136:         uint256 _amount,
137:         uint256 _l2TxGasLimit,
138:         uint256 _l2TxGasPerPubdataByte,
139:         address _refundRecipient
140:     ) public payable nonReentrant returns (bytes32 l2TxHash) {
141:         require(_amount != 0, "0T");  // <= FOUND
142:         uint256 amount = _depositFundsToSharedBridge(msg.sender, IERC20(_l1Token), _amount);
143:         require(amount == _amount, "3T");  // <= FOUND
144: 
145:         l2TxHash = sharedBridge.depositLegacyErc20Bridge{value: msg.value}(
146:             msg.sender,
147:             _l2Receiver,
148:             _l1Token,
149:             _amount,
150:             _l2TxGasLimit,
151:             _l2TxGasPerPubdataByte,
152:             _refundRecipient
153:         );
154:         depositAmount[msg.sender][_l1Token][l2TxHash] = _amount;
155:         emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount);
156:     }

```
['[161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161-L161)']
```solidity
148:     function bridgehubDepositBaseToken(
149:         uint256 _chainId,
150:         address _prevMsgSender,
151:         address _l1Token,
152:         uint256 _amount
153:     ) external payable virtual onlyBridgehubOrEra(_chainId) {
154:         if (_l1Token == ETH_TOKEN_ADDRESS) {
155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");
156:         } else {
157:             
158:             require(msg.value == 0, "ShB m.v > 0 b d.it");
159: 
160:             uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount); 
161:             require(amount == _amount, "3T");  // <= FOUND
162:         }
163: 
164:         if (!hyperbridgingEnabled[_chainId]) {
165:             chainBalance[_chainId][_l1Token] += _amount;
166:         }
167:         
168:         emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);
169:     }

```
['[186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186-L186)']
```solidity
176:     function claimFailedDeposit(
177:         address _depositSender,
178:         address _l1Token,
179:         bytes32 _l2TxHash,
180:         uint256 _l2BatchNumber,
181:         uint256 _l2MessageIndex,
182:         uint16 _l2TxNumberInBatch,
183:         bytes32[] calldata _merkleProof
184:     ) external nonReentrant {
185:         uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash];
186:         require(amount != 0, "2T");  // <= FOUND
187:         delete depositAmount[_depositSender][_l1Token][_l2TxHash];
188: 
189:         sharedBridge.claimFailedDepositLegacyErc20Bridge(
190:             _depositSender,
191:             _l1Token,
192:             amount,
193:             _l2TxHash,
194:             _l2BatchNumber,
195:             _l2MessageIndex,
196:             _l2TxNumberInBatch,
197:             _merkleProof
198:         );
199:         emit ClaimedFailedDeposit(_depositSender, _l1Token, amount);
200:     }

```
['[215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215-L215)']
```solidity
208:     function finalizeWithdrawal(
209:         uint256 _l2BatchNumber,
210:         uint256 _l2MessageIndex,
211:         uint16 _l2TxNumberInBatch,
212:         bytes calldata _message,
213:         bytes32[] calldata _merkleProof
214:     ) external nonReentrant {
215:         require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw"); // <= FOUND
216:         
217: 
218:         (address l1Receiver, address l1Token, uint256 amount) = sharedBridge.finalizeWithdrawalLegacyErc20Bridge(
219:             _l2BatchNumber,
220:             _l2MessageIndex,
221:             _l2TxNumberInBatch,
222:             _message,
223:             _merkleProof
224:         );
225:         emit WithdrawalFinalized(l1Receiver, l1Token, amount);
226:     }

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206-L206)']
```solidity
182:     function bridgehubDeposit(
183:         uint256 _chainId,
184:         address _prevMsgSender,
185:         uint256, 
186:         bytes calldata _data
187:     ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
189: 
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
191:             _data,
192:             (address, uint256, address)
193:         );
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
196: 
197:         uint256 amount;
198:         if (_l1Token == ETH_TOKEN_ADDRESS) {
199:             amount = msg.value;
200:             require(_depositAmount == 0, "ShB wrong withdraw amount");
201:         } else {
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
203:             amount = _depositAmount;
204: 
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T");  // <= FOUND
207:         }
208:         require(amount != 0, "6T"); 
209: 
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
211:         if (!hyperbridgingEnabled[_chainId]) {
212:             chainBalance[_chainId][_l1Token] += amount;
213:         }
214: 
215:         {
216:             
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);
218: 
219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });
226:         }
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
228:     }

```
['[325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L325-L325)']
```solidity
303:     function _claimFailedDeposit(
304:         bool _checkedInLegacyBridge,
305:         uint256 _chainId,
306:         address _depositSender,
307:         address _l1Token,
308:         uint256 _amount,
309:         bytes32 _l2TxHash,
310:         uint256 _l2BatchNumber,
311:         uint256 _l2MessageIndex,
312:         uint16 _l2TxNumberInBatch,
313:         bytes32[] calldata _merkleProof
314:     ) internal nonReentrant {
315:         {
316:             bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
317:                 _chainId,
318:                 _l2TxHash,
319:                 _l2BatchNumber,
320:                 _l2MessageIndex,
321:                 _l2TxNumberInBatch,
322:                 _merkleProof,
323:                 TxStatus.Failure
324:             );
325:             require(proofValid, "yn"); // <= FOUND
326:         }
327:         require(_amount > 0, "y1");
328: 
329:         {
330:             bool notCheckedInLegacyBridgeOrWeCanCheckDeposit;
331:             {
332:                 
333:                 bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);
334:                 
335:                 
336:                 
337:                 notCheckedInLegacyBridgeOrWeCanCheckDeposit = (!_checkedInLegacyBridge) || weCanCheckDepositHere;
338:             }
339:             if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
342:                 require(dataHash == txDataHash, "ShB: d.it not hap");
343:                 delete depositHappened[_chainId][_l2TxHash];
344:             }
345:         }
346: 
347:         if (!hyperbridgingEnabled[_chainId]) {
348:             
349:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
350:             chainBalance[_chainId][_l1Token] -= _amount;
351:         }
352: 
353:         
354:         if (_l1Token == ETH_TOKEN_ADDRESS) {
355:             bool callSuccess;
356:             
357:             assembly {
358:                 callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)
359:             }
360:             require(callSuccess, "ShB: claimFailedDeposit failed");
361:         } else {
362:             IERC20(_l1Token).safeTransfer(_depositSender, _amount);
363:             
364:             
365:         }
366: 
367:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);
368:     }

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62-L62)']
```solidity
60:     function acceptAdmin() external {
61:         address currentPendingAdmin = pendingAdmin;
62:         require(msg.sender == currentPendingAdmin, "n42");  // <= FOUND
63: 
64:         address previousAdmin = admin;
65:         admin = currentPendingAdmin;
66:         delete pendingAdmin;
67: 
68:         emit NewPendingAdmin(currentPendingAdmin, address(0));
69:         emit NewAdmin(previousAdmin, pendingAdmin);
70:     }

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62-L62)']
```solidity
60:     function acceptAdmin() external {
61:         address currentPendingAdmin = pendingAdmin;
62:         require(msg.sender == currentPendingAdmin, "n42");  // <= FOUND
63: 
64:         address previousAdmin = admin;
65:         admin = currentPendingAdmin;
66:         delete pendingAdmin;
67: 
68:         emit NewPendingAdmin(currentPendingAdmin, address(0));
69:         emit NewAdmin(previousAdmin, pendingAdmin);
70:     }

```
['[195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195-L195)']
```solidity
182:     function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
183:         uint256 delay = executionDelay; 
184:         unchecked {
185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
187:                     _newBatchesData[i].batchNumber
188:                 );
189: 
190:                 
191:                 
192:                 
193:                 
194: 
195:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c");  // <= FOUND
196:             }
197:         }
198:         _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
199:     }

```
['[217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L217-L217)']
```solidity
203:     function executeBatchesSharedBridge(
204:         uint256 _chainId,
205:         StoredBatchInfo[] calldata _newBatchesData
206:     ) external onlyValidator(_chainId) {
207:         uint256 delay = executionDelay; 
208:         unchecked {
209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
211: 
212:                 
213:                 
214:                 
215:                 
216: 
217:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c");  // <= FOUND
218:             }
219:         }
220:         _propagateToZkSyncStateTransition(_chainId);
221:     }

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25-L25)']
```solidity
24:     function initialize(InitializeData calldata _initializeData) external reentrancyGuardInitializer returns (bytes32) {
25:         require(address(_initializeData.verifier) != address(0), "vt"); // <= FOUND
26:         require(_initializeData.admin != address(0), "vy");
27:         require(_initializeData.validatorTimelock != address(0), "hc");
28:         require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu");
29: 
30:         s.chainId = _initializeData.chainId;
31:         s.bridgehub = _initializeData.bridgehub;
32:         s.stateTransitionManager = _initializeData.stateTransitionManager;
33:         s.baseToken = _initializeData.baseToken;
34:         s.baseTokenBridge = _initializeData.baseTokenBridge;
35:         s.protocolVersion = _initializeData.protocolVersion;
36: 
37:         s.verifier = _initializeData.verifier;
38:         s.admin = _initializeData.admin;
39:         s.validators[_initializeData.validatorTimelock] = true;
40: 
41:         s.storedBatchHashes[0] = _initializeData.storedBatchZero;
42:         s.verifierParams = _initializeData.verifierParams;
43:         s.l2BootloaderBytecodeHash = _initializeData.l2BootloaderBytecodeHash;
44:         s.l2DefaultAccountBytecodeHash = _initializeData.l2DefaultAccountBytecodeHash;
45:         s.priorityTxMaxGasLimit = _initializeData.priorityTxMaxGasLimit;
46:         s.feeParams = _initializeData.feeParams;
47:         s.blobVersionedHashRetriever = _initializeData.blobVersionedHashRetriever;
48: 
49:         
50:         
51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
52: 
53:         return Diamond.DIAMOND_INIT_SUCCESS_RETURN_VALUE;
54:     }

```
['[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34-L34)']
```solidity
32:     function acceptAdmin() external {
33:         address pendingAdmin = s.pendingAdmin;
34:         require(msg.sender == pendingAdmin, "n4");  // <= FOUND
35: 
36:         address previousAdmin = s.admin;
37:         s.admin = pendingAdmin;
38:         delete s.pendingAdmin;
39: 
40:         emit NewPendingAdmin(pendingAdmin, address(0));
41:         emit NewAdmin(previousAdmin, pendingAdmin);
42:     }

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59-L59)']
```solidity
58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {
59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5"); // <= FOUND
60: 
61:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;
62:         s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
64:     }

```
['[70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L70-L70)']
```solidity
67:     function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
68:         
69:         
70:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6"); // <= FOUND
71: 
72:         FeeParams memory oldFeeParams = s.feeParams;
73:         s.feeParams = _newFeeParams;
74: 
75:         emit NewFeeParams(oldFeeParams, _newFeeParams);
76:     }

```
['[136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L136-L136)']
```solidity
133:     function freezeDiamond() external onlyAdminOrStateTransitionManager {
134:         Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
135: 
136:         require(!diamondStorage.isFrozen, "a9");  // <= FOUND
137:         diamondStorage.isFrozen = true;
138: 
139:         emit Freeze();
140:     }

```
['[146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146-L146)']
```solidity
143:     function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
144:         Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
145: 
146:         require(diamondStorage.isFrozen, "a7");  // <= FOUND
147:         diamondStorage.isFrozen = false;
148: 
149:         emit Unfreeze();
150:     }

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37-L37)']
```solidity
32:     function _commitOneBatch(
33:         StoredBatchInfo memory _previousBatch,
34:         CommitBatchInfo calldata _newBatch,
35:         bytes32 _expectedSystemContractUpgradeTxHash
36:     ) internal view returns (StoredBatchInfo memory) {
37:         require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f");  // <= FOUND
38: 
39:         uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0]));
40:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us");
41: 
42:         
43:         
44:         LogProcessingOutput memory logOutput = _processL2Logs(_newBatch, _expectedSystemContractUpgradeTxHash);
45: 
46:         bytes32[] memory blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);
47:         bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);
48:         if (s.feeParams.pubdataPricingMode == PubdataPricingMode.Validium) {
49:             
50:             require(logOutput.pubdataHash == 0x00, "v0h");
51:             require(_newBatch.pubdataCommitments.length == 1);
52:         } else if (pubdataSource == uint8(PubdataSource.Blob)) {
53:             
54:             
55:             blobHashes[0] = logOutput.blob1Hash;
56:             blobHashes[1] = logOutput.blob2Hash;
57:             
58:             blobCommitments = _verifyBlobInformation(_newBatch.pubdataCommitments[1:], blobHashes);
59:         } else if (pubdataSource == uint8(PubdataSource.Calldata)) {
60:             
61:             require(
62:                 logOutput.pubdataHash ==
63:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
64:                 "wp"
65:             );
66:             blobHashes[0] = logOutput.blob1Hash;
67:             blobCommitments[0] = bytes32(
68:                 _newBatch.pubdataCommitments[_newBatch.pubdataCommitments.length - 32:_newBatch
69:                     .pubdataCommitments
70:                     .length]
71:             );
72:         }
73: 
74:         require(_previousBatch.batchHash == logOutput.previousBatchHash, "l");
75:         
76:         require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t");
77:         
78:         require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta");
79: 
80:         
81:         _verifyBatchTimestamp(logOutput.packedBatchAndL2BlockTimestamp, _newBatch.timestamp, _previousBatch.timestamp);
82: 
83:         
84:         bytes32 commitment = _createBatchCommitment(_newBatch, logOutput.stateDiffHash, blobCommitments, blobHashes);
85: 
86:         return

```
['[110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L110-L110)']
```solidity
103:     function _verifyBatchTimestamp(
104:         uint256 _packedBatchAndL2BlockTimestamp,
105:         uint256 _expectedBatchTimestamp,
106:         uint256 _previousBatchTimestamp
107:     ) internal view {
108:         
109:         uint256 batchTimestamp = _packedBatchAndL2BlockTimestamp >> 128;
110:         require(batchTimestamp == _expectedBatchTimestamp, "tb"); // <= FOUND
111: 
112:         
113:         
114:         require(_previousBatchTimestamp < batchTimestamp, "h3");
115: 
116:         uint256 lastL2BlockTimestamp = _packedBatchAndL2BlockTimestamp & PACKED_L2_BLOCK_TIMESTAMP_MASK;
117: 
118:         
119:         
120:         
121:         
122:         require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1"); 
123:         require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2"); 
124:     }

```
['[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149-L149)']
```solidity
130:     function _processL2Logs(
131:         CommitBatchInfo calldata _newBatch,
132:         bytes32 _expectedSystemContractUpgradeTxHash
133:     ) internal pure returns (LogProcessingOutput memory logOutput) {
134:         
135:         bytes memory emittedL2Logs = _newBatch.systemLogs;
136: 
137:         
138:         
139:         uint256 processedLogs;
140: 
141:         
142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
143:             
144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
147: 
148:             
149:             require(!_checkBit(processedLogs, uint8(logKey)), "kp"); // <= FOUND
150:             processedLogs = _setBit(processedLogs, uint8(logKey));
151: 
152:             
153:             if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
154:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
155:                 logOutput.l2LogsTreeRoot = logValue;
156:             } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
157:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
158:                 logOutput.pubdataHash = logValue;
159:             } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
160:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
161:                 logOutput.stateDiffHash = logValue;
162:             } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
163:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
164:                 logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
165:             } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
166:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
167:                 logOutput.previousBatchHash = logValue;
168:             } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
169:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
170:                 logOutput.chainedPriorityTxsHash = logValue;
171:             } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
172:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
173:                 logOutput.numberOfLayer1Txs = uint256(logValue);
174:             } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
175:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
176:                 logOutput.blob1Hash = logValue;
177:             } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
178:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
179:                 logOutput.blob2Hash = logValue;
180:             } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
181:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
182:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
183:             } else {
184:                 revert("ul");
185:             }
186:         }
187: 
188:         
189:         
190:         
191:         if (_expectedSystemContractUpgradeTxHash == bytes32(0)) {
192:             require(processedLogs == 511, "b7");
193:         } else {
194:             require(processedLogs == 1023, "b8");
195:         }
196:     }

```
['[231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L231-L231)']
```solidity
215:     function _commitBatches(
216:         StoredBatchInfo memory _lastCommittedBatchData,
217:         CommitBatchInfo[] calldata _newBatchesData
218:     ) internal {
219:         
220:         
221:         
222:         
223:         
224:         
225:         
226:         require(
227:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:             "Executor facet: wrong protocol version"
229:         );
230:         
231:         require(_newBatchesData.length == 1, "e4"); // <= FOUND
232:         
233:         require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); 
234: 
235:         bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
236:         
237:         if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
238:             _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
239:         } else {
240:             _commitBatchesWithSystemContractsUpgrade(
241:                 _lastCommittedBatchData,
242:                 _newBatchesData,
243:                 systemContractsUpgradeTxHash
244:             );
245:         }
246: 
247:         s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
248:     }

```
['[284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284-L284)']
```solidity
273:     function _commitBatchesWithSystemContractsUpgrade(
274:         StoredBatchInfo memory _lastCommittedBatchData,
275:         CommitBatchInfo[] calldata _newBatchesData,
276:         bytes32 _systemContractUpgradeTxHash
277:     ) internal {
278:         
279:         
280:         
281: 
282:         
283:         
284:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik"); // <= FOUND
285: 
286:         
287:         s.l2SystemContractsUpgradeBatchNumber = _newBatchesData[0].batchNumber;
288: 
289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit(
300:                 _lastCommittedBatchData.batchNumber,
301:                 _lastCommittedBatchData.batchHash,
302:                 _lastCommittedBatchData.commitment
303:             );
304:         }
305:     }

```
['[323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323-L323)']
```solidity
321:     function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal {
322:         uint256 currentBatchNumber = _storedBatch.batchNumber;
323:         require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k");  // <= FOUND
324:         require(
325:             _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],
326:             "exe10" 
327:         );
328: 
329:         bytes32 priorityOperationsHash = _collectOperationsFromPriorityQueue(_storedBatch.numberOfLayer1Txs);
330:         require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x"); 
331: 
332:         
333:         s.l2LogsRootHashes[currentBatchNumber] = _storedBatch.l2LogsTreeRoot;
334:     }

```
['[358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358-L358)']
```solidity
349:     function _executeBatches(StoredBatchInfo[] calldata _batchesData) internal {
350:         uint256 nBatches = _batchesData.length;
351:         for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352:             _executeOneBatch(_batchesData[i], i);
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
354:         }
355: 
356:         uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
357:         s.totalBatchesExecuted = newTotalBatchesExecuted;
358:         require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n");  // <= FOUND
359: 
360:         uint256 batchWhenUpgradeHappened = s.l2SystemContractsUpgradeBatchNumber;
361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) {
362:             delete s.l2SystemContractsUpgradeTxHash;
363:             delete s.l2SystemContractsUpgradeBatchNumber;
364:         }
365:     }

```
['[402](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402-L402)']
```solidity
386:     function _proveBatches(
387:         StoredBatchInfo calldata _prevBatch,
388:         StoredBatchInfo[] calldata _committedBatches,
389:         ProofInput calldata _proof
390:     ) internal {
391:         
392:         uint256 currentTotalBatchesVerified = s.totalBatchesVerified;
393:         uint256 committedBatchesLength = _committedBatches.length;
394: 
395:         
396:         VerifierParams memory verifierParams = s.verifierParams;
397: 
398:         
399:         uint256[] memory proofPublicInput = new uint256[](committedBatchesLength);
400: 
401:         
402:         require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1"); // <= FOUND
403: 
404:         bytes32 prevBatchCommitment = _prevBatch.commitment;
405:         for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {
406:             currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
407:             require(
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409:                 "o1"
410:             );
411: 
412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment;
413:             proofPublicInput[i] = _getBatchProofPublicInput(
414:                 prevBatchCommitment,
415:                 currentBatchCommitment,
416:                 verifierParams
417:             );
418: 
419:             prevBatchCommitment = currentBatchCommitment;
420:         }
421:         require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q");
422: 
423:         
424: 
425:         
426:         assert(block.chainid != 1);
427:         
428:         
429:         if (_proof.serializedProof.length > 0) {
430:             _verifyProof(proofPublicInput, _proof);
431:         }
432:         
433:         _verifyProof(proofPublicInput, _proof);
434:         
435: 
436:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);
437:         s.totalBatchesVerified = currentTotalBatchesVerified;
438:     }

```
['[442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L442-L442)']
```solidity
440:     function _verifyProof(uint256[] memory proofPublicInput, ProofInput calldata _proof) internal view {
441:         
442:         require(proofPublicInput.length == 1, "t4"); // <= FOUND
443: 
444:         bool successVerifyProof = s.verifier.verify(
445:             proofPublicInput,
446:             _proof.serializedProof,
447:             _proof.recursiveAggregationInput
448:         );
449:         require(successVerifyProof, "p"); 
450:     }

```
['[482](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482-L482)']
```solidity
481:     function _revertBatches(uint256 _newLastBatch) internal {
482:         require(s.totalBatchesCommitted > _newLastBatch, "v1");  // <= FOUND
483:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); 
484: 
485:         if (_newLastBatch < s.totalBatchesVerified) {
486:             s.totalBatchesVerified = _newLastBatch;
487:         }
488:         s.totalBatchesCommitted = _newLastBatch;
489: 
490:         
491:         
492:         if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
493:             delete s.l2SystemContractsUpgradeBatchNumber;
494:         }
495: 
496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
497:     }

```
['[543](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L543-L543)']
```solidity
537:     function _batchAuxiliaryOutput(
538:         CommitBatchInfo calldata _batch,
539:         bytes32 _stateDiffHash,
540:         bytes32[] memory _blobCommitments,
541:         bytes32[] memory _blobHashes
542:     ) internal pure returns (bytes memory) {
543:         require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu"); // <= FOUND
544: 
545:         bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs);
546: 
547:         return
548:             abi.encodePacked(
549:                 l2ToL1LogsHash,
550:                 _stateDiffHash,
551:                 _batch.bootloaderHeapInitialContentsHash,
552:                 _batch.eventsQueueStateHash,
553:                 _encodeBlobAuxilaryOutput(_blobCommitments, _blobHashes)
554:             );
555:     }

```
['[567](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L567-L567)']
```solidity
561:     function _encodeBlobAuxilaryOutput(
562:         bytes32[] memory _blobCommitments,
563:         bytes32[] memory _blobHashes
564:     ) internal pure returns (bytes32[] memory blobAuxOutputWords) {
565:         
566:         
567:         require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10"); // <= FOUND
568:         require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11");
569: 
570:         
571:         
572:         
573:         
574:         
575:         
576:         
577: 
578:         blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT);
579: 
580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
583:         }
584:     }

```
['[631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631-L631)']
```solidity
625:     function _verifyBlobInformation(
626:         bytes calldata _pubdataCommitments,
627:         bytes32[] memory _blobHashes
628:     ) internal view returns (bytes32[] memory blobCommitments) {
629:         uint256 versionedHashIndex = 0;
630: 
631:         require(_pubdataCommitments.length > 0, "pl"); // <= FOUND
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
634:         blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);
635: 
636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
638: 
639:             require(blobVersionedHash != bytes32(0), "vh");
640: 
641:             
642:             
643:             bytes32 openingPoint = bytes32(
644:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645:             );
646: 
647:             _pointEvaluationPrecompile(
648:                 blobVersionedHash,
649:                 openingPoint,
650:                 _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE]
651:             );
652: 
653:             
654:             blobCommitments[versionedHashIndex] = keccak256(
655:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656:             );
657:             versionedHashIndex += 1;
658:         }
659: 
660:         
661:         
662:         bytes32 versionedHash = _getBlobVersionedHash(versionedHashIndex);
663:         require(versionedHash == bytes32(0), "lh");
664: 
665:         
666:         
667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
668:             require(
669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
671:                 "bh"
672:             );
673:         }
674:     }

```
['[681](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681-L681)']
```solidity
679:     function _getBlobVersionedHash(uint256 _index) internal view returns (bytes32 versionedHash) {
680:         (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index));
681:         require(success, "vc"); // <= FOUND
682:         versionedHash = abi.decode(data, (bytes32));
683:     }

```
['[183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183-L183)']
```solidity
181:     function isFunctionFreezable(bytes4 _selector) external view returns (bool) {
182:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();
183:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2"); // <= FOUND
184:         return ds.selectorToFacet[_selector].isFreezable;
185:     }

```
['[110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110-L110)']
```solidity
104:     function _proveL2LogInclusion(
105:         uint256 _batchNumber,
106:         uint256 _index,
107:         L2Log memory _log,
108:         bytes32[] calldata _proof
109:     ) internal view returns (bool) {
110:         require(_batchNumber <= s.totalBatchesExecuted, "xx"); // <= FOUND
111: 
112:         bytes32 hashedLog = keccak256(
113:             abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
114:         );
115:         
116:         
117:         require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");
118: 
119:         
120:         
121:         
122: 
123:         bytes32 calculatedRootHash = Merkle.calculateRoot(_proof, _index, hashedLog);
124:         bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];
125: 
126:         return actualRootHash == calculatedRootHash;
127:     }

```
['[243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L243-L243)']
```solidity
228:     function _requestL2TransactionSender(
229:         BridgehubL2TransactionRequest memory _request
230:     ) internal nonReentrant returns (bytes32 canonicalTxHash) {
231:         
232:         
233:         address l2Sender = _request.sender;
234:         if (l2Sender != tx.origin) {
235:             l2Sender = AddressAliasHelper.applyL1ToL2Alias(_request.sender);
236:         }
237: 
238:         
239:         
240:         
241:         
242:         
243:         require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp"); // <= FOUND
244: 
245:         
246:         WritePriorityOpParams memory params;
247: 
248:         params.sender = l2Sender;
249:         params.l2Value = _request.l2Value;
250:         params.contractAddressL2 = _request.contractL2;
251:         params.l2GasLimit = _request.l2GasLimit;
252:         params.l2GasPricePerPubdata = _request.l2GasPerPubdataByteLimit;
253:         params.refundRecipient = _request.refundRecipient;
254: 
255:         canonicalTxHash = _requestL2Transaction(_request.mintValue, params, _request.l2Calldata, _request.factoryDeps);
256:     }

```
['[264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L264-L264)']
```solidity
258:     function _requestL2Transaction(
259:         uint256 _mintValue,
260:         WritePriorityOpParams memory _params,
261:         bytes memory _calldata,
262:         bytes[] memory _factoryDeps
263:     ) internal returns (bytes32 canonicalTxHash) {
264:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj"); // <= FOUND
265:         _params.txId = s.priorityQueue.getTotalPriorityTxs();
266: 
267:         
268:         
269: 
270:         _params.l2GasPrice = _deriveL2GasPrice(tx.gasprice, _params.l2GasPricePerPubdata);
271:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
272:         require(_mintValue >= baseCost + _params.l2Value, "mv"); 
273: 
274:         
275:         address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
276:         
277:         if (refundRecipient.code.length > 0) {
278:             refundRecipient = AddressAliasHelper.applyL1ToL2Alias(refundRecipient);
279:         }
280:         _params.refundRecipient = refundRecipient;
281: 
282:         
283:         _params.expirationTimestamp = uint64(block.timestamp + PRIORITY_EXPIRATION); 
284:         _params.valueToMint = _mintValue;
285: 
286:         canonicalTxHash = _writePriorityOp(_params, _calldata, _factoryDeps);
287:     }

```
['[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107-L107)']
```solidity
96:     function diamondCut(DiamondCutData memory _diamondCut) internal {
97:         FacetCut[] memory facetCuts = _diamondCut.facetCuts;
98:         address initAddress = _diamondCut.initAddress;
99:         bytes memory initCalldata = _diamondCut.initCalldata;
100:         uint256 facetCutsLength = facetCuts.length;
101:         for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {
102:             Action action = facetCuts[i].action;
103:             address facet = facetCuts[i].facet;
104:             bool isFacetFreezable = facetCuts[i].isFreezable;
105:             bytes4[] memory selectors = facetCuts[i].selectors;
106: 
107:             require(selectors.length > 0, "B");  // <= FOUND
108: 
109:             if (action == Action.Add) {
110:                 _addFunctions(facet, selectors, isFacetFreezable);
111:             } else if (action == Action.Replace) {
112:                 _replaceFunctions(facet, selectors, isFacetFreezable);
113:             } else if (action == Action.Remove) {
114:                 _removeFunctions(facet, selectors);
115:             } else {
116:                 revert("C"); 
117:             }
118:         }
119: 
120:         _initializeDiamondCut(initAddress, initCalldata);
121:         emit DiamondCut(facetCuts, initAddress, initCalldata);
122:     }

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132-L132)']
```solidity
126:     function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
127:         DiamondStorage storage ds = getDiamondStorage();
128: 
129:         
130:         
131:         
132:         require(_facet.code.length > 0, "G"); // <= FOUND
133: 
134:         
135:         _saveFacetIfNew(_facet);
136: 
137:         uint256 selectorsLength = _selectors.length;
138:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
139:             bytes4 selector = _selectors[i];
140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
141:             require(oldFacet.facetAddress == address(0), "J"); 
142: 
143:             _addOneFunction(_facet, selector, _isFacetFreezable);
144:         }
145:     }

```
['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155-L155)']
```solidity
149:     function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
150:         DiamondStorage storage ds = getDiamondStorage();
151: 
152:         
153:         
154:         
155:         require(_facet.code.length > 0, "K"); // <= FOUND
156: 
157:         uint256 selectorsLength = _selectors.length;
158:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
159:             bytes4 selector = _selectors[i];
160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:             require(oldFacet.facetAddress != address(0), "L"); 
162: 
163:             _removeOneFunction(oldFacet.facetAddress, selector);
164:             
165:             _saveFacetIfNew(_facet);
166:             _addOneFunction(_facet, selector, _isFacetFreezable);
167:         }
168:     }

```
['[175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175-L175)']
```solidity
172:     function _removeFunctions(address _facet, bytes4[] memory _selectors) private {
173:         DiamondStorage storage ds = getDiamondStorage();
174: 
175:         require(_facet == address(0), "a1");  // <= FOUND
176: 
177:         uint256 selectorsLength = _selectors.length;
178:         for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
179:             bytes4 selector = _selectors[i];
180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
181:             require(oldFacet.facetAddress != address(0), "a2"); 
182: 
183:             _removeOneFunction(oldFacet.facetAddress, selector);
184:         }
185:     }

```
['[215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215-L215)']
```solidity
205:     function _addOneFunction(address _facet, bytes4 _selector, bool _isSelectorFreezable) private {
206:         DiamondStorage storage ds = getDiamondStorage();
207: 
208:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
209: 
210:         
211:         
212:         
213:         if (selectorPosition != 0) {
214:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
215:             require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1"); // <= FOUND
216:         }
217: 
218:         ds.selectorToFacet[_selector] = SelectorToFacet({
219:             facetAddress: _facet,
220:             selectorPosition: selectorPosition,
221:             isFreezable: _isSelectorFreezable
222:         });
223:         ds.facetToSelectors[_facet].selectors.push(_selector);
224:     }

```
['[280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280-L280)']
```solidity
278:     function _initializeDiamondCut(address _init, bytes memory _calldata) private {
279:         if (_init == address(0)) {
280:             require(_calldata.length == 0, "H");  // <= FOUND
281:         } else {
282:             
283:             (bool success, bytes memory data) = _init.delegatecall(_calldata);
284:             if (!success) {
285:                 
286:                 if (data.length <= 4) {
287:                     revert("I"); 
288:                 }
289: 
290:                 assembly {
291:                     revert(add(data, 0x20), mload(data))
292:                 }
293:             }
294: 
295:             
296:             
297:             require(data.length == 32, "lp");
298:             require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1");
299:         }
300:     }

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24-L24)']
```solidity
18:     function calculateRoot(
19:         bytes32[] calldata _path,
20:         uint256 _index,
21:         bytes32 _itemHash
22:     ) internal pure returns (bytes32) {
23:         uint256 pathLength = _path.length;
24:         require(pathLength > 0, "xc"); // <= FOUND
25:         require(pathLength < 256, "bt");
26:         require(_index < (1 << pathLength), "px");
27: 
28:         bytes32 currentHash = _itemHash;
29:         for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
30:             currentHash = (_index % 2 == 0)
31:                 ? _efficientHash(currentHash, _path[i])
32:                 : _efficientHash(_path[i], currentHash);
33:             _index /= 2;
34:         }
35: 
36:         return currentHash;
37:     }

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65-L65)']
```solidity
64:     function front(Queue storage _queue) internal view returns (PriorityOperation memory) {
65:         require(!_queue.isEmpty(), "D");  // <= FOUND
66: 
67:         return _queue.data[_queue.head];
68:     }

```
['[73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L73-L73)']
```solidity
72:     function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation) {
73:         require(!_queue.isEmpty(), "s");  // <= FOUND
74: 
75:         
76:         uint256 head = _queue.head;
77: 
78:         priorityOperation = _queue.data[head];
79:         delete _queue.data[head];
80:         _queue.head = head + 1;
81:     }

```
['[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28-L28)']
```solidity
19:     function validateL1ToL2Transaction(
20:         L2CanonicalTransaction memory _transaction,
21:         bytes memory _encoded,
22:         uint256 _priorityTxMaxGasLimit,
23:         uint256 _priorityTxMaxPubdata
24:     ) internal pure {
25:         uint256 l2GasForTxBody = getTransactionBodyGasLimit(_transaction.gasLimit, _encoded.length);
26: 
27:         
28:         require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui"); // <= FOUND
29:         
30:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk");
31: 
32:         
33:         
34:         require(
35:             getMinimalPriorityTransactionGasLimit(
36:                 _encoded.length,
37:                 _transaction.factoryDeps.length,
38:                 _transaction.gasPerPubdataByteLimit
39:             ) <= l2GasForTxBody,
40:             "up"
41:         );
42:     }

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48-L48)']
```solidity
46:     function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {
47:         
48:         require(_transaction.from <= type(uint16).max, "ua"); // <= FOUND
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
61:     }

```
['[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L115-L115)']
```solidity
109:     function getTransactionBodyGasLimit(
110:         uint256 _totalGasLimit,
111:         uint256 _encodingLength
112:     ) internal pure returns (uint256 txBodyGasLimit) {
113:         uint256 overhead = getOverheadForTransaction(_encodingLength);
114: 
115:         require(_totalGasLimit >= overhead, "my");  // <= FOUND
116:         unchecked {
117:             
118:             txBodyGasLimit = _totalGasLimit - overhead;
119:         }
120:     }

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58-L58)']
```solidity
46:     function _initializeReentrancyGuard() private {
47:         uint256 lockSlotOldValue;
48: 
49:         
50:         
51:         
52:         assembly {
53:             lockSlotOldValue := sload(LOCK_FLAG_ADDRESS)
54:             sstore(LOCK_FLAG_ADDRESS, _NOT_ENTERED)
55:         }
56: 
57:         
58:         require(lockSlotOldValue == 0, "1B"); // <= FOUND
59:     }

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84-L84)']
```solidity
82:     function hashL2Bytecode(bytes calldata _bytecode) internal view returns (bytes32 hashedBytecode) {
83:         
84:         require(_bytecode.length % 32 == 0, "po"); // <= FOUND
85: 
86:         uint256 lengthInWords = _bytecode.length / 32;
87:         require(lengthInWords < 2 ** 16, "pp"); 
88:         require(lengthInWords % 2 == 1, "pr"); 
89:         hashedBytecode =
90:             EfficientCall.sha(_bytecode) &
91:             0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF;
92:         
93:         hashedBytecode = (hashedBytecode | bytes32(uint256(1 << 248)));
94:         
95:         hashedBytecode = hashedBytecode | bytes32(lengthInWords << 224);
96:     }

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55-L55)']
```solidity
49:     function initialize(
50:         address _l1Bridge,
51:         address _l1LegecyBridge,
52:         bytes32 _l2TokenProxyBytecodeHash,
53:         address _aliasedOwner
54:     ) external reinitializer(2) {
55:         require(_l1Bridge != address(0), "bf"); // <= FOUND
56:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
57:         require(_aliasedOwner != address(0), "sf");
58:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df");
59: 
60:         l1Bridge = _l1Bridge;
61:         l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;
62: 
63:         if (block.chainid != ERA_CHAIN_ID) {
64:             address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
65:             l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
66:             l2TokenBeacon.transferOwnership(_aliasedOwner);
67:         } else {
68:             require(_l1LegecyBridge != address(0), "bf2");
69:             
70:         }
71:     }

```
[]
```solidity
79:     function finalizeDeposit(
80:         address _l1Sender,
81:         address _l2Receiver,
82:         address _l1Token,
83:         uint256 _amount,
84:         bytes calldata _data
85:     ) external payable override {
86:         
87:         require(
88:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90:             "mq"
91:         );
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");
93: 
94:         address expectedL2Token = l2TokenAddress(_l1Token);
95:         address currentL1Token = l1TokenAddress[expectedL2Token];
96:         if (currentL1Token == address(0)) {
97:             address deployedToken = _deployL2Token(_l1Token, _data);
98:             require(deployedToken == expectedL2Token, "mt");
99:             l1TokenAddress[expectedL2Token] = _l1Token;
100:         } else {
101:             require(currentL1Token == _l1Token, "gg"); 
102:         }
103: 
104:         IL2StandardToken(expectedL2Token).bridgeMint(_l2Receiver, _amount);
105:         emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount);
106:     }

```
['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129-L129)']
```solidity
123:     function withdraw(address _l1Receiver, address _l2Token, uint256 _amount) external override {
124:         require(_amount > 0, "Amount cannot be zero");
125: 
126:         IL2StandardToken(_l2Token).bridgeBurn(msg.sender, _amount);
127: 
128:         address l1Token = l1TokenAddress[_l2Token];
129:         require(l1Token != address(0), "yh"); // <= FOUND
130: 
131:         bytes memory message = _getL1WithdrawMessage(_l1Receiver, l1Token, _amount);
132:         L2ContractHelper.sendMessageToL1(message);
133: 
134:         emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount);
135:     }

```
['[176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L176-L176)']
```solidity
164:     function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy) {
165:         (bool success, bytes memory returndata) = SystemContractsCaller.systemCallWithReturndata(
166:             uint32(gasleft()),
167:             DEPLOYER_SYSTEM_CONTRACT,
168:             0,
169:             abi.encodeCall(
170:                 IContractDeployer.create2,
171:                 (salt, l2TokenProxyBytecodeHash, abi.encode(address(l2TokenBeacon), ""))
172:             )
173:         );
174: 
175:         
176:         require(success, "mk"); // <= FOUND
177:         proxy = BeaconProxy(abi.decode(returndata, (address)));
178:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51-L51)']
```solidity
50:     function bridgeInitialize(address _l1Address, bytes memory _data) external initializer {
51:         require(_l1Address != address(0), "in6");  // <= FOUND
52:         l1Address = _l1Address;
53: 
54:         l2Bridge = msg.sender;
55: 
56:         
57:         (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode(
58:             _data,
59:             (bytes, bytes, bytes)
60:         );
61: 
62:         ERC20Getters memory getters;
63:         string memory decodedName;
64:         string memory decodedSymbol;
65: 
66:         
67:         
68: 
69:         
70:         
71:         
72:         
73:         
74: 
75:         try this.decodeString(nameBytes) returns (string memory nameString) {
76:             decodedName = nameString;
77:         } catch {
78:             getters.ignoreName = true;
79:         }
80: 
81:         try this.decodeString(symbolBytes) returns (string memory symbolString) {
82:             decodedSymbol = symbolString;
83:         } catch {
84:             getters.ignoreSymbol = true;
85:         }
86: 
87:         
88:         __ERC20_init_unchained(decodedName, decodedSymbol);
89: 
90:         
91:         __ERC20Permit_init(decodedName);
92: 
93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
94:             
95:             decimals_ = decimalsUint8;
96:         } catch {
97:             getters.ignoreDecimals = true;
98:         }
99: 
100:         availableGetters = getters;

```
['[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120-L120)']
```solidity
111:     function reinitializeToken(
112:         ERC20Getters calldata _availableGetters,
113:         string memory _newName,
114:         string memory _newSymbol,
115:         uint8 _version
116:     ) external onlyNextVersion(_version) reinitializer(_version) {
117:         
118:         
119:         address beaconAddress = _getBeacon();
120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt"); // <= FOUND
121: 
122:         __ERC20_init_unchained(_newName, _newSymbol);
123:         __ERC20Permit_init(_newName);
124:         availableGetters = _availableGetters;
125: 
126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_);
127:     }

```


</details>

## [Gas-19] Divisions which do not divide by -X cannot overflow or underflow so such operations can be unchecked to save gas

### Resolution 
Make such found divisions are unchecked when ensured it is safe to do so

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L86-L86)']
```solidity
82:     function hashL2Bytecode(bytes calldata _bytecode) internal view returns (bytes32 hashedBytecode) {
83:         
84:         require(_bytecode.length % 32 == 0, "po");
85: 
86:         uint256 lengthInWords = _bytecode.length / 32; // <= FOUND
87:         require(lengthInWords < 2 ** 16, "pp"); 
88:         require(lengthInWords % 2 == 1, "pr"); 
89:         hashedBytecode =
90:             EfficientCall.sha(_bytecode) &
91:             0x00000000FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF;
92:         
93:         hashedBytecode = (hashedBytecode | bytes32(uint256(1 << 248)));
94:         
95:         hashedBytecode = hashedBytecode | bytes32(lengthInWords << 224);
96:     }

```
['[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L180-L180)']
```solidity
179:     function _splitRawNonce(uint256 _rawMinNonce) internal pure returns (uint256 deploymentNonce, uint256 minNonce) {
180:         deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER; // <= FOUND
181:         minNonce = _rawMinNonce % DEPLOY_NONCE_MULTIPLIER;
182:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L51-L51)']
```solidity
50:     function keccakGasCost(uint256 _length) internal pure returns (uint256) {
51:         return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1); // <= FOUND
52:     }

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L62-L62)']
```solidity
61:     function sha256GasCost(uint256 _length) internal pure returns (uint256) {
62:         return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1); // <= FOUND
63:     }

```


</details>

## [Gas-20] State variables which are not modified within functions should be set as constants or immutable for values set at deployment

### Resolution 
Set state variables listed below as constant or immutable for values set at deployment. Ensure it is safe to do so

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L37-L37)']
```solidity
37: uint256 public blockGasLimit = type(uint32).max; // <= FOUND

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L41-L41)']
```solidity
41: address public coinbase = BOOTLOADER_FORMAL_ADDRESS; // <= FOUND

```
['[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L44-L44)']
```solidity
44: uint256 public difficulty = 2.5e15; // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L37-L37)']
```solidity
37: address private l1LegacyBridge; // <= FOUND

```


</details>

## [Gas-21] Divisions of powers of 2 can be replaced by a right shift operation to save gas

### Resolution 
Replace such found divisions with right shift operations when ensured it is safe to do so. NOTE: This only applies to uint variables!

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L46-L46)']
```solidity
43:             
44:             
45:             
46:             uint256 mapIndex = _index / 8; // <= FOUND

```
['[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L86-L86)']
```solidity
86:         uint256 lengthInWords = _bytecode.length / 32; // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L57-L57)']
```solidity
56:             require(
57:                 dictionary.length / 8 <= encodedData.length / 2, // <= FOUND
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             );

```


</details>

## [Gas-22] multiplications of powers of 2 can be replaced by a left shift operation to save gas

### Resolution 
Replace such found multiplications with left shift operations when ensured it is safe to do so. NOTE: This only applies to uint variables!

Num of instances: 14

### Findings 


<details><summary>Click to show findings</summary>

['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L97-L97)']
```solidity
97:                 vInt += 8 + block.chainid * 2; // <= FOUND

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L62-L62)']
```solidity
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8; // <= FOUND

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L29-L29)']
```solidity
27:             
28:             
29:             uint256 bitOffset = (_index & 7) * 32; // <= FOUND

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L33-L33)']
```solidity
31:     
33:     uint256 private constant MAXIMAL_MIN_NONCE_INCREMENT = 2 ** 32; // <= FOUND

```
['[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L28-L28)']
```solidity
28:     uint256 private constant DEPLOY_NONCE_MULTIPLIER = 2 ** 128; // <= FOUND

```
['[582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582-L582)']
```solidity
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i]; // <= FOUND

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L52-L52)']
```solidity
51:             require(
52:                 encodedData.length * 4 == _bytecode.length, // <= FOUND
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             );

```
['[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L94-L94)']
```solidity
94: uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1; // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L46-L46)']
```solidity
46:             codeLengthInWords = uint256(uint8(_bytecodeHash[2])) * 256 + uint256(uint8(_bytecodeHash[3])); // <= FOUND

```
['[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L66-L66)']
```solidity
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4); // <= FOUND

```
['[253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L253-L253)']
```solidity
253:         number >>= (256 - (_calldataSlice.length * 8)); // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L37-L37)']
```solidity
37:                 uint256 shiftedVal = _val << (lbs * 8); // <= FOUND

```
['[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L72-L72)']
```solidity
72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8); // <= FOUND

```
['[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L108-L108)']
```solidity
106:         
107:         
108:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32); // <= FOUND

```


</details>

## [Gas-23] Structs can be packed into fewer storage slots

### Resolution 
In Solidity, each storage slot has a size of 32 bytes. If a struct contains multiple uint values, it's efficient to pack these into as few storage slots as possible to optimize gas usage. The EVM (Ethereum Virtual Machine) charges gas for each storage operation, so minimizing the number of slots used can result in substantial gas savings. This can be achieved by ordering struct fields according to their size or by using smaller data types where possible. However, developers must balance these optimizations with the need for code clarity and the precision requirements of their application. Always ensure that data packing does not compromise the functionality or security of the contract.

Num of instances: 12

### Findings 


<details><summary>Click to show findings</summary>

['[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28-L38)']
```solidity
28: struct ProposedUpgrade {
29:     L2CanonicalTransaction l2ProtocolUpgradeTx;
30:     bytes[] factoryDeps;
31:     bytes32 bootloaderHash;
32:     bytes32 defaultAccountHash;
33:     address verifier;
34:     VerifierParams verifierParams;
35:     bytes l1ContractsUpgradeCalldata;
36:     bytes postUpgradeCalldata;
37:     uint256 upgradeTimestamp; // <= FOUND
38:     uint256 newProtocolVersion; // <= FOUND
39: }

```
['[117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L117-L149)']
```solidity
117: struct Transaction {
118:     
119:     uint256 txType; // <= FOUND
120:     
121:     uint256 from; // <= FOUND
122:     
123:     uint256 to; // <= FOUND
124:     
126:     uint256 gasLimit; // <= FOUND
127:     
128:     uint256 gasPerPubdataByteLimit; // <= FOUND
129:     
131:     uint256 maxFeePerGas; // <= FOUND
132:     
134:     uint256 maxPriorityFeePerGas; // <= FOUND
135:     
136:     uint256 paymaster; // <= FOUND
137:     
138:     uint256 nonce; // <= FOUND
139:     
140:     uint256 value; // <= FOUND
141:     
149:     uint256[4] reserved; // <= FOUND
150:     
151:     bytes data;
152:     
153:     bytes signature;
154:     
157:     bytes32[] factoryDeps;
158:     
159:     bytes paymasterInput;
160:     
162:     bytes reservedDynamic;
163: }

```
['[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L10-L17)']
```solidity
10: struct L2TransactionRequestDirect {
11:     uint256 chainId; // <= FOUND
12:     uint256 mintValue; // <= FOUND
13:     address l2Contract;
14:     uint256 l2Value; // <= FOUND
15:     bytes l2Calldata;
16:     uint256 l2GasLimit; // <= FOUND
17:     uint256 l2GasPerPubdataByteLimit; // <= FOUND
18:     bytes[] factoryDeps;
19:     address refundRecipient;
20: }

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L22-L30)']
```solidity
22: struct L2TransactionRequestTwoBridgesOuter {
23:     uint256 chainId; // <= FOUND
24:     uint256 mintValue; // <= FOUND
25:     uint256 l2Value; // <= FOUND
26:     uint256 l2GasLimit; // <= FOUND
27:     uint256 l2GasPerPubdataByteLimit; // <= FOUND
28:     address refundRecipient;
29:     address secondBridgeAddress;
30:     uint256 secondBridgeValue; // <= FOUND
31:     bytes secondBridgeCalldata;
32: }

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IDiamondInit.sol#L25-L39)']
```solidity
25: struct InitializeData {
26:     uint256 chainId; // <= FOUND
27:     address bridgehub;
28:     address stateTransitionManager;
29:     uint256 protocolVersion; // <= FOUND
30:     address admin;
31:     address validatorTimelock;
32:     address baseToken;
33:     address baseTokenBridge;
34:     bytes32 storedBatchZero;
35:     IVerifier verifier;
36:     VerifierParams verifierParams;
37:     bytes32 l2BootloaderBytecodeHash;
38:     bytes32 l2DefaultAccountBytecodeHash;
39:     uint256 priorityTxMaxGasLimit; // <= FOUND
40:     FeeParams feeParams;
41:     address blobVersionedHashRetriever;
42: }

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L27-L34)']
```solidity
27: struct LogProcessingOutput {
28:     uint256 numberOfLayer1Txs; // <= FOUND
29:     bytes32 chainedPriorityTxsHash;
30:     bytes32 previousBatchHash;
31:     bytes32 pubdataHash;
32:     bytes32 stateDiffHash;
33:     bytes32 l2LogsTreeRoot;
34:     uint256 packedBatchAndL2BlockTimestamp; // <= FOUND
35:     bytes32 blob1Hash;
36:     bytes32 blob2Hash;
37: }

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L55-L64)']
```solidity
55: struct WritePriorityOpParams {
56:     address sender;
57:     uint256 txId; // <= FOUND
58:     uint256 l2Value; // <= FOUND
59:     address contractAddressL2;
60:     uint64 expirationTimestamp;
61:     uint256 l2GasLimit; // <= FOUND
62:     uint256 l2GasPrice; // <= FOUND
63:     uint256 l2GasPricePerPubdata; // <= FOUND
64:     uint256 valueToMint; // <= FOUND
65:     address refundRecipient;
66: }

```
['[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L98-L120)']
```solidity
98: struct L2CanonicalTransaction {
99:     uint256 txType; // <= FOUND
100:     uint256 from; // <= FOUND
101:     uint256 to; // <= FOUND
102:     uint256 gasLimit; // <= FOUND
103:     uint256 gasPerPubdataByteLimit; // <= FOUND
104:     uint256 maxFeePerGas; // <= FOUND
105:     uint256 maxPriorityFeePerGas; // <= FOUND
106:     uint256 paymaster; // <= FOUND
107:     uint256 nonce; // <= FOUND
108:     uint256 value; // <= FOUND
109:     
117:     uint256[4] reserved; // <= FOUND
118:     bytes data;
119:     bytes signature;
120:     uint256[] factoryDeps; // <= FOUND
121:     bytes paymasterInput;
122:     
124:     bytes reservedDynamic;
125: }

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L127-L134)']
```solidity
127: struct BridgehubL2TransactionRequest {
128:     address sender;
129:     address contractL2;
130:     uint256 mintValue; // <= FOUND
131:     uint256 l2Value; // <= FOUND
132:     bytes l2Calldata;
133:     uint256 l2GasLimit; // <= FOUND
134:     uint256 l2GasPerPubdataByteLimit; // <= FOUND
135:     bytes[] factoryDeps;
136:     address refundRecipient;
137: }

```
['[401](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L401-L403)']
```solidity
401:     struct MessageParams {
402:         uint256 l2BatchNumber; // <= FOUND
403:         uint256 l2MessageIndex; // <= FOUND
404:         uint16 l2TxNumberInBatch;
405:     }

```
['[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L90)']
```solidity
83:     struct StoredBatchInfo {
84:         uint64 batchNumber;
85:         bytes32 batchHash;
86:         uint64 indexRepeatedStorageChanges;
87:         uint256 numberOfLayer1Txs; // <= FOUND
88:         bytes32 priorityOperationsHash;
89:         bytes32 l2LogsTreeRoot;
90:         uint256 timestamp; // <= FOUND
91:         bytes32 commitment;
92:     }

```
['[126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L126-L128)']
```solidity
126:     struct ProofInput {
127:         uint256[] recursiveAggregationInput; // <= FOUND
128:         uint256[] serializedProof; // <= FOUND
129:     }

```


</details>

## [Gas-24] Expression ("") is cheaper than new bytes(0)

### Resolution 
In Solidity, using an empty string ("") instead of "new bytes(0)" in expressions can result in cheaper gas costs. This is because "new bytes(0)" creates a dynamic byte array, leading to additional overhead. By simply using ("") when an empty bytes array is needed, you can optimize for gas efficiency.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L196-L199)']
```solidity
182:         L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
183:             txType: SYSTEM_UPGRADE_L2_TX_TYPE,
184:             from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
185:             to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
186:             gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
187:             gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
188:             maxFeePerGas: uint256(0),
189:             maxPriorityFeePerGas: uint256(0),
190:             paymaster: uint256(0),
191:             
192:             nonce: protocolVersion,
193:             value: 0,
194:             reserved: [uint256(0), 0, 0, 0],
195:             data: systemContextCalldata,
196:             signature: new bytes(0), // <= FOUND
197:             factoryDeps: uintEmptyArray,
198:             paymasterInput: new bytes(0), // <= FOUND
199:             reservedDynamic: new bytes(0) // <= FOUND
200:         });

```
['[213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L213-L214)']
```solidity
213:             l1ContractsUpgradeCalldata: new bytes(0), // <= FOUND
214:             postUpgradeCalldata: new bytes(0), // <= FOUND
215:             upgradeTimestamp: 0,
216:             newProtocolVersion: protocolVersion
217:         });

```
['[308](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308-L311)']
```solidity
294:         transaction = L2CanonicalTransaction({
295:             txType: PRIORITY_OPERATION_L2_TX_TYPE,
296:             from: uint256(uint160(_priorityOpParams.sender)),
297:             to: uint256(uint160(_priorityOpParams.contractAddressL2)),
298:             gasLimit: _priorityOpParams.l2GasLimit,
299:             gasPerPubdataByteLimit: _priorityOpParams.l2GasPricePerPubdata,
300:             maxFeePerGas: uint256(_priorityOpParams.l2GasPrice),
301:             maxPriorityFeePerGas: uint256(0),
302:             paymaster: uint256(0),
303:             
304:             nonce: uint256(_priorityOpParams.txId),
305:             value: _priorityOpParams.l2Value,
306:             reserved: [_priorityOpParams.valueToMint, uint256(uint160(_priorityOpParams.refundRecipient)), 0, 0],
307:             data: _calldata,
308:             signature: new bytes(0), // <= FOUND
309:             factoryDeps: _hashFactoryDeps(_factoryDeps),
310:             paymasterInput: new bytes(0), // <= FOUND
311:             reservedDynamic: new bytes(0) // <= FOUND
312:         });

```


</details>

## [Gas-25] Private functions used once can be inlined

### Resolution 
Private functions which are only called once can be inlined to save GAS.

Num of instances: 15

### Findings 


<details><summary>Click to show findings</summary>

['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L92-L92)']
```solidity
92:     function _setL2DefaultAccountBytecodeHash(bytes32 _l2DefaultAccountBytecodeHash) private  // <= FOUND

```
['[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L109-L109)']
```solidity
109:     function _setL2BootloaderBytecodeHash(bytes32 _l2BootloaderBytecodeHash) private  // <= FOUND

```
['[126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L126-L126)']
```solidity
126:     function _setVerifier(IVerifier _newVerifier) private  // <= FOUND

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L142-L142)']
```solidity
142:     function _setVerifierParams(VerifierParams calldata _newVerifierParams) private  // <= FOUND

```
['[222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L222-L222)']
```solidity
222:     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure  // <= FOUND

```
['[126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L126-L126)']
```solidity
126:     function _addFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private  // <= FOUND

```
['[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L149-L149)']
```solidity
149:     function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private  // <= FOUND

```
['[172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L172-L172)']
```solidity
172:     function _removeFunctions(address _facet, bytes4[] memory _selectors) private  // <= FOUND

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L257-L257)']
```solidity
257:     function _removeFacet(address _facet) private  // <= FOUND

```
['[278](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L278-L278)']
```solidity
278:     function _initializeDiamondCut(address _init, bytes memory _calldata) private  // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L46-L46)']
```solidity
46:     function _initializeReentrancyGuard() private  // <= FOUND

```
['[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L118-L118)']
```solidity
118:     function _encodeHashEIP712Transaction(Transaction calldata _transaction) private view returns (bytes32)  // <= FOUND

```
['[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L147-L147)']
```solidity
147:     function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32)  // <= FOUND

```
['[219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L219-L219)']
```solidity
219:     function _encodeHashEIP2930Transaction(Transaction calldata _transaction) private view returns (bytes32)  // <= FOUND

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L289-L289)']
```solidity
289:     function _encodeHashEIP1559Transaction(Transaction calldata _transaction) private view returns (bytes32)  // <= FOUND

```


</details>

## [Gas-26] Use bitmap to save gas

### Resolution 
Bitmaps in Solidity are essentially a way of representing a set of boolean values within an integer type variable such as `uint256`. Each bit in the integer represents a true or false value (1 or 0), thus allowing efficient storage of multiple boolean values.

Bitmaps can save gas in the Ethereum network because they condense a lot of information into a small amount of storage. In Ethereum, storage is one of the most significant costs in terms of gas usage. By reducing the amount of storage space needed, you can potentially save on gas fees.

Here's a quick comparison:

If you were to represent 256 different boolean values in the traditional way, you would have to declare 256 different `bool` variables. Given that each `bool` occupies a storage slot and each storage slot costs 20,000 gas to initialize, you would end up paying a considerable amount of gas.

On the other hand, if you were to use a bitmap, you could store these 256 boolean values within a single `uint256` variable. In other words, you'd only pay for a single storage slot, resulting in significant gas savings.

However, it's important to note that while bitmaps can provide gas efficiencies, they do add complexity to the code, making it harder to read and maintain. Also, using bitmaps is efficient only when dealing with a large number of boolean variables that are frequently changed or accessed together. 

In contrast, the straightforward counterpart to bitmaps would be using arrays or mappings to store boolean values, with each `bool` value occupying its own storage slot. This approach is simpler and more readable but could potentially be more expensive in terms of gas usage.

Num of instances: 13

### Findings 


<details><summary>Click to show findings</summary>

['[418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418-L418)']
```solidity
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true; // <= FOUND

```
['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L87-L87)']
```solidity
87:         stateTransitionManagerIsRegistered[_stateTransitionManager] = true; // <= FOUND

```
['[103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103-L103)']
```solidity
103:         tokenIsRegistered[_token] = true; // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L68)']
```solidity
68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator"); // <= FOUND

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82-L82)']
```solidity
82:         validators[_chainId][_newValidator] = true; // <= FOUND

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L39-L39)']
```solidity
39:         s.validators[_initializeData.validatorTimelock] = true; // <= FOUND

```
['[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L137-L137)']
```solidity
137:         diamondStorage.isFrozen = true; // <= FOUND

```
['[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L78-L78)']
```solidity
78:             getters.ignoreName = true; // <= FOUND

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L84-L84)']
```solidity
84:             getters.ignoreSymbol = true; // <= FOUND

```
['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L97-L97)']
```solidity
97:             getters.ignoreDecimals = true; // <= FOUND

```
['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97-L97)']
```solidity
97:         stateTransitionManagerIsRegistered[_stateTransitionManager] = false; // <= FOUND

```
['[91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91-L91)']
```solidity
91:         validators[_chainId][_validator] = false; // <= FOUND

```
['[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L147-L147)']
```solidity
147:         diamondStorage.isFrozen = false; // <= FOUND

```


</details>

## [Gas-27] Use assembly hashing

### Resolution 
From a gas standpoint, the assembly version of the keccak256 hashing function can be more efficient than the high-level Solidity version. This is because Solidity has additional overhead when handling function calls and memory management, which can increase the gas cost.

Num of instances: 38

### Findings 


<details><summary>Click to show findings</summary>

['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76-L76)']
```solidity
76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, "")); // <= FOUND

```
['[210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L210-L210)']
```solidity
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount)); // <= FOUND

```
['[341](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L341-L341)']
```solidity
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount)); // <= FOUND

```
['[598](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598-L598)']
```solidity
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount)); // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100-L100)']
```solidity
100:         storedBatchZero = keccak256(abi.encode(batchZero)); // <= FOUND

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102-L102)']
```solidity
102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut)); // <= FOUND

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138-L138)']
```solidity
138:         initialCutHash = keccak256(abi.encode(_diamondCut)); // <= FOUND

```
['[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147-L147)']
```solidity
147:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData)); // <= FOUND

```
['[255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L255-L256)']
```solidity
255:         
256:         bytes32 cutHashInput = keccak256(_diamondCut); // <= FOUND

```
['[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104-L104)']
```solidity
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut)); // <= FOUND

```
['[313](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L313-L313)']
```solidity
313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash)); // <= FOUND

```
['[506](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L506-L506)']
```solidity
506:         bytes32 passThroughDataHash = keccak256(_batchPassThroughData(_newBatchData)); // <= FOUND

```
['[507](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L507-L507)']
```solidity
507:         bytes32 metadataHash = keccak256(_batchMetaParameters()); // <= FOUND

```
['[508](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L508-L508)']
```solidity
508:         bytes32 auxiliaryOutputHash = keccak256( // <= FOUND
509:             _batchAuxiliaryOutput(_newBatchData, _stateDiffHash, _blobCommitments, _blobHashes)
510:         );

```
['[545](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L545-L545)']
```solidity
545:         bytes32 l2ToL1LogsHash = keccak256(_batch.systemLogs); // <= FOUND

```
['[654](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654-L655)']
```solidity
654:             
655:             blobCommitments[versionedHashIndex] = keccak256( // <= FOUND
656:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
657:             );

```
['[112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L112-L112)']
```solidity
112:         bytes32 hashedLog = keccak256( // <= FOUND
113:             abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
114:         );

```
['[332](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L332-L332)']
```solidity
332:         canonicalTxHash = keccak256(transactionEncoding); // <= FOUND

```
['[212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L212-L212)']
```solidity
212:         bytes32 l2ProtocolUpgradeTxHash = keccak256(encodedTransaction); // <= FOUND

```
['[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L108-L108)']
```solidity
108:         bytes32 data = keccak256( // <= FOUND
109:             bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
110:         );

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L29-L29)']
```solidity
29:             txHash = keccak256(bytes.concat(signedTxHash, EfficientCall.keccak(_transaction.signature))); // <= FOUND

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L105-L105)']
```solidity
105:         bytes32 hash = keccak256( // <= FOUND
106:             bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
107:         );

```
['[121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L121-L123)']
```solidity
121:         
122:         
123:         bytes32 hash = keccak256( // <= FOUND
124:             bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
125:         );

```
['[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L89-L93)']
```solidity
89:         
90:         
91:         
92:         
93:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64); // <= FOUND

```
['[95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L95-L95)']
```solidity
95:         bytes32 hashedLog = keccak256( // <= FOUND
96:             abi.encodePacked(
97:                 _l2ToL1Log.l2ShardId,
98:                 _l2ToL1Log.isService,
99:                 _l2ToL1Log.txNumberInBlock,
100:                 _l2ToL1Log.sender,
101:                 _l2ToL1Log.key,
102:                 _l2ToL1Log.value
103:             )
104:         );

```
['[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106-L106)']
```solidity
106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog)); // <= FOUND

```
['[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122-L123)']
```solidity
122:         
123:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash)); // <= FOUND

```
['[148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L148-L153)']
```solidity
148:         
149:         
150:         
151:         
152:         
153:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + // <= FOUND
154:             3 *
155:             keccakGasCost(64) +
156:             gasSpentOnMessageHashing +
157:             COMPUTATIONAL_PRICE_FOR_PUBDATA *
158:             pubdataLen;

```
['[164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L164-L164)']
```solidity
164:         chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash)); // <= FOUND

```
['[212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L212-L212)']
```solidity
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog)); // <= FOUND

```
['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L225-L225)']
```solidity
225:                 l2ToL1LogsTreeArray[i] = keccak256( // <= FOUND
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );

```
['[243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L243-L243)']
```solidity
243:             reconstructedChainedMessagesHash = keccak256(abi.encode(reconstructedChainedMessagesHash, hashedMessage)); // <= FOUND

```
['[259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L259-L259)']
```solidity
259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256( // <= FOUND
260:                 abi.encode(
261:                     reconstructedChainedL1BytecodesRevealDataHash,
262:                     Utils.hashL2Bytecode(
263:                         _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength]
264:                     )
265:                 )
266:             );

```
['[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L159-L162)']
```solidity
159:             
160:             
161:             
162:             hash = keccak256(abi.encode(_block)); // <= FOUND

```
['[403](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403-L403)']
```solidity
403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash)); // <= FOUND

```
['[119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L119-L119)']
```solidity
119:         bytes32 structHash = keccak256( // <= FOUND
120:             abi.encode(
121:                 EIP712_TRANSACTION_TYPE_HASH,
122:                 _transaction.txType,
123:                 _transaction.from,
124:                 _transaction.to,
125:                 _transaction.gasLimit,
126:                 _transaction.gasPerPubdataByteLimit,
127:                 _transaction.maxFeePerGas,
128:                 _transaction.maxPriorityFeePerGas,
129:                 _transaction.paymaster,
130:                 _transaction.nonce,
131:                 _transaction.value,
132:                 EfficientCall.keccak(_transaction.data),
133:                 keccak256(abi.encodePacked(_transaction.factoryDeps)),
134:                 EfficientCall.keccak(_transaction.paymasterInput)
135:             )
136:         );

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L138-L138)']
```solidity
138:         bytes32 domainSeparator = keccak256( // <= FOUND
139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
140:         );

```
['[150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150-L150)']
```solidity
150:         bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), "")); // <= FOUND

```


</details>

## [Gas-28] Consider using OZ EnumerateSet in place of nested mappings

### Resolution 
Nested mappings and multi-dimensional arrays in Solidity operate through a process of double hashing, wherein the original storage slot and the first key are concatenated and hashed, and then this hash is again concatenated with the second key and hashed. This process can be quite gas expensive due to the double-hashing operation and subsequent storage operation (sstore).

A possible optimization involves manually concatenating the keys followed by a single hash operation and an sstore. However, this technique introduces the risk of storage collision, especially when there are other nested hash maps in the contract that use the same key types. Because Solidity is unaware of the number and structure of nested hash maps in a contract, it follows a conservative approach in computing the storage slot to avoid possible collisions.

OpenZeppelin's EnumerableSet provides a potential solution to this problem. It creates a data structure that combines the benefits of set operations with the ability to enumerate stored elements, which is not natively available in Solidity. EnumerableSet handles the element uniqueness internally and can therefore provide a more gas-efficient and collision-resistant alternative to nested mappings or multi-dimensional arrays in certain scenarios. 

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

['[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114-L114)']
```solidity
114:     mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized)) // <= FOUND

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32-L32)']
```solidity
32:     mapping(address account => mapping(address l1Token => mapping(bytes32 depositL2TxHash => uint256 amount))) // <= FOUND

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51-L51)']
```solidity
51:     mapping(address => mapping(address => uint256)) private __DEPRECATED_totalDepositedAmountPerUser; // <= FOUND

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52-L52)']
```solidity
52:     mapping(uint256 chainId => mapping(bytes32 l2DepositTxHash => bytes32 depositDataHash)) // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57-L57)']
```solidity
57:     mapping(uint256 chainId => mapping(uint256 l2BatchNumber => mapping(uint256 l2ToL1MessageNumber => bool isFinalized))) // <= FOUND

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L65-L65)']
```solidity
65:     mapping(uint256 chainId => mapping(address l1Token => uint256 balance)) internal chainBalance; // <= FOUND

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L50-L50)']
```solidity
50:     mapping(uint256 _chainId => mapping(address _validator => bool)) public validators; // <= FOUND

```
['[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L21-L21)']
```solidity
21:     mapping(uint256 contractAddress => mapping(uint256 index => bytes32 value)) internal immutableDataStorage; // <= FOUND

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L41-L41)']
```solidity
41:     mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues; // <= FOUND

```


</details>

## [Gas-29] Using this.<fn>() wastes gas

### Resolution 
In Solidity, when you call a function within the same contract using `this.<functionName>()`, it is considered an external function call. Even though it's a function within the same contract, calling it with `this` makes it behave as if it's an external function. This results in more gas being consumed because external function calls in Ethereum require more computational resources than internal calls.

The reason is that external calls need to go through the full process of transferring control between contracts, which includes steps such as saving and restoring the state, copying arguments to the memory, etc. In contrast, an internal function call is more like a traditional function call in a non-contract programming context, and it's far less resource-intensive.

As a result, it is advisable to use direct function calls, like `<functionName>()`, whenever calling functions within the same contract to optimize for gas efficiency.

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254-L254)']
```solidity
254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender); // <= FOUND

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L84-L84)']
```solidity
75:         
76:         
77: 
78:         
79:         
80:         
81:         
82:         
83: 
84:         try this.decodeString(nameBytes) returns (string memory nameString) { // <= FOUND

```
['[81](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L81-L81)']
```solidity
81:         try this.decodeString(symbolBytes) returns (string memory symbolString) { // <= FOUND

```
['[93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L93-L93)']
```solidity
93:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) { // <= FOUND

```


</details>

## [Gas-30] Use selfBalance() in place of address(this).balance

### Resolution 
In Solidity, using `selfBalance` instead of `address(this).balance` is advantageous for gas optimization. `address(this).balance` performs an external call to retrieve the contract's balance, which costs extra gas. As a resolution, defining a `selfBalance` state variable that's updated accordingly provides a more gas-efficient approach. Using selfBalance instead of address(this).balance can save around 800 gas per call. This is because address(this).balance makes an EXTBAL operation, which costs 700 gas, and additionally, the operation is a SLOAD, which costs around 800 gas. Please note that these estimates are based on the Ethereum gas schedule and might vary depending on the Ethereum network state and its future upgrades.

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118-L118)']
```solidity
118:             uint256 balanceBefore = address(this).balance; // <= FOUND

```
['[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120-L120)']
```solidity
120:             uint256 balanceAfter = address(this).balance; // <= FOUND

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41-L41)']
```solidity
41:         uint256 amount = address(this).balance; // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100-L100)']
```solidity
100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value"); // <= FOUND

```


</details>

## [Gas-31] Use assembly to emit events

### Resolution 
With the use of inline assembly in Solidity, we can take advantage of low-level features like scratch space and the free memory pointer, offering more gas-efficient ways of emitting events. The scratch space is a certain area of memory where we can temporarily store data, and the free memory pointer indicates the next available memory slot. Using these, we can efficiently assemble event data without incurring additional memory expansion costs. However, safety is paramount: to avoid overwriting or leakage, we must cache the free memory pointer before use and restore it afterward, ensuring that it points to the correct memory location post-operation.

Num of instances: 67

### Findings 


<details><summary>Click to show findings</summary>

['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L155-L155)']
```solidity
155:         emit DepositInitiated(l2TxHash, msg.sender, _l2Receiver, _l1Token, _amount); // <= FOUND

```
['[199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L199-L199)']
```solidity
199:         emit ClaimedFailedDeposit(_depositSender, _l1Token, amount); // <= FOUND

```
['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L225-L225)']
```solidity
225:         emit WithdrawalFinalized(l1Receiver, l1Token, amount); // <= FOUND

```
['[169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L169-L169)']
```solidity
168:         
169:         emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount); // <= FOUND

```
['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L227-L227)']
```solidity
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount); // <= FOUND

```
['[239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L239-L239)']
```solidity
239:         emit BridgehubDepositFinalized(_chainId, _txDataHash, _txHash); // <= FOUND

```
['[367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L367-L367)']
```solidity
367:         emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount); // <= FOUND

```
['[454](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L454-L454)']
```solidity
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount); // <= FOUND

```
['[602](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L602-L602)']
```solidity
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount); // <= FOUND

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56-L56)']
```solidity
56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin); // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68-L68)']
```solidity
68:         emit NewPendingAdmin(currentPendingAdmin, address(0)); // <= FOUND

```
['[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69-L69)']
```solidity
69:         emit NewAdmin(previousAdmin, pendingAdmin); // <= FOUND

```
['[145](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L145-L145)']
```solidity
145:         emit NewChain(_chainId, _stateTransitionManager, _admin); // <= FOUND

```
['[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47-L47)']
```solidity
47:         emit ChangeSecurityCouncil(address(0), _securityCouncil); // <= FOUND

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L50-L50)']
```solidity
50:         emit ChangeMinDelay(0, _minDelay); // <= FOUND

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L132-L132)']
```solidity
132:         emit TransparentOperationScheduled(id, _delay, _operation); // <= FOUND

```
['[144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L144-L144)']
```solidity
144:         emit ShadowOperationScheduled(_id, _delay); // <= FOUND

```
['[157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L157-L157)']
```solidity
157:         emit OperationCancelled(_id); // <= FOUND

```
['[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L180-L180)']
```solidity
180:         emit OperationExecuted(id); // <= FOUND

```
['[250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250-L250)']
```solidity
250:         emit ChangeMinDelay(minDelay, _newDelay); // <= FOUND

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257-L257)']
```solidity
257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil); // <= FOUND

```
['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227-L227)']
```solidity
227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion); // <= FOUND

```
['[235](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L235-L235)']
```solidity
235:         emit StateTransitionNewChain(_chainId, _stateTransitionContract); // <= FOUND

```
['[287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L287-L287)']
```solidity
287:         emit StateTransitionNewChain(_chainId, stateTransitionAddress); // <= FOUND

```
['[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L83-L83)']
```solidity
83:         emit ValidatorAdded(_chainId, _newValidator); // <= FOUND

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L92-L92)']
```solidity
92:         emit ValidatorRemoved(_chainId, _validator); // <= FOUND

```
['[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L98-L98)']
```solidity
98:         emit NewExecutionDelay(_executionDelay); // <= FOUND

```
['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L40)']
```solidity
40:         emit NewPendingAdmin(pendingAdmin, address(0)); // <= FOUND

```
['[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L47-L47)']
```solidity
47:         emit ValidatorStatusUpdate(_validator, _active); // <= FOUND

```
['[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L54-L54)']
```solidity
54:         emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable); // <= FOUND

```
['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L63-L63)']
```solidity
63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit); // <= FOUND

```
['[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L75-L75)']
```solidity
75:         emit NewFeeParams(oldFeeParams, _newFeeParams); // <= FOUND

```
['[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86-L86)']
```solidity
86:         emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator); // <= FOUND

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L92-L92)']
```solidity
92:         emit ValidiumModeStatusUpdate(_validiumMode); // <= FOUND

```
['[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L115-L115)']
```solidity
115:         emit ExecuteUpgrade(_diamondCut); // <= FOUND

```
['[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139-L139)']
```solidity
139:         emit Freeze(); // <= FOUND

```
['[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149-L149)']
```solidity
149:         emit Unfreeze(); // <= FOUND

```
['[261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L261)']
```solidity
261:             emit BlockCommit( // <= FOUND
262:                 _lastCommittedBatchData.batchNumber,
263:                 _lastCommittedBatchData.batchHash,
264:                 _lastCommittedBatchData.commitment
265:             );

```
['[353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353)']
```solidity
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment); // <= FOUND

```
['[438](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L438-L438)']
```solidity
436:         
437: 
438:         emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified); // <= FOUND

```
['[496](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L496-L496)']
```solidity
496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted); // <= FOUND

```
['[344](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L344-L344)']
```solidity
343:         
344:         emit NewPriorityRequest( // <= FOUND
345:             _priorityOpParams.txId,
346:             canonicalTxHash,
347:             _priorityOpParams.expirationTimestamp,
348:             transaction,
349:             _factoryDeps
350:         );

```
['[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L67-L67)']
```solidity
67:         emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade); // <= FOUND

```
['[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L104-L104)']
```solidity
104:         emit NewL2DefaultAccountBytecodeHash(previousDefaultAccountBytecodeHash, _l2DefaultAccountBytecodeHash); // <= FOUND

```
['[121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L121-L121)']
```solidity
121:         emit NewL2BootloaderBytecodeHash(previousBootloaderBytecodeHash, _l2BootloaderBytecodeHash); // <= FOUND

```
['[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L137-L137)']
```solidity
137:         emit NewVerifier(address(oldVerifier), address(_newVerifier)); // <= FOUND

```
['[157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L157-L157)']
```solidity
157:         emit NewVerifierParams(oldVerifierParams, _newVerifierParams); // <= FOUND

```
['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L40-L40)']
```solidity
40:         emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion); // <= FOUND

```
['[121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L121-L121)']
```solidity
121:         emit DiamondCut(facetCuts, initAddress, initCalldata); // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L68-L68)']
```solidity
68:         emit AccountVersionUpdated(msg.sender, _version); // <= FOUND

```
['[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L86-L86)']
```solidity
86:         emit AccountNonceOrderingUpdated(msg.sender, _nonceOrdering); // <= FOUND

```
['[355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L355-L355)']
```solidity
355:         emit ContractDeployed(_sender, _bytecodeHash, _newAddress); // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L59-L59)']
```solidity
59:             emit MarkedAsKnown(_bytecodeHash, _shouldSendToL1); // <= FOUND

```
['[111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L111-L111)']
```solidity
111:         emit L2ToL1LogSent(_l2ToL1Log); // <= FOUND

```
['[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L156-L156)']
```solidity
156:         emit L1MessageSent(msg.sender, hash, _message); // <= FOUND

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L181-L181)']
```solidity
181:         emit BytecodeL1PublicationRequested(_bytecodeHash); // <= FOUND

```
['[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L49-L49)']
```solidity
49:         emit Transfer(_from, _to, _amount); // <= FOUND

```
['[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L67-L67)']
```solidity
67:         emit Mint(_account, _amount); // <= FOUND

```
['[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L79-L79)']
```solidity
79:         emit Withdrawal(msg.sender, _l1Receiver, amount); // <= FOUND

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L92-L92)']
```solidity
92:         emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData); // <= FOUND

```
['[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L96-L96)']
```solidity
96:         emit ValueSetUnderNonce(msg.sender, _key, _value); // <= FOUND

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L105-L105)']
```solidity
105:         emit FinalizeDeposit(_l1Sender, _l2Receiver, expectedL2Token, _amount); // <= FOUND

```
['[134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L134-L134)']
```solidity
134:         emit WithdrawalInitiated(msg.sender, _l1Receiver, _l2Token, _amount); // <= FOUND

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101-L101)']
```solidity
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_); // <= FOUND

```
['[126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126-L126)']
```solidity
126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_); // <= FOUND

```
['[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L147-L147)']
```solidity
147:         emit BridgeMint(_to, _amount); // <= FOUND

```
['[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L156-L156)']
```solidity
156:         emit BridgeBurn(_from, _amount); // <= FOUND

```


</details>

## [Gas-32] Shorten the array rather than copying to a new one

### Resolution 
Leveraging inline assembly in Solidity provides the ability to directly manipulate the length slot of an array, thereby altering its length without the need to copy the elements to a new array of the desired size. This technique is more gas-efficient as it avoids the computational expense associated with array duplication. However, this method circumvents the type-checking and safety mechanisms of high-level Solidity and should be used judiciously. Always ensure that the array doesn't contain vital data beyond the revised length, as this data will become unreachable yet still consume storage space.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L46-L46)']
```solidity
46:         bytes32[] memory blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS); // <= FOUND

```
['[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L47-L47)']
```solidity
47:         bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS); // <= FOUND

```
['[399](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L399-L400)']
```solidity
399:         
400:         uint256[] memory proofPublicInput = new uint256[](committedBatchesLength); // <= FOUND

```
['[578](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L578-L586)']
```solidity
578:         
579:         
580:         
581:         
582:         
583:         
584:         
585: 
586:         blobAuxOutputWords = new bytes32[](2 * TOTAL_BLOBS_IN_COMMITMENT); // <= FOUND

```
['[634](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L634-L634)']
```solidity
634:         blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS); // <= FOUND

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L206-L206)']
```solidity
206:         result = new Facet[](facetsLen); // <= FOUND

```
['[355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L355-L355)']
```solidity
355:         hashedFactoryDeps = new uint256[](factoryDepsLen); // <= FOUND

```
['[204](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L204-L204)']
```solidity
204:         bytes32[] memory l2ToL1LogsTreeArray = new bytes32[](L2_TO_L1_LOGS_MERKLE_TREE_LEAVES); // <= FOUND

```


</details>

## [Gas-33] Use assembly in place of abi.decode to extract calldata values more efficiently

### Resolution 
Using inline assembly to extract calldata values can be more gas-efficient than using `abi.decode` in Solidity. Inline assembly gives more direct access to EVM operations, enabling optimized usage of calldata. However, assembly should be used judiciously as it's more prone to errors. Opt for this approach when performance is critical and the complexity it introduces is manageable.

Num of instances: 11

### Findings 


<details><summary>Click to show findings</summary>

['[190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L190-L190)']
```solidity
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode( // <= FOUND
191:             _data,
192:             (address, uint256, address)
193:         );

```
['[253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L253-L253)']
```solidity
252:         
253:         Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData)); // <= FOUND

```
['[617](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L617-L617)']
```solidity
617:         (, uint256 result) = abi.decode(data, (uint256, uint256)); // <= FOUND

```
['[682](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L682-L682)']
```solidity
682:         versionedHash = abi.decode(data, (bytes32)); // <= FOUND

```
['[298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298-L298)']
```solidity
298:             require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1"); // <= FOUND

```
['[348](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L348-L348)']
```solidity
347:             
348:             ImmutableData[] memory immutables = abi.decode(returnData, (ImmutableData[])); // <= FOUND

```
['[376](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L376-L376)']
```solidity
374:             
375:             
376:             (address token, uint256 minAllowance) = abi.decode(_transaction.paymasterInput[4:68], (address, uint256)); // <= FOUND

```
['[177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L177-L177)']
```solidity
177:         proxy = BeaconProxy(abi.decode(returndata, (address))); // <= FOUND

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L58-L58)']
```solidity
57:         
58:         (bytes memory nameBytes, bytes memory symbolBytes, bytes memory decimalsBytes) = abi.decode( // <= FOUND
59:             _data,
60:             (bytes, bytes, bytes)
61:         );

```
['[179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L179-L179)']
```solidity
179:         (result) = abi.decode(_input, (string)); // <= FOUND

```
['[184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L184-L184)']
```solidity
184:         (result) = abi.decode(_input, (uint8)); // <= FOUND

```


</details>

## [Gas-34] Counting down in for statements is more gas efficient

### Resolution 
Looping downwards in Solidity is more gas efficient due to how the EVM compares variables. In a 'for' loop that counts down, the end condition is usually to compare with zero, which is cheaper than comparing with another number. As such, restructure your loops to count downwards where possible.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L225)']
```solidity
225:        for (uint256 i = 0; i < _calls.length; ++i) { // <= FOUND
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
227:             if (!success) {
228:                 
229:                 assembly {
230:                     revert(add(returnData, 0x20), mload(returnData))
231:                 }
232:             }
233:         }

```
['[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580)']
```solidity
580:        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
583:         }

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226)']
```solidity
226:        for (uint256 i = 0; i < _factoryDeps.length; ++i) { // <= FOUND
227:             require(
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229:                 "Wrong factory dep hash"
230:             );
231:         }

```
['[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L135-L144)']
```solidity
127:        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84);
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++; // <= FOUND
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92);
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144:             stateDiffPtr++; // <= FOUND
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }

```
['[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248-L248)']
```solidity
248:        for (uint256 i = 0; i < deploymentsLength; ++i) { // <= FOUND
249:             sumOfValues += _deployments[i].value;
250:         }

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206-L206)']
```solidity
206:        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) { // <= FOUND
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }

```
['[224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224-L224)']
```solidity
224:            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) { // <= FOUND
225:                 l2ToL1LogsTreeArray[i] = keccak256(
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );
228:             }

```
['[657](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L657-L657)']
```solidity
636:        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
638: 
639:             require(blobVersionedHash != bytes32(0), "vh");
640: 
641:             
642:             
643:             bytes32 openingPoint = bytes32(
644:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645:             );
646: 
647:             _pointEvaluationPrecompile(
648:                 blobVersionedHash,
649:                 openingPoint,
650:                 _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE]
651:             );
652: 
653:             
654:             blobCommitments[versionedHashIndex] = keccak256(
655:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656:             );
657:             versionedHashIndex += 1; // <= FOUND
658:         }

```


</details>

## [Gas-35] Struct variables can be packed into fewer storage slots by truncating timestamp bytes

### Resolution 
Struct uint variables in Solidity are typically stored in 32-byte storage slots. When dealing with timestamps, which generally fit into a smaller byte size, it can be beneficial to truncate these bytes and pack them with other variables. This reduces the number of required storage slots, saving both storage space and associated gas costs. For example, a timestamp generally fits into a uint32, so it can be combined with other small variables within a single storage slot. When designing a contract, carefully structuring struct variables to utilize truncation and packing can lead to a more efficient and cost-effective implementation.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28-L37)']
```solidity
28: struct ProposedUpgrade { // <= FOUND
29:     L2CanonicalTransaction l2ProtocolUpgradeTx;
30:     bytes[] factoryDeps;
31:     bytes32 bootloaderHash;
32:     bytes32 defaultAccountHash;
33:     address verifier;
34:     VerifierParams verifierParams;
35:     bytes l1ContractsUpgradeCalldata;
36:     bytes postUpgradeCalldata;
37:     uint256 upgradeTimestamp; // <= FOUND
38:     uint256 newProtocolVersion;
39: }

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L27-L34)']
```solidity
27: struct LogProcessingOutput { // <= FOUND
28:     uint256 numberOfLayer1Txs;
29:     bytes32 chainedPriorityTxsHash;
30:     bytes32 previousBatchHash;
31:     bytes32 pubdataHash;
32:     bytes32 stateDiffHash;
33:     bytes32 l2LogsTreeRoot;
34:     uint256 packedBatchAndL2BlockTimestamp; // <= FOUND
35:     bytes32 blob1Hash;
36:     bytes32 blob2Hash;
37: }

```
['[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83-L90)']
```solidity
83:     struct StoredBatchInfo { // <= FOUND
84:         uint64 batchNumber;
85:         bytes32 batchHash;
86:         uint64 indexRepeatedStorageChanges;
87:         uint256 numberOfLayer1Txs;
88:         bytes32 priorityOperationsHash;
89:         bytes32 l2LogsTreeRoot;
90:         uint256 timestamp; // <= FOUND
91:         bytes32 commitment;
92:     }

```


</details>

## [Gas-36] Using private rather than public for constants and immutables, saves gas

### Resolution 
Using private visibility for constants and immutables in Solidity instead of public can save gas. This is because private elements are not included in the contract's ABI, reducing the deployment and interaction costs. To achieve better efficiency, it is recommended to use private visibility when external access is not needed.

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L26-L26)']
```solidity
26: string public constant override getName = "ValidatorTimelock"; // <= FOUND

```
['[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L20-L20)']
```solidity
20: string public constant override getName = "AdminFacet"; // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L27-L27)']
```solidity
27: string public constant override getName = "ExecutorFacet"; // <= FOUND

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25-L25)']
```solidity
25: string public constant override getName = "GettersFacet"; // <= FOUND

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35-L35)']
```solidity
35: string public constant override getName = "MailboxFacet"; // <= FOUND

```


</details>

## [Gas-37] Modulus operations that could be unchecked

### Resolution 
In Solidity 0.8.x and above, arithmetic operations like **modulus** automatically check for underflows and overflows, and revert the transaction if such a condition is met. This built-in safety feature provides a layer of security against potential numerical errors. However, these automatic checks also come with additional gas costs. In some situations, you may already have a guard condition, like a require() statement or an if statement, that ensures the safety of the arithmetic operation. In such cases, the automatic check becomes redundant and leads to unnecessary gas expenditure.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30-L30)']
```solidity
30:             currentHash = (_index % 2 == 0) // <= FOUND
31:                 ? _efficientHash(currentHash, _path[i])
32:                 : _efficientHash(_path[i], currentHash);

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L181-L181)']
```solidity
181:         minNonce = _rawMinNonce % DEPLOY_NONCE_MULTIPLIER; // <= FOUND

```
['[213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L213-L213)']
```solidity
213:         l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash; // <= FOUND

```


</details>

## [Gas-38] Mark Functions That Revert For Normal Users As payable

### Resolution 
In Solidity, marking functions as `payable` allows them to accept Ether. If a function is known to revert for regular users (non-admin or specific roles) but needs to be accessible to others, marking it as `payable` can be beneficial. This ensures that even if a regular user accidentally sends Ether to the function, the Ether won't be trapped, as the function reverts, returning the funds. This can save gas by avoiding unnecessary failure handling in the function itself. Resolution: Carefully assess the roles and access patterns, and mark functions that should revert for regular users as `payable` to handle accidental Ether transfers.

Num of instances: 36

### Findings 


<details><summary>Click to show findings</summary>

['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116-L116)']
```solidity
116:     function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
117:         if (_token == ETH_TOKEN_ADDRESS) {
118:             uint256 balanceBefore = address(this).balance;
119:             IMailbox(_target).transferEthToSharedBridge();
120:             uint256 balanceAfter = address(this).balance;
121:             require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
122:             chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
123:                 chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
124:                 balanceAfter -
125:                 balanceBefore;
126:         } else {
127:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
128:             uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
129:             require(amount > 0, "ShB: 0 amount to transfer");
130:             IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
131:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
132:             require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
134:         }
135:     }

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L142-L142)']
```solidity
142:     function initializeChainGovernance(uint256 _chainId, address _l2BridgeAddress) external onlyOwner {
143:         l2BridgeAddress[_chainId] = _l2BridgeAddress;
144:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51-L51)']
```solidity
51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
52:         
53:         address oldPendingAdmin = pendingAdmin;
54:         
55:         pendingAdmin = _newPendingAdmin;
56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
57:     }

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L82-L82)']
```solidity
82:     function addStateTransitionManager(address _stateTransitionManager) external onlyOwner {
83:         require(
84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],
85:             "Bridgehub: state transition already registered"
86:         );
87:         stateTransitionManagerIsRegistered[_stateTransitionManager] = true;
88:     }

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L92-L92)']
```solidity
92:     function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
93:         require(
94:             stateTransitionManagerIsRegistered[_stateTransitionManager],
95:             "Bridgehub: state transition not registered yet"
96:         );
97:         stateTransitionManagerIsRegistered[_stateTransitionManager] = false;
98:     }

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L101-L101)']
```solidity
101:     function addToken(address _token) external onlyOwner {
102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered");
103:         tokenIsRegistered[_token] = true;
104:     }

```
['[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108-L108)']
```solidity
108:     function setSharedBridge(address _sharedBridge) external onlyOwner {
109:         sharedBridge = IL1SharedBridge(_sharedBridge);
110:     }

```
['[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L114)']
```solidity
114:     function createNewChain(
115:         uint256 _chainId,
116:         address _stateTransitionManager,
117:         address _baseToken,
118:         uint256, 
119:         address _admin,
120:         bytes calldata _initData
121:     ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");
123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
124: 
125:         require(
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         );
129:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set");
131: 
132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
133: 
134:         stateTransitionManager[_chainId] = _stateTransitionManager;
135:         baseToken[_chainId] = _baseToken;
136: 
137:         IStateTransitionManager(_stateTransitionManager).createNewChain(
138:             _chainId,
139:             _baseToken,
140:             address(sharedBridge),
141:             _admin,
142:             _initData
143:         );
144: 
145:         emit NewChain(_chainId, _stateTransitionManager, _admin);
146:         return _chainId;
147:     }

```
['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L129-L129)']
```solidity
129:     function scheduleTransparent(Operation calldata _operation, uint256 _delay) external onlyOwner {
130:         bytes32 id = hashOperation(_operation);
131:         _schedule(id, _delay);
132:         emit TransparentOperationScheduled(id, _delay, _operation);
133:     }

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L142-L142)']
```solidity
142:     function scheduleShadow(bytes32 _id, uint256 _delay) external onlyOwner {
143:         _schedule(_id, _delay);
144:         emit ShadowOperationScheduled(_id, _delay);
145:     }

```
['[154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L154-L154)']
```solidity
154:     function cancel(bytes32 _id) external onlyOwner {
155:         require(isOperationPending(_id), "Operation must be pending");
156:         delete timestamps[_id];
157:         emit OperationCancelled(_id);
158:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51-L51)']
```solidity
51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
52:         
53:         address oldPendingAdmin = pendingAdmin;
54:         
55:         pendingAdmin = _newPendingAdmin;
56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
57:     }

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L132-L132)']
```solidity
132:     function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {
133:         validatorTimelock = _validatorTimelock;
134:     }

```
['[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L137-L137)']
```solidity
137:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {
138:         initialCutHash = keccak256(abi.encode(_diamondCut));
139:     }

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L142-L142)']
```solidity
142:     function setNewVersionUpgrade(
143:         Diamond.DiamondCutData calldata _cutData,
144:         uint256 _oldProtocolVersion,
145:         uint256 _newProtocolVersion
146:     ) external onlyOwner {
147:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
148:         protocolVersion = _newProtocolVersion;
149:     }

```
['[152](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L152-L152)']
```solidity
152:     function setUpgradeDiamondCut(
153:         Diamond.DiamondCutData calldata _cutData,
154:         uint256 _oldProtocolVersion
155:     ) external onlyOwner {
156:         upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
157:     }

```
['[160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L160-L160)']
```solidity
160:     function freezeChain(uint256 _chainId) external onlyOwner {
161:         IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
162:     }

```
['[165](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L165-L165)']
```solidity
165:     function unfreezeChain(uint256 _chainId) external onlyOwner {
166:         IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
167:     }

```
['[170](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L170-L170)']
```solidity
170:     function revertBatches(uint256 _chainId, uint256 _newLastBatch) external onlyOwnerOrAdmin {
171:         IZkSyncStateTransition(stateTransition[_chainId]).revertBatches(_newLastBatch);
172:     }

```
['[230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L230-L230)']
```solidity
230:     function registerAlreadyDeployedStateTransition(
231:         uint256 _chainId,
232:         address _stateTransitionContract
233:     ) external onlyOwner {
234:         stateTransition[_chainId] = _stateTransitionContract;
235:         emit StateTransitionNewChain(_chainId, _stateTransitionContract);
236:     }

```
['[73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73-L73)']
```solidity
73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
74:         stateTransitionManager = _stateTransitionManager;
75:     }

```
['[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96-L96)']
```solidity
96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner {
97:         executionDelay = _executionDelay;
98:         emit NewExecutionDelay(_executionDelay);
99:     }

```
['[45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45-L45)']
```solidity
45:     function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
46:         s.validators[_validator] = _active;
47:         emit ValidatorStatusUpdate(_validator, _active);
48:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L51-L51)']
```solidity
51:     function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
52:         
53:         s.zkPorterIsAvailable = _zkPorterIsAvailable;
54:         emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable);
55:     }

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L58-L58)']
```solidity
58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager {
59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
60: 
61:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;
62:         s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
64:     }

```
['[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67-L67)']
```solidity
67:     function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
68:         
69:         
70:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");
71: 
72:         FeeParams memory oldFeeParams = s.feeParams;
73:         s.feeParams = _newFeeParams;
74: 
75:         emit NewFeeParams(oldFeeParams, _newFeeParams);
76:     }

```
['[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79-L79)']
```solidity
79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
80:         uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;
81:         uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;
82: 
83:         s.baseTokenGasPriceMultiplierNominator = _nominator;
84:         s.baseTokenGasPriceMultiplierDenominator = _denominator;
85: 
86:         emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator);
87:     }

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L100-L100)']
```solidity
100:     function upgradeChainFromVersion(
101:         uint256 _oldProtocolVersion,
102:         Diamond.DiamondCutData calldata _diamondCut
103:     ) external onlyAdminOrStateTransitionManager {
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
110:         require(
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         );
114:         Diamond.diamondCut(_diamondCut);
115:         emit ExecuteUpgrade(_diamondCut);
116:         require(
117:             s.protocolVersion > _oldProtocolVersion,
118:             "StateTransition: protocolVersion mismatch in STC after upgrading"
119:         );
120:     }

```
['[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L123-L123)']
```solidity
123:     function executeUpgrade(Diamond.DiamondCutData calldata _diamondCut) external onlyStateTransitionManager {
124:         Diamond.diamondCut(_diamondCut);
125:         emit ExecuteUpgrade(_diamondCut);
126:     }

```
['[133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L133-L133)']
```solidity
133:     function freezeDiamond() external onlyAdminOrStateTransitionManager {
134:         Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
135: 
136:         require(!diamondStorage.isFrozen, "a9"); 
137:         diamondStorage.isFrozen = true;
138: 
139:         emit Freeze();
140:     }

```
['[143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L143-L143)']
```solidity
143:     function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
144:         Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();
145: 
146:         require(diamondStorage.isFrozen, "a7"); 
147:         diamondStorage.isFrozen = false;
148: 
149:         emit Unfreeze();
150:     }

```
['[472](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472-L472)']
```solidity
472:     function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {
473:         _revertBatches(_newLastBatch);
474:     }

```
['[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L78-L78)']
```solidity
78:     function addValidator(uint256 _chainId, address _newValidator) external onlyChainAdmin(_chainId) {
79:         if (validators[_chainId][_newValidator]) {
80:             revert AddressAlreadyValidator(_chainId);
81:         }
82:         validators[_chainId][_newValidator] = true;
83:         emit ValidatorAdded(_chainId, _newValidator);
84:     }

```
['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L87-L87)']
```solidity
87:     function removeValidator(uint256 _chainId, address _validator) external onlyChainAdmin(_chainId) {
88:         if (!validators[_chainId][_validator]) {
89:             revert ValidatorDoesNotExist(_chainId);
90:         }
91:         validators[_chainId][_validator] = false;
92:         emit ValidatorRemoved(_chainId, _validator);
93:     }

```
['[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23-L23)']
```solidity
23:     function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
24:         
25:         address oldPendingAdmin = s.pendingAdmin;
26:         
27:         s.pendingAdmin = _newPendingAdmin;
28:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
29:     }

```
['[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L89-L89)']
```solidity
89:     function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis"); 
91:         s.feeParams.pubdataPricingMode = _validiumMode;
92:         emit ValidiumModeStatusUpdate(_validiumMode);
93:     }

```


</details>

## [Gas-39] Lack of unchecked in loops

### Resolution 
In Solidity, the `unchecked` block allows arithmetic operations to not revert on overflow. Without using `unchecked` in loops, extra gas is consumed due to overflow checks. If it's certain that overflows won't occur within the loop, using `unchecked` can make the loop more gas-efficient by skipping unnecessary checks.

Num of instances: 21

### Findings 


<details><summary>Click to show findings</summary>

['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L225)']
```solidity
225:        for (uint256 i = 0; i < _calls.length; ++i) {
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
227:             if (!success) {
228:                 
229:                 assembly {
230:                     revert(add(returnData, 0x20), mload(returnData))
231:                 }
232:             }
233:         }

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L142)']
```solidity
142:        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
143:             
144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
147: 
148:             
149:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");
150:             processedLogs = _setBit(processedLogs, uint8(logKey));
151: 
152:             
153:             if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
154:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
155:                 logOutput.l2LogsTreeRoot = logValue;
156:             } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
157:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
158:                 logOutput.pubdataHash = logValue;
159:             } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
160:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
161:                 logOutput.stateDiffHash = logValue;
162:             } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
163:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
164:                 logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
165:             } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
166:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
167:                 logOutput.previousBatchHash = logValue;
168:             } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
169:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
170:                 logOutput.chainedPriorityTxsHash = logValue;
171:             } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
172:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
173:                 logOutput.numberOfLayer1Txs = uint256(logValue);
174:             } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
175:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
176:                 logOutput.blob1Hash = logValue;
177:             } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
178:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
179:                 logOutput.blob2Hash = logValue;
180:             } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
181:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
182:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
183:             } else {
184:                 revert("ul");
185:             }
186:         }

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257)']
```solidity
257:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259: 
260:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:             emit BlockCommit(
262:                 _lastCommittedBatchData.batchNumber,
263:                 _lastCommittedBatchData.batchHash,
264:                 _lastCommittedBatchData.commitment
265:             );
266:         }

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289-L289)']
```solidity
289:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit(
300:                 _lastCommittedBatchData.batchNumber,
301:                 _lastCommittedBatchData.batchHash,
302:                 _lastCommittedBatchData.commitment
303:             );
304:         }

```
['[311](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311-L311)']
```solidity
311:        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) {
312:             PriorityOperation memory priorityOp = s.priorityQueue.popFront();
313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
314:         }

```
['[351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351-L351)']
```solidity
351:        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352:             _executeOneBatch(_batchesData[i], i);
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
354:         }

```
['[405](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405-L405)']
```solidity
405:        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) {
406:             currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
407:             require(
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409:                 "o1"
410:             );
411: 
412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment;
413:             proofPublicInput[i] = _getBatchProofPublicInput(
414:                 prevBatchCommitment,
415:                 currentBatchCommitment,
416:                 verifierParams
417:             );
418: 
419:             prevBatchCommitment = currentBatchCommitment;
420:         }

```
['[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580)']
```solidity
580:        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
583:         }

```
['[636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636)']
```solidity
636:        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
638: 
639:             require(blobVersionedHash != bytes32(0), "vh");
640: 
641:             
642:             
643:             bytes32 openingPoint = bytes32(
644:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645:             );
646: 
647:             _pointEvaluationPrecompile(
648:                 blobVersionedHash,
649:                 openingPoint,
650:                 _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE]
651:             );
652: 
653:             
654:             blobCommitments[versionedHashIndex] = keccak256(
655:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656:             );
657:             versionedHashIndex += 1;
658:         }

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208-L208)']
```solidity
208:        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
209:             address facetAddr = ds.facets[i];
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
211: 
212:             result[i] = Facet(facetAddr, facetToSelectors.selectors);
213:         }

```
['[356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356-L356)']
```solidity
356:        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
358: 
359:             
360:             assembly {
361:                 mstore(add(hashedFactoryDeps, mul(add(i, 1), 32)), hashedBytecode)
362:             }
363:         }

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226)']
```solidity
226:        for (uint256 i = 0; i < _factoryDeps.length; ++i) {
227:             require(
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229:                 "Wrong factory dep hash"
230:             );
231:         }

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101-L101)']
```solidity
101:        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {
102:             Action action = facetCuts[i].action;
103:             address facet = facetCuts[i].facet;
104:             bool isFacetFreezable = facetCuts[i].isFreezable;
105:             bytes4[] memory selectors = facetCuts[i].selectors;
106: 
107:             require(selectors.length > 0, "B"); 
108: 
109:             if (action == Action.Add) {
110:                 _addFunctions(facet, selectors, isFacetFreezable);
111:             } else if (action == Action.Replace) {
112:                 _replaceFunctions(facet, selectors, isFacetFreezable);
113:             } else if (action == Action.Remove) {
114:                 _removeFunctions(facet, selectors);
115:             } else {
116:                 revert("C"); 
117:             }
118:         }

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138-L138)']
```solidity
138:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
139:             bytes4 selector = _selectors[i];
140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
141:             require(oldFacet.facetAddress == address(0), "J"); 
142: 
143:             _addOneFunction(_facet, selector, _isFacetFreezable);
144:         }

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158-L158)']
```solidity
158:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
159:             bytes4 selector = _selectors[i];
160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:             require(oldFacet.facetAddress != address(0), "L"); 
162: 
163:             _removeOneFunction(oldFacet.facetAddress, selector);
164:             
165:             _saveFacetIfNew(_facet);
166:             _addOneFunction(_facet, selector, _isFacetFreezable);
167:         }

```
['[178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178-L178)']
```solidity
178:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
179:             bytes4 selector = _selectors[i];
180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
181:             require(oldFacet.facetAddress != address(0), "a2"); 
182: 
183:             _removeOneFunction(oldFacet.facetAddress, selector);
184:         }

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29-L29)']
```solidity
29:        for (uint256 i; i < pathLength; i = i.uncheckedInc()) {
30:             currentHash = (_index % 2 == 0)
31:                 ? _efficientHash(currentHash, _path[i])
32:                 : _efficientHash(_path[i], currentHash);
33:             _index /= 2;
34:         }

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127-L127)']
```solidity
127:        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) {
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84);
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++;
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92);
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144:             stateDiffPtr++;
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }

```
['[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248-L248)']
```solidity
248:        for (uint256 i = 0; i < deploymentsLength; ++i) {
249:             sumOfValues += _deployments[i].value;
250:         }

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206-L206)']
```solidity
206:        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) {
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }

```
['[224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224-L224)']
```solidity
224:            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) {
225:                 l2ToL1LogsTreeArray[i] = keccak256(
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );
228:             }

```


</details>

## [Gas-40] Consider migrating require statements to custom errors

### Resolution 
Using custom errors instead of 'require' statements in Solidity can lead to gas savings and improve developer experience. Custom errors provide explicit error messages, aiding in troubleshooting. Moreover, custom errors are cheaper as they don't require a string literal, thus saving gas. Hence, developers should replace 'require' statements with custom errors wherever possible for efficiency and readability.

Num of instances: 312

### Findings 


<details><summary>Click to show findings</summary>

['[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64-L64)']
```solidity
64:         require(msg.sender == address(sharedBridge), "Not shared bridge"); // <= FOUND

```
['[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L66-L66)']
```solidity
66:         require(amount == _amount, "Incorrect amount"); // <= FOUND

```
['[141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141-L141)']
```solidity
141:         require(_amount != 0, "0T");  // <= FOUND

```
['[161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161-L161)']
```solidity
161:         require(amount == _amount, "3T");  // <= FOUND

```
['[186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186-L186)']
```solidity
186:         require(amount != 0, "2T");  // <= FOUND

```
['[215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215-L215)']
```solidity
215:         require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw"); // <= FOUND

```
['[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69-L69)']
```solidity
69:         require(msg.sender == address(bridgehub), "ShB not BH"); // <= FOUND

```
['[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L78)']
```solidity
75:         require( // <= FOUND
76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77:             "L1SharedBridge: not bridgehub or era chain"
78:         ); // <= FOUND

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84-L84)']
```solidity
84:         require(msg.sender == address(legacyBridge), "ShB not legacy bridge"); // <= FOUND

```
['[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L108-L108)']
```solidity
108:         require(_owner != address(0), "ShB owner 0"); // <= FOUND

```
['[121](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L121-L121)']
```solidity
121:             require(balanceAfter > balanceBefore, "ShB: 0 eth transferred"); // <= FOUND

```
['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129-L129)']
```solidity
129:             require(amount > 0, "ShB: 0 amount to transfer"); // <= FOUND

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132-L132)']
```solidity
132:             require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred"); // <= FOUND

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138-L138)']
```solidity
138:         require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition"); // <= FOUND

```
['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155-L155)']
```solidity
155:             require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount"); // <= FOUND

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158-L159)']
```solidity
158:             
159:             require(msg.value == 0, "ShB m.v > 0 b d.it"); // <= FOUND

```
['[161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L161-L161)']
```solidity
161:             require(amount == _amount, "3T");  // <= FOUND

```
['[188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188-L188)']
```solidity
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed"); // <= FOUND

```
['[194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L194-L194)']
```solidity
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported"); // <= FOUND

```
['[195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L195-L195)']
```solidity
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported"); // <= FOUND

```
['[200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200-L200)']
```solidity
200:             require(_depositAmount == 0, "ShB wrong withdraw amount"); // <= FOUND

```
['[202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202-L202)']
```solidity
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2"); // <= FOUND

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206-L206)']
```solidity
206:             require(withdrawAmount == _depositAmount, "5T");  // <= FOUND

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208-L208)']
```solidity
208:         require(amount != 0, "6T");  // <= FOUND

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237-L237)']
```solidity
237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap"); // <= FOUND

```
['[325](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L325-L325)']
```solidity
325:             require(proofValid, "yn"); // <= FOUND

```
['[327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327-L327)']
```solidity
327:         require(_amount > 0, "y1"); // <= FOUND

```
['[342](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L342-L342)']
```solidity
342:                 require(dataHash == txDataHash, "ShB: d.it not hap"); // <= FOUND

```
['[349](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349-L350)']
```solidity
349:             
350:             require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds"); // <= FOUND

```
['[360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L360-L360)']
```solidity
360:             require(callSuccess, "ShB: claimFailedDeposit failed"); // <= FOUND

```
['[396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L396-L396)']
```solidity
396:             require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal"); // <= FOUND

```
['[417](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417-L417)']
```solidity
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized"); // <= FOUND

```
['[427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L427-L427)']
```solidity
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2"); // <= FOUND

```
['[439](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L439-L440)']
```solidity
439:             
440:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2");  // <= FOUND

```
['[449](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L449-L449)']
```solidity
449:             require(callSuccess, "ShB: withdraw failed"); // <= FOUND

```
['[484](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L484-L484)']
```solidity
484:         require(success, "ShB withd w proof");  // <= FOUND

```
['[501](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L501-L511)']
```solidity
501:         
502:         
503:         
504:         
505:         
506:         
507:         
508:         
509: 
510:         
511:         require(_l2ToL1message.length >= 56, "ShB wrong msg len");  // <= FOUND

```
['[517](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L517-L524)']
```solidity
517:             
518: 
519:             
520: 
521:             
522:             
523:             
524:             require(_l2ToL1message.length == 76, "ShB wrong msg len 2"); // <= FOUND

```
['[563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563-L563)']
```solidity
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep"); // <= FOUND

```
['[564](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L564-L564)']
```solidity
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2"); // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46-L46)']
```solidity
46:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin"); // <= FOUND

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62-L62)']
```solidity
62:         require(msg.sender == currentPendingAdmin, "n42");  // <= FOUND

```
['[83](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L83-L86)']
```solidity
83:         require( // <= FOUND
84:             !stateTransitionManagerIsRegistered[_stateTransitionManager],
85:             "Bridgehub: state transition already registered"
86:         ); // <= FOUND

```
['[93](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L93-L96)']
```solidity
93:         require( // <= FOUND
94:             stateTransitionManagerIsRegistered[_stateTransitionManager],
95:             "Bridgehub: state transition not registered yet"
96:         ); // <= FOUND

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L102-L102)']
```solidity
102:         require(!tokenIsRegistered[_token], "Bridgehub: token already registered"); // <= FOUND

```
['[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122-L122)']
```solidity
122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0"); // <= FOUND

```
['[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123-L123)']
```solidity
123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large"); // <= FOUND

```
['[125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L125-L128)']
```solidity
125:         require( // <= FOUND
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         ); // <= FOUND

```
['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L129-L129)']
```solidity
129:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered"); // <= FOUND

```
['[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L130-L130)']
```solidity
130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set"); // <= FOUND

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132-L132)']
```solidity
132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered"); // <= FOUND

```
['[223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L223-L223)']
```solidity
223:                 require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1"); // <= FOUND

```
['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225-L225)']
```solidity
225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value"); // <= FOUND

```
['[269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L269-L272)']
```solidity
269:                 require( // <= FOUND
270:                     msg.value == _request.mintValue + _request.secondBridgeValue,
271:                     "Bridgehub: msg.value mismatch 2"
272:                 ); // <= FOUND

```
['[275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L275-L275)']
```solidity
275:                 require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3"); // <= FOUND

```
['[296](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L296-L296)']
```solidity
296:         require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch"); // <= FOUND

```
['[300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L300-L303)']
```solidity
300:         require( // <= FOUND
301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302:             "Bridgehub: second bridge address too low"
303:         );  // <= FOUND

```
['[42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42-L42)']
```solidity
42:         require(_admin != address(0), "Admin should be non zero address"); // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59-L59)']
```solidity
59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function"); // <= FOUND

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65-L65)']
```solidity
65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function"); // <= FOUND

```
['[71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L74)']
```solidity
71:         require( // <= FOUND
72:             msg.sender == owner() || msg.sender == securityCouncil,
73:             "Only the owner and security council are allowed to call this function"
74:         ); // <= FOUND

```
['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L155-L155)']
```solidity
155:         require(isOperationPending(_id), "Operation must be pending"); // <= FOUND

```
['[172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L172-L173)']
```solidity
172:         
173:         require(isOperationReady(id), "Operation must be ready before execution"); // <= FOUND

```
['[177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L177-L179)']
```solidity
177:         
178:         
179:         require(isOperationReady(id), "Operation must be ready after execution"); // <= FOUND

```
['[191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L191-L192)']
```solidity
191:         
192:         require(isOperationPending(id), "Operation must be pending before execution"); // <= FOUND

```
['[196](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L196-L198)']
```solidity
196:         
197:         
198:         require(isOperationPending(id), "Operation must be pending after execution"); // <= FOUND

```
['[216](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L216-L216)']
```solidity
216:         require(!isOperation(_id), "Operation with this proposal id already exists"); // <= FOUND

```
['[217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L217-L217)']
```solidity
217:         require(_delay >= minDelay, "Proposed delay is less than minimum delay"); // <= FOUND

```
['[240](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240-L240)']
```solidity
240:         require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed"); // <= FOUND

```
['[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64-L64)']
```solidity
64:         require(msg.sender == bridgehub, "StateTransition: only bridgehub"); // <= FOUND

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L82-L82)']
```solidity
82:         require(_initializeData.governor != address(0), "StateTransition: governor zero"); // <= FOUND

```
['[256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L256-L256)']
```solidity
256:         require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch"); // <= FOUND

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62-L62)']
```solidity
62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin"); // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L68)']
```solidity
68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator"); // <= FOUND

```
['[195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L195-L200)']
```solidity
195:                 
196:                 
197:                 
198:                 
199: 
200:                 require(block.timestamp >= commitBatchTimestamp + delay, "5c");  // <= FOUND

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L25-L25)']
```solidity
25:         require(address(_initializeData.verifier) != address(0), "vt"); // <= FOUND

```
['[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L26-L26)']
```solidity
26:         require(_initializeData.admin != address(0), "vy"); // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L27-L27)']
```solidity
27:         require(_initializeData.validatorTimelock != address(0), "hc"); // <= FOUND

```
['[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L28-L28)']
```solidity
28:         require(_initializeData.priorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "vu"); // <= FOUND

```
['[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L14-L16)']
```solidity
14:         
15:         
16:         require(_chainId == block.chainid, "pr"); // <= FOUND

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25-L28)']
```solidity
25:         
26:         
27:         
28:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut"); // <= FOUND

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30-L30)']
```solidity
30:         require(facetAddress != address(0), "F");  // <= FOUND

```
['[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31-L31)']
```solidity
31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1");  // <= FOUND

```
['[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34-L34)']
```solidity
34:         require(msg.sender == pendingAdmin, "n4");  // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L59-L59)']
```solidity
59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5"); // <= FOUND

```
['[70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L70-L72)']
```solidity
70:         
71:         
72:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6"); // <= FOUND

```
['[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90-L90)']
```solidity
90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis");  // <= FOUND

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105-L108)']
```solidity
105:         require( // <= FOUND
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         ); // <= FOUND

```
['[110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L110-L113)']
```solidity
110:         require( // <= FOUND
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         ); // <= FOUND

```
['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L116-L119)']
```solidity
116:         require( // <= FOUND
117:             s.protocolVersion > _oldProtocolVersion,
118:             "StateTransition: protocolVersion mismatch in STC after upgrading"
119:         ); // <= FOUND

```
['[136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L136-L136)']
```solidity
136:         require(!diamondStorage.isFrozen, "a9");  // <= FOUND

```
['[146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L146-L146)']
```solidity
146:         require(diamondStorage.isFrozen, "a7");  // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L37-L37)']
```solidity
37:         require(_newBatch.batchNumber == _previousBatch.batchNumber + 1, "f");  // <= FOUND

```
['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L40-L40)']
```solidity
40:         require(pubdataSource == uint8(PubdataSource.Calldata) || pubdataSource == uint8(PubdataSource.Blob), "us"); // <= FOUND

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50-L51)']
```solidity
50:             
51:             require(logOutput.pubdataHash == 0x00, "v0h"); // <= FOUND

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L51-L51)']
```solidity
51:             require(_newBatch.pubdataCommitments.length == 1); // <= FOUND

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61-L66)']
```solidity
61:             
62:             require( // <= FOUND
63:                 logOutput.pubdataHash ==
64:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]),
65:                 "wp"
66:             ); // <= FOUND

```
['[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L74-L74)']
```solidity
74:         require(_previousBatch.batchHash == logOutput.previousBatchHash, "l"); // <= FOUND

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L76-L77)']
```solidity
76:         
77:         require(logOutput.chainedPriorityTxsHash == _newBatch.priorityOperationsHash, "t"); // <= FOUND

```
['[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L78-L79)']
```solidity
78:         
79:         require(logOutput.numberOfLayer1Txs == _newBatch.numberOfLayer1Txs, "ta"); // <= FOUND

```
['[110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L110-L110)']
```solidity
110:         require(batchTimestamp == _expectedBatchTimestamp, "tb"); // <= FOUND

```
['[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L114-L116)']
```solidity
114:         
115:         
116:         require(_previousBatchTimestamp < batchTimestamp, "h3"); // <= FOUND

```
['[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L122-L126)']
```solidity
122:         
123:         
124:         
125:         
126:         require(block.timestamp - COMMIT_TIMESTAMP_NOT_OLDER <= batchTimestamp, "h1");  // <= FOUND

```
['[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L123-L123)']
```solidity
123:         require(lastL2BlockTimestamp <= block.timestamp + COMMIT_TIMESTAMP_APPROXIMATION_DELTA, "h2");  // <= FOUND

```
['[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L149-L150)']
```solidity
149:             
150:             require(!_checkBit(processedLogs, uint8(logKey)), "kp"); // <= FOUND

```
['[154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L154-L154)']
```solidity
154:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm"); // <= FOUND

```
['[157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L157-L157)']
```solidity
157:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln"); // <= FOUND

```
['[160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L160-L160)']
```solidity
160:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb"); // <= FOUND

```
['[163](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L163-L163)']
```solidity
163:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc"); // <= FOUND

```
['[166](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L166-L166)']
```solidity
166:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv"); // <= FOUND

```
['[169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L169-L169)']
```solidity
169:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl"); // <= FOUND

```
['[172](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L172-L172)']
```solidity
172:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk"); // <= FOUND

```
['[175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L175-L175)']
```solidity
175:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc"); // <= FOUND

```
['[178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L178-L178)']
```solidity
178:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd"); // <= FOUND

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L181-L181)']
```solidity
181:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu"); // <= FOUND

```
['[182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L182-L182)']
```solidity
182:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut"); // <= FOUND

```
['[192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L192-L192)']
```solidity
192:             require(processedLogs == 511, "b7"); // <= FOUND

```
['[194](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L194-L194)']
```solidity
194:             require(processedLogs == 1023, "b8"); // <= FOUND

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226-L236)']
```solidity
226:         
227:         
228:         
229:         
230:         
231:         
232:         
233:         require( // <= FOUND
234:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
235:             "Executor facet: wrong protocol version"
236:         ); // <= FOUND

```
['[231](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L231-L232)']
```solidity
231:         
232:         require(_newBatchesData.length == 1, "e4"); // <= FOUND

```
['[233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233-L234)']
```solidity
233:         
234:         require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i");  // <= FOUND

```
['[284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284-L290)']
```solidity
284:         
285:         
286:         
287: 
288:         
289:         
290:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik"); // <= FOUND

```
['[323](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L323-L323)']
```solidity
323:         require(currentBatchNumber == s.totalBatchesExecuted + _executedBatchIdx + 1, "k");  // <= FOUND

```
['[324](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L324-L327)']
```solidity
324:         require( // <= FOUND
325:             _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber],
326:             "exe10" 
327:         ); // <= FOUND

```
['[330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L330-L330)']
```solidity
330:         require(priorityOperationsHash == _storedBatch.priorityOperationsHash, "x");  // <= FOUND

```
['[358](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L358-L358)']
```solidity
358:         require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n");  // <= FOUND

```
['[402](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402-L403)']
```solidity
402:         
403:         require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1"); // <= FOUND

```
['[407](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407-L410)']
```solidity
407:             require( // <= FOUND
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409:                 "o1"
410:             ); // <= FOUND

```
['[421](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L421-L421)']
```solidity
421:         require(currentTotalBatchesVerified <= s.totalBatchesCommitted, "q"); // <= FOUND

```
['[442](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L442-L443)']
```solidity
442:         
443:         require(proofPublicInput.length == 1, "t4"); // <= FOUND

```
['[449](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L449-L449)']
```solidity
449:         require(successVerifyProof, "p");  // <= FOUND

```
['[482](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L482-L482)']
```solidity
482:         require(s.totalBatchesCommitted > _newLastBatch, "v1");  // <= FOUND

```
['[483](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L483-L483)']
```solidity
483:         require(_newLastBatch >= s.totalBatchesExecuted, "v2");  // <= FOUND

```
['[543](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L543-L543)']
```solidity
543:         require(_batch.systemLogs.length <= MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, "pu"); // <= FOUND

```
['[567](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L567-L569)']
```solidity
567:         
568:         
569:         require(_blobCommitments.length == MAX_NUMBER_OF_BLOBS, "b10"); // <= FOUND

```
['[568](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L568-L568)']
```solidity
568:         require(_blobHashes.length == MAX_NUMBER_OF_BLOBS, "b11"); // <= FOUND

```
['[616](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L616-L618)']
```solidity
616:         
617:         
618:         require(success, "failed to call point evaluation precompile"); // <= FOUND

```
['[618](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L618-L618)']
```solidity
618:         require(result == BLS_MODULUS, "precompile unexpected output"); // <= FOUND

```
['[631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631-L631)']
```solidity
631:         require(_pubdataCommitments.length > 0, "pl"); // <= FOUND

```
['[632](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L632-L632)']
```solidity
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd"); // <= FOUND

```
['[633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633-L633)']
```solidity
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs"); // <= FOUND

```
['[639](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L639-L639)']
```solidity
639:             require(blobVersionedHash != bytes32(0), "vh"); // <= FOUND

```
['[663](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L663-L663)']
```solidity
663:         require(versionedHash == bytes32(0), "lh"); // <= FOUND

```
['[668](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L672)']
```solidity
668:             require( // <= FOUND
669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) ||
670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)),
671:                 "bh"
672:             ); // <= FOUND

```
['[681](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L681-L681)']
```solidity
681:         require(success, "vc"); // <= FOUND

```
['[183](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L183-L183)']
```solidity
183:         require(ds.selectorToFacet[_selector].facetAddress != address(0), "g2"); // <= FOUND

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L39-L39)']
```solidity
39:         require(s.chainId == ERA_CHAIN_ID, "transferEthToSharedBridge only available for Era on mailbox"); // <= FOUND

```
['[110](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L110-L110)']
```solidity
110:         require(_batchNumber <= s.totalBatchesExecuted, "xx"); // <= FOUND

```
['[117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L117-L119)']
```solidity
117:         
118:         
119:         require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw"); // <= FOUND

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L158)']
```solidity
158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set"); // <= FOUND

```
['[185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185-L185)']
```solidity
185:         require(s.chainId == ERA_CHAIN_ID, "finalizeEthWithdrawal only available for Era on mailbox"); // <= FOUND

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L206-L206)']
```solidity
206:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token"); // <= FOUND

```
['[243](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L243-L248)']
```solidity
243:         
244:         
245:         
246:         
247:         
248:         require(_request.l2GasPerPubdataByteLimit == REQUIRED_L2_GAS_PRICE_PER_PUBDATA, "qp"); // <= FOUND

```
['[264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L264-L264)']
```solidity
264:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj"); // <= FOUND

```
['[272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L272-L272)']
```solidity
272:         require(_mintValue >= baseCost + _params.l2Value, "mv");  // <= FOUND

```
['[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16-L16)']
```solidity
16:         require(msg.sender == s.admin, "StateTransition Chain: not admin"); // <= FOUND

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L22)']
```solidity
22:         require(s.validators[msg.sender], "StateTransition Chain: not validator"); // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27-L27)']
```solidity
27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager"); // <= FOUND

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32-L32)']
```solidity
32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub"); // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L40)']
```solidity
37:         require( // <= FOUND
38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager,
39:             "StateTransition Chain: Only by admin or state transition manager"
40:         ); // <= FOUND

```
['[45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L48)']
```solidity
45:         require( // <= FOUND
46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47:             "StateTransition Chain: Only by validator or state transition manager"
48:         ); // <= FOUND

```
['[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53-L53)']
```solidity
53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function"); // <= FOUND

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L52-L56)']
```solidity
52:         
53:         
54:         
55:         
56:         require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet"); // <= FOUND

```
['[190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L190-L190)']
```solidity
190:         require(_l2ProtocolUpgradeTx.txType == SYSTEM_UPGRADE_L2_TX_TYPE, "L2 system upgrade tx type is wrong"); // <= FOUND

```
['[205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L205-L210)']
```solidity
205:         
206:         
207:         require( // <= FOUND
208:             _l2ProtocolUpgradeTx.nonce == _newProtocolVersion,
209:             "The new protocol version should be included in the L2 system upgrade tx"
210:         ); // <= FOUND

```
['[223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223-L223)']
```solidity
223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps"); // <= FOUND

```
['[224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L224-L224)']
```solidity
224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32"); // <= FOUND

```
['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L227-L230)']
```solidity
227:             require( // <= FOUND
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229:                 "Wrong factory dep hash"
230:             ); // <= FOUND

```
['[238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L241)']
```solidity
238:         require( // <= FOUND
239:             _newProtocolVersion > previousProtocolVersion,
240:             "New protocol version is not greater than the current one"
241:         ); // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L27-L30)']
```solidity
27:         require( // <= FOUND
28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:             "Too big protocol version difference"
30:         ); // <= FOUND

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33-L35)']
```solidity
33:         
34:         
35:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized"); // <= FOUND

```
['[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L37)']
```solidity
34:         require( // <= FOUND
35:             s.l2SystemContractsUpgradeBatchNumber == 0,
36:             "The batch number of the previous upgrade has not been cleaned"
37:         ); // <= FOUND

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22-L26)']
```solidity
22:         require( // <= FOUND
23:             
24:             _newProtocolVersion >= previousProtocolVersion,
25:             "New protocol version is not greater than the current one"
26:         ); // <= FOUND

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33-L34)']
```solidity
33:         
34:         require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized"); // <= FOUND

```
['[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107-L107)']
```solidity
107:             require(selectors.length > 0, "B");  // <= FOUND

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132-L135)']
```solidity
132:         
133:         
134:         
135:         require(_facet.code.length > 0, "G"); // <= FOUND

```
['[141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L141-L141)']
```solidity
141:             require(oldFacet.facetAddress == address(0), "J");  // <= FOUND

```
['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155-L158)']
```solidity
155:         
156:         
157:         
158:         require(_facet.code.length > 0, "K"); // <= FOUND

```
['[161](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L161-L161)']
```solidity
161:             require(oldFacet.facetAddress != address(0), "L");  // <= FOUND

```
['[175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L175-L175)']
```solidity
175:         require(_facet == address(0), "a1");  // <= FOUND

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L181-L181)']
```solidity
181:             require(oldFacet.facetAddress != address(0), "a2");  // <= FOUND

```
['[215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L215-L215)']
```solidity
215:             require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1"); // <= FOUND

```
['[280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280-L280)']
```solidity
280:             require(_calldata.length == 0, "H");  // <= FOUND

```
['[297](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L297-L299)']
```solidity
297:             
298:             
299:             require(data.length == 32, "lp"); // <= FOUND

```
['[298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L298-L298)']
```solidity
298:             require(abi.decode(data, (bytes32)) == DIAMOND_INIT_SUCCESS_RETURN_VALUE, "lp1"); // <= FOUND

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24-L24)']
```solidity
24:         require(pathLength > 0, "xc"); // <= FOUND

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L25-L25)']
```solidity
25:         require(pathLength < 256, "bt"); // <= FOUND

```
['[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L26-L26)']
```solidity
26:         require(_index < (1 << pathLength), "px"); // <= FOUND

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L65-L65)']
```solidity
65:         require(!_queue.isEmpty(), "D");  // <= FOUND

```
['[73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L73-L73)']
```solidity
73:         require(!_queue.isEmpty(), "s");  // <= FOUND

```
['[28](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L28-L29)']
```solidity
28:         
29:         require(l2GasForTxBody <= _priorityTxMaxGasLimit, "ui"); // <= FOUND

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L30-L31)']
```solidity
30:         
31:         require(l2GasForTxBody / _transaction.gasPerPubdataByteLimit <= _priorityTxMaxPubdata, "uk"); // <= FOUND

```
['[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L34-L43)']
```solidity
34:         
35:         
36:         require( // <= FOUND
37:             getMinimalPriorityTransactionGasLimit(
38:                 _encoded.length,
39:                 _transaction.factoryDeps.length,
40:                 _transaction.gasPerPubdataByteLimit
41:             ) <= l2GasForTxBody,
42:             "up"
43:         ); // <= FOUND

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48-L49)']
```solidity
48:         
49:         require(_transaction.from <= type(uint16).max, "ua"); // <= FOUND

```
['[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49-L49)']
```solidity
49:         require(_transaction.to <= type(uint160).max, "ub"); // <= FOUND

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50-L50)']
```solidity
50:         require(_transaction.paymaster == 0, "uc"); // <= FOUND

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51-L51)']
```solidity
51:         require(_transaction.value == 0, "ud"); // <= FOUND

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52-L52)']
```solidity
52:         require(_transaction.maxFeePerGas == 0, "uq"); // <= FOUND

```
['[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53-L53)']
```solidity
53:         require(_transaction.maxPriorityFeePerGas == 0, "ux"); // <= FOUND

```
['[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54-L54)']
```solidity
54:         require(_transaction.reserved[0] == 0, "ue"); // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55-L55)']
```solidity
55:         require(_transaction.reserved[1] <= type(uint160).max, "uf"); // <= FOUND

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56-L56)']
```solidity
56:         require(_transaction.reserved[2] == 0, "ug"); // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57-L57)']
```solidity
57:         require(_transaction.reserved[3] == 0, "uo"); // <= FOUND

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58-L58)']
```solidity
58:         require(_transaction.signature.length == 0, "uh"); // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59-L59)']
```solidity
59:         require(_transaction.paymasterInput.length == 0, "ul1"); // <= FOUND

```
['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60-L60)']
```solidity
60:         require(_transaction.reservedDynamic.length == 0, "um"); // <= FOUND

```
['[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L115-L115)']
```solidity
115:         require(_totalGasLimit >= overhead, "my");  // <= FOUND

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58-L59)']
```solidity
58:         
59:         require(lockSlotOldValue == 0, "1B"); // <= FOUND

```
['[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L75-L76)']
```solidity
75:         
76:         require(_status == _NOT_ENTERED, "r1"); // <= FOUND

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35-L35)']
```solidity
35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract"); // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L37-L38)']
```solidity
37:         
38:         require(Utils.isContractConstructing(_hash), "Code hash is not for a contract on constructor"); // <= FOUND

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L48-L49)']
```solidity
48:         
49:         require(Utils.isContractConstructed(_hash), "Code hash is not for a constructed contract"); // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L57-L57)']
```solidity
57:         require(Utils.isContractConstructing(codeHash), "Code hash is not for a contract on constructor"); // <= FOUND

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L92-L92)']
```solidity
92:             require(vInt == 27 || vInt == 28, "Invalid v value"); // <= FOUND

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22-L22)']
```solidity
22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER"); // <= FOUND

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24-L24)']
```solidity
24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA"); // <= FOUND

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L51-L54)']
```solidity
51:             require( // <= FOUND
52:                 encodedData.length * 4 == _bytecode.length,
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             ); // <= FOUND

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L56-L59)']
```solidity
56:             require( // <= FOUND
57:                 dictionary.length / 8 <= encodedData.length / 2,
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             ); // <= FOUND

```
['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L63-L63)']
```solidity
63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds"); // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L68-L68)']
```solidity
68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode"); // <= FOUND

```
['[119](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L119-L122)']
```solidity
119:         
120:         
121:         
122:         require(_enumerationIndexSize <= MAX_ENUMERATION_INDEX_SIZE, "enumeration index size is too large"); // <= FOUND

```
['[140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L140-L140)']
```solidity
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch"); // <= FOUND

```
['[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L156-L156)']
```solidity
156:         require(numInitialWritesProcessed == numberOfInitialWrites, "Incorrect number of initial storage diffs"); // <= FOUND

```
['[171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L171-L171)']
```solidity
171:             require(enumIndex == compressedEnumIndex, "rw: enum key mismatch"); // <= FOUND

```
['[187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L187-L187)']
```solidity
187:         require(stateDiffPtr == _compressedStateDiffs.length, "Extra data in _compressedStateDiffs"); // <= FOUND

```
['[230](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L230-L230)']
```solidity
230:                 require(convertedValue == _finalValue, "transform or no compression: compressed and final mismatch"); // <= FOUND

```
['[232](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L232-L235)']
```solidity
232:                 require( // <= FOUND
233:                     _initialValue + convertedValue == _finalValue,
234:                     "add: initial plus converted not equal to final"
235:                 ); // <= FOUND

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L237-L240)']
```solidity
237:                 require( // <= FOUND
238:                     _initialValue - convertedValue == _finalValue,
239:                     "sub: initial minus converted not equal to final"
240:                 ); // <= FOUND

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29-L29)']
```solidity
29:         require(msg.sender == address(this), "Callable only by self"); // <= FOUND

```
['[77](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L77-L81)']
```solidity
77:         require( // <= FOUND
78:             _nonceOrdering == AccountNonceOrdering.Arbitrary &&
79:                 currentInfo.nonceOrdering == AccountNonceOrdering.Sequential,
80:             "It is only possible to change from sequential to arbitrary ordering"
81:         ); // <= FOUND

```
['[239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L239-L242)']
```solidity
239:         require( // <= FOUND
240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
241:             "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:         ); // <= FOUND

```
['[251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L251-L251)']
```solidity
251:         require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments"); // <= FOUND

```
['[264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L264-L264)']
```solidity
264:         require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero"); // <= FOUND

```
['[265](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L265-L265)']
```solidity
265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space"); // <= FOUND

```
['[268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L268-L272)']
```solidity
268:         
269:         require( // <= FOUND
270:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0,
271:             "Code hash is non-zero"
272:         ); // <= FOUND

```
['[273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L273-L274)']
```solidity
273:         
274:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied"); // <= FOUND

```
['[303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L303-L303)']
```solidity
303:         require(knownCodeMarker > 0, "The code hash is not known"); // <= FOUND

```
['[350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350-L350)']
```solidity
350:             require(value == 0, "The value must be zero if we do not call the constructor"); // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100-L100)']
```solidity
100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value"); // <= FOUND

```
['[160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L160-L160)']
```solidity
160:         require(_signature.length == 65, "Signature length is incorrect"); // <= FOUND

```
['[173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L173-L173)']
```solidity
173:         require(v == 27 || v == 28, "v is neither 27 nor 28"); // <= FOUND

```
['[184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L184-L193)']
```solidity
184:         
185:         
186:         
187:         
188:         
189:         
190:         
191:         
192:         
193:         require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s"); // <= FOUND

```
['[202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L202-L202)']
```solidity
202:         require(success, "Failed to pay the fee to the operator"); // <= FOUND

```
['[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20-L20)']
```solidity
20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor"); // <= FOUND

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76-L76)']
```solidity
76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash"); // <= FOUND

```
['[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L78-L78)']
```solidity
78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd"); // <= FOUND

```
['[201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L201-L201)']
```solidity
201:         require(numberOfL2ToL1Logs <= L2_TO_L1_LOGS_MERKLE_TREE_LEAVES, "Too many L2->L1 logs"); // <= FOUND

```
['[214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L214-L217)']
```solidity
214:         require( // <= FOUND
215:             reconstructedChainedLogsHash == chainedLogsHash,
216:             "reconstructedChainedLogsHash is not equal to chainedLogsHash"
217:         ); // <= FOUND

```
['[245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L245-L248)']
```solidity
245:         require( // <= FOUND
246:             reconstructedChainedMessagesHash == chainedMessagesHash,
247:             "reconstructedChainedMessagesHash is not equal to chainedMessagesHash"
248:         ); // <= FOUND

```
['[269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L269-L272)']
```solidity
269:         require( // <= FOUND
270:             reconstructedChainedL1BytecodesRevealDataHash == chainedL1BytecodesRevealDataHash,
271:             "reconstructedChainedL1BytecodesRevealDataHash is not equal to chainedL1BytecodesRevealDataHash"
272:         ); // <= FOUND

```
['[279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L279-L288)']
```solidity
279:         
280:         
281:         
282:         
283:         
284:         require( // <= FOUND
285:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) ==
286:                 STATE_DIFF_COMPRESSION_VERSION_NUMBER,
287:             "state diff compression version mismatch"
288:         ); // <= FOUND

```
['[298](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L298-L298)']
```solidity
298:         require(calldataPtr <= MAX_ALLOWED_PUBDATA_PER_BATCH, "L1 Messenger pubdata is too long"); // <= FOUND

```
['[315](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L315-L316)']
```solidity
315:         
316:         require(calldataPtr == _totalL2ToL1PubdataAndStateDiffs.length, "Extra data in the totalL2ToL1Pubdata array"); // <= FOUND

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L33-L38)']
```solidity
33:         require( // <= FOUND
34:             msg.sender == MSG_VALUE_SYSTEM_CONTRACT ||
35:                 msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) ||
36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS,
37:             "Only system contracts with special access can call this method"
38:         ); // <= FOUND

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L41-L41)']
```solidity
41:         require(fromBalance >= _amount, "Transfer amount exceeds balance"); // <= FOUND

```
['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L60-L61)']
```solidity
60:         
61:         require(to != address(this), "MsgValueSimulator calls itself"); // <= FOUND

```
['[66](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L66-L66)']
```solidity
66:         require(_value <= MAXIMAL_MIN_NONCE_INCREMENT, "The value for incrementing the nonce is too high"); // <= FOUND

```
['[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L85-L85)']
```solidity
85:         require(_value != 0, "Nonce value cannot be set to 0"); // <= FOUND

```
['[89](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L89-L89)']
```solidity
89:             require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used"); // <= FOUND

```
['[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L115-L115)']
```solidity
115:         require(oldMinNonce == _expectedNonce, "Incorrect nonce"); // <= FOUND

```
['[136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L136-L139)']
```solidity
136:         require( // <= FOUND
137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT),
138:             "Only the contract deployer can increment the deployment nonce"
139:         ); // <= FOUND

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L22-L22)']
```solidity
22:         require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs"); // <= FOUND

```
['[242](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L242-L242)']
```solidity
242:         require(_isFirstInBatch, "Upgrade transaction must be first"); // <= FOUND

```
['[245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L245-L246)']
```solidity
245:         
246:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero"); // <= FOUND

```
['[249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L249-L249)']
```solidity
249:             require(correctPrevBlockHash == _expectedPrevL2BlockHash, "The previous L2 block hash is incorrect"); // <= FOUND

```
['[287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287-L287)']
```solidity
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block"); // <= FOUND

```
['[351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L351-L354)']
```solidity
351:             require( // <= FOUND
352:                 _l2BlockTimestamp >= currentBatchTimestamp,
353:                 "The timestamp of the L2 block must be greater than or equal to the timestamp of the current batch"
354:             ); // <= FOUND

```
['[355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355-L355)']
```solidity
355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch"); // <= FOUND

```
['[367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L367-L367)']
```solidity
367:             require(!_isFirstInBatch, "Can not reuse L2 block number from the previous batch"); // <= FOUND

```
['[368](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L368-L368)']
```solidity
368:             require(currentL2BlockTimestamp == _l2BlockTimestamp, "The timestamp of the same L2 block must be same"); // <= FOUND

```
['[369](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L369-L372)']
```solidity
369:             require( // <= FOUND
370:                 _expectedPrevL2BlockHash == _getLatest257L2blockHash(_l2BlockNumber - 1),
371:                 "The previous hash of the same L2 block must be same"
372:             ); // <= FOUND

```
['[373](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L373-L373)']
```solidity
373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock"); // <= FOUND

```
['[385](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L385-L385)']
```solidity
385:             require(_expectedPrevL2BlockHash == pendingL2BlockHash, "The current L2 block hash is incorrect"); // <= FOUND

```
['[386](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L386-L389)']
```solidity
386:             require( // <= FOUND
387:                 _l2BlockTimestamp > currentL2BlockTimestamp,
388:                 "The timestamp of the new L2 block must be greater than the timestamp of the previous L2 block"
389:             ); // <= FOUND

```
['[413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413-L414)']
```solidity
413:         
414:         require(currentBatchNumber > 0, "The current batch number must be greater than 0"); // <= FOUND

```
['[429](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L429-L432)']
```solidity
429:         require( // <= FOUND
430:             _newTimestamp > currentBlockTimestamp,
431:             "The timestamp of the batch must be greater than the timestamp of the previous block"
432:         ); // <= FOUND

```
['[451](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L451-L451)']
```solidity
451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental"); // <= FOUND

```
['[452](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452-L452)']
```solidity
452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct"); // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L46-L50)']
```solidity
46:         
47:         
48:         
49:         
50:         require(_maxTotalGas >= gasleft(), "Gas limit is too low"); // <= FOUND

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L76-L78)']
```solidity
76:             
77:             
78:             require(pubdataAllowance + gasleft() >= pubdataCost + CALL_RETURN_OVERHEAD, "Not enough gas for pubdata"); // <= FOUND

```
['[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L38-L38)']
```solidity
38:         require(returnData.length == 32, "keccak256 returned invalid data"); // <= FOUND

```
['[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L47-L47)']
```solidity
47:         require(returnData.length == 32, "sha returned invalid data"); // <= FOUND

```
['[319](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L319-L319)']
```solidity
319:         require(index < 10, "There are only 10 accessible registers"); // <= FOUND

```
['[350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L350-L350)']
```solidity
350:         require(precompileCallSuccess, "Failed to charge gas"); // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L27-L27)']
```solidity
27:         require(_x <= type(uint32).max, "Overflow"); // <= FOUND

```
['[363](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L363-L363)']
```solidity
363:         require(_transaction.paymasterInput.length >= 4, "The standard paymaster input must be at least 4 bytes long"); // <= FOUND

```
['[367](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L367-L370)']
```solidity
367:             require( // <= FOUND
368:                 _transaction.paymasterInput.length >= 68,
369:                 "The approvalBased paymaster input must be at least 68 bytes long"
370:             ); // <= FOUND

```
['[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L21-L21)']
```solidity
21:         require(_x <= type(uint128).max, "Overflow"); // <= FOUND

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L33-L33)']
```solidity
33:         require(_x <= type(uint24).max, "Overflow"); // <= FOUND

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84-L85)']
```solidity
84:         
85:         require(_bytecode.length % 32 == 0, "po"); // <= FOUND

```
['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L87-L87)']
```solidity
87:         require(lengthInWords < 2 ** 16, "pp");  // <= FOUND

```
['[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L88-L88)']
```solidity
88:         require(lengthInWords % 2 == 1, "pr");  // <= FOUND

```
['[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21-L24)']
```solidity
21:         require( // <= FOUND
22:             SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender),
23:             "This method require system call flag"
24:         ); // <= FOUND

```
['[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L31-L34)']
```solidity
31:         require( // <= FOUND
32:             SystemContractHelper.isSystemContract(msg.sender),
33:             "This method require the caller to be system contract"
34:         ); // <= FOUND

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41-L41)']
```solidity
41:         require(msg.sender == caller, "Inappropriate caller"); // <= FOUND

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48-L48)']
```solidity
48:         require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader"); // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55-L55)']
```solidity
55:         require(msg.sender == FORCE_DEPLOYER); // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55-L55)']
```solidity
55:         require(_l1Bridge != address(0), "bf"); // <= FOUND

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L56-L56)']
```solidity
56:         require(_l2TokenProxyBytecodeHash != bytes32(0), "df"); // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L57-L57)']
```solidity
57:         require(_aliasedOwner != address(0), "sf"); // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L68-L68)']
```solidity
68:             require(_l1LegecyBridge != address(0), "bf2"); // <= FOUND

```
['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87-L92)']
```solidity
87:         
88:         require( // <= FOUND
89:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
90:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
91:             "mq"
92:         ); // <= FOUND

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92-L92)']
```solidity
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge"); // <= FOUND

```
['[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L98-L98)']
```solidity
98:             require(deployedToken == expectedL2Token, "mt"); // <= FOUND

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L101-L101)']
```solidity
101:             require(currentL1Token == _l1Token, "gg");  // <= FOUND

```
['[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124-L124)']
```solidity
124:         require(_amount > 0, "Amount cannot be zero"); // <= FOUND

```
['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L129-L129)']
```solidity
129:         require(l1Token != address(0), "yh"); // <= FOUND

```
['[176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L176-L177)']
```solidity
176:         
177:         require(success, "mk"); // <= FOUND

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L51-L51)']
```solidity
51:         require(_l1Address != address(0), "in6");  // <= FOUND

```
['[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120-L120)']
```solidity
120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt"); // <= FOUND

```
['[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130-L130)']
```solidity
130:         require(msg.sender == l2Bridge, "xnt");  // <= FOUND

```
['[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L137-L139)']
```solidity
137:         
138:         
139:         require(_version == _getInitializedVersion() + 1, "v"); // <= FOUND

```


</details>

## [Gas-41] Where a value is casted more than once, consider caching the result to save gas

### Resolution 
Casting values multiple times in Solidity can be gas-inefficient. When a value undergoes repeated type conversions, the EVM must execute additional operations for each cast, consuming more gas than necessary. To optimize for gas efficiency, cache the result of the initial cast in a local variable and reuse it, rather than performing multiple casts. This not only conserves gas but also enhances code readability, reducing potential error points. For example, instead of repeatedly casting an `address` to `uint256`, cast once, store the result in a local variable, and reference that variable in subsequent operations.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L60-L72)']
```solidity
60:     function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) {
61:         unchecked {
62:             if (_len < 56) {
63:                 encoded = new bytes(1);
64:                 encoded[0] = bytes1(uint8(_len + _offset));
65:             } else {
66:                 uint256 hbs = _highestByteSet(uint256(_len)); // <= FOUND
67: 
68:                 encoded = new bytes(hbs + 2);
69:                 encoded[0] = bytes1(uint8(_offset + hbs + 56));
70: 
71:                 uint256 lbs = 31 - hbs;
72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8); // <= FOUND
73: 
74:                 assembly {
75:                     mstore(add(encoded, 0x21), shiftedVal)
76:                 }
77:             }
78:         }
79:     }

```
['[258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L258-L269)']
```solidity
258:     function _nonSystemDeployOnAddress(
259:         bytes32 _bytecodeHash,
260:         address _newAddress,
261:         AccountAbstractionVersion _aaVersion,
262:         bytes calldata _input
263:     ) internal {
264:         require(_bytecodeHash != bytes32(0x0), "BytecodeHash cannot be zero");
265:         require(uint160(_newAddress) > MAX_SYSTEM_CONTRACT_ADDRESS, "Can not deploy contracts in kernel space"); // <= FOUND
266: 
267:         
268:         require(
269:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0, // <= FOUND
270:             "Code hash is non-zero"
271:         );
272:         
273:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied");
274: 
275:         _performDeployOnAddress(_bytecodeHash, _newAddress, _aaVersion, _input);
276:     }

```


</details>

## [Gas-42] Assembly let var only used on once

### Resolution 
If a variable is only once, it makes more sense to use the value the variable holds directly

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L227-L237)']
```solidity
227:         assembly {
228:             
229:             calldatacopy(0, 0, calldatasize())
230:             
231:             let result := call(gas(), contractAddress, 0, 0, calldatasize(), 0, 0) // <= FOUND
232:             
233:             let size := returndatasize()
234:             
235:             returndatacopy(0, 0, size)
236:             
237:             switch result // <= FOUND
238:             case 0 {
239:                 
240:                 revert(0, size)
241:             }
242:             default {
243:                 
244:                 return(0, size)
245:             }
246:         }

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L33-L52)']
```solidity
33:         assembly {
34:             
35:             let ptr := mload(0x40) // <= FOUND
36:             
37:             calldatacopy(ptr, 0, calldatasize()) // <= FOUND
38:             
39:             let result := delegatecall(gas(), facetAddress, ptr, calldatasize(), 0, 0) // <= FOUND
40:             
41:             let size := returndatasize()
42:             
43:             returndatacopy(ptr, 0, size) // <= FOUND
44:             
45:             switch result // <= FOUND
46:             case 0 {
47:                 
48:                 revert(ptr, size) // <= FOUND
49:             }
50:             default {
51:                 
52:                 return(ptr, size) // <= FOUND
53:             }
54:         }

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L30-L33)']
```solidity
30:         assembly {
31:             
32:             let ptr := add(totalBlobs, 0x20) // <= FOUND
33:             calldatacopy(ptr, _pubdata.offset, _pubdata.length) // <= FOUND
34:         }

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L46-L49)']
```solidity
46:             assembly {
47:                 
48:                 let ptr := add(totalBlobs, 0x20) // <= FOUND
49:                 blobHash := keccak256(add(ptr, start), BLOB_SIZE_BYTES) // <= FOUND
50:             }

```


</details>

## [Gas-43] Assembly let var never used

### Resolution 
If a variable is not used, it is redundant and can be removed if safe to do so

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L50-L55)']
```solidity
50:         assembly {
51:             
52:             _isService := and(_isService, 1)
53:             
54:             
55:             let success := call(_isService, callAddr, _key, _value, 0xFFFF, 0, 0) // <= FOUND
56:         }

```


</details>

## [Gas-44] Use assembly to validate msg.sender

### Resolution 
Utilizing assembly for validating `msg.sender` can potentially save gas as it allows for more direct and efficient access to Ethereum’s EVM opcodes, bypassing some of the overhead introduced by Solidity’s higher-level abstractions. However, this practice requires deep expertise in EVM, as incorrect implementation can introduce critical vulnerabilities. It is a trade-off between gas efficiency and code safety.

Num of instances: 31

### Findings 


<details><summary>Click to show findings</summary>

['[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L64-L64)']
```solidity
64:         require(msg.sender == address(sharedBridge), "Not shared bridge"); // <= FOUND

```
['[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69-L69)']
```solidity
69:         require(msg.sender == address(bridgehub), "ShB not BH"); // <= FOUND

```
['[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L76)']
```solidity
75:         require( // <= FOUND
76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY), // <= FOUND
77:             "L1SharedBridge: not bridgehub or era chain"
78:         );

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L84-L84)']
```solidity
84:         require(msg.sender == address(legacyBridge), "ShB not legacy bridge"); // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L46-L46)']
```solidity
46:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin"); // <= FOUND

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L62-L62)']
```solidity
62:         require(msg.sender == currentPendingAdmin, "n42");  // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59-L59)']
```solidity
59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function"); // <= FOUND

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L65-L65)']
```solidity
65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function"); // <= FOUND

```
['[71](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L71-L72)']
```solidity
71:         require( // <= FOUND
72:             msg.sender == owner() || msg.sender == securityCouncil, // <= FOUND
73:             "Only the owner and security council are allowed to call this function"
74:         );

```
['[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L64-L64)']
```solidity
64:         require(msg.sender == bridgehub, "StateTransition: only bridgehub"); // <= FOUND

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L62-L62)']
```solidity
62:         require(msg.sender == stateTransitionManager.getChainAdmin(_chainId), "ValidatorTimelock: only chain admin"); // <= FOUND

```
['[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L34-L34)']
```solidity
34:         require(msg.sender == pendingAdmin, "n4");  // <= FOUND

```
['[16](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L16-L16)']
```solidity
16:         require(msg.sender == s.admin, "StateTransition Chain: not admin"); // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L27-L27)']
```solidity
27:         require(msg.sender == s.stateTransitionManager, "StateTransition Chain: not state transition manager"); // <= FOUND

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L32-L32)']
```solidity
32:         require(msg.sender == s.bridgehub, "StateTransition Chain: not bridgehub"); // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L37-L38)']
```solidity
37:         require( // <= FOUND
38:             msg.sender == s.admin || msg.sender == s.stateTransitionManager, // <= FOUND
39:             "StateTransition Chain: Only by admin or state transition manager"
40:         );

```
['[45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L46)']
```solidity
45:         require( // <= FOUND
46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager, // <= FOUND
47:             "StateTransition Chain: Only by validator or state transition manager"
48:         );

```
['[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L53-L53)']
```solidity
53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function"); // <= FOUND

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L35-L35)']
```solidity
35:         require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract"); // <= FOUND

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L22-L22)']
```solidity
22:         require(msg.sender == FORCE_DEPLOYER, "Can only be called by FORCE_DEPLOYER"); // <= FOUND

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29-L29)']
```solidity
29:         require(msg.sender == address(this), "Callable only by self"); // <= FOUND

```
['[239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L239-L240)']
```solidity
239:         require( // <= FOUND
240:             msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT), // <= FOUND
241:             "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
242:         );

```
['[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L20-L20)']
```solidity
20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor"); // <= FOUND

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L33-L36)']
```solidity
33:         require( // <= FOUND
34:             msg.sender == MSG_VALUE_SYSTEM_CONTRACT || // <= FOUND
35:                 msg.sender == address(DEPLOYER_SYSTEM_CONTRACT) || // <= FOUND
36:                 msg.sender == BOOTLOADER_FORMAL_ADDRESS, // <= FOUND
37:             "Only system contracts with special access can call this method"
38:         );

```
['[136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L136-L137)']
```solidity
136:         require( // <= FOUND
137:             msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), // <= FOUND
138:             "Only the contract deployer can increment the deployment nonce"
139:         );

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L41-L41)']
```solidity
41:         require(msg.sender == caller, "Inappropriate caller"); // <= FOUND

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L48-L48)']
```solidity
48:         require(msg.sender == BOOTLOADER_FORMAL_ADDRESS, "Callable only by the bootloader"); // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L55-L55)']
```solidity
55:         require(msg.sender == FORCE_DEPLOYER); // <= FOUND

```
['[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L120-L120)']
```solidity
120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt"); // <= FOUND

```
['[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L130-L130)']
```solidity
130:         require(msg.sender == l2Bridge, "xnt");  // <= FOUND

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L138-L138)']
```solidity
138:         require(bridgehub.getStateTransition(_chainId) == msg.sender, "receiveEth not state transition"); // <= FOUND

```


</details>

## [Gas-45] Use += for mappings

### Resolution 
Using `+=` for mappings simplifies code and can potentially save gas. When you need to increment a value within a mapping, writing `mappingA[xyz] = mappingA[xyz] + 1;` can be made more concise with `mappingA[xyz] += 1;`.

**Resolution**: To enhance code clarity and potentially reduce gas costs, replace explicit addition assignments with the `+=` operator when dealing with mappings. This not only shortens the code but also makes it easier to read and understand. Employ tools like linters or static analysis to systematically identify and correct such instances, ensuring optimized and cleaner code throughout your smart contract.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L133-L133)']
```solidity
133:             chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount; // <= FOUND

```


</details>

## [Gas-46] Simple checks for zero uint can be done using assembly to save gas

### Resolution 
Using assembly for simple zero checks on unsigned integers can save gas due to lower-level, optimized operations. 

**Resolution**: Implement inline assembly with Solidity's `assembly` block to perform zero checks. Ensure thorough testing and verification, as assembly lacks the safety checks of high-level Solidity, potentially introducing vulnerabilities if not used carefully.

Num of instances: 58

### Findings 


<details><summary>Click to show findings</summary>

['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158-L159)']
```solidity
158:             
159:             require(msg.value == 0, "ShB m.v > 0 b d.it"); // <= FOUND

```
['[200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L200-L200)']
```solidity
200:             require(_depositAmount == 0, "ShB wrong withdraw amount"); // <= FOUND

```
['[202](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202-L202)']
```solidity
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2"); // <= FOUND

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237-L237)']
```solidity
237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap"); // <= FOUND

```
['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L225-L225)']
```solidity
225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value"); // <= FOUND

```
['[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L90-L90)']
```solidity
90:         require(s.totalBatchesCommitted == 0, "AdminFacet: set validium only after genesis");  // <= FOUND

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L50-L51)']
```solidity
50:             
51:             require(logOutput.pubdataHash == 0x00, "v0h"); // <= FOUND

```
['[284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L284-L290)']
```solidity
284:         
285:         
286:         
287: 
288:         
289:         
290:         require(s.l2SystemContractsUpgradeBatchNumber == 0, "ik"); // <= FOUND

```
['[291](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L291-L292)']
```solidity
291:             
292:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0); // <= FOUND

```
['[633](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L633-L633)']
```solidity
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs"); // <= FOUND

```
['[34](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L34-L35)']
```solidity
34:         require(
35:             s.l2SystemContractsUpgradeBatchNumber == 0, // <= FOUND
36:             "The batch number of the previous upgrade has not been cleaned"
37:         );

```
['[280](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L280-L280)']
```solidity
280:             require(_calldata.length == 0, "H");  // <= FOUND

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30-L30)']
```solidity
30:             currentHash = (_index % 2 == 0) // <= FOUND
31:                 ? _efficientHash(currentHash, _path[i])
32:                 : _efficientHash(_path[i], currentHash);

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L50-L50)']
```solidity
50:         require(_transaction.paymaster == 0, "uc"); // <= FOUND

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L51-L51)']
```solidity
51:         require(_transaction.value == 0, "ud"); // <= FOUND

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L52-L52)']
```solidity
52:         require(_transaction.maxFeePerGas == 0, "uq"); // <= FOUND

```
['[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L53-L53)']
```solidity
53:         require(_transaction.maxPriorityFeePerGas == 0, "ux"); // <= FOUND

```
['[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L54-L54)']
```solidity
54:         require(_transaction.reserved[0] == 0, "ue"); // <= FOUND

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L56-L56)']
```solidity
56:         require(_transaction.reserved[2] == 0, "ug"); // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L57-L57)']
```solidity
57:         require(_transaction.reserved[3] == 0, "uo"); // <= FOUND

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L58-L58)']
```solidity
58:         require(_transaction.signature.length == 0, "uh"); // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L59-L59)']
```solidity
59:         require(_transaction.paymasterInput.length == 0, "ul1"); // <= FOUND

```
['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L60-L60)']
```solidity
60:         require(_transaction.reservedDynamic.length == 0, "um"); // <= FOUND

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/ReentrancyGuard.sol#L58-L59)']
```solidity
58:         
59:         require(lockSlotOldValue == 0, "1B"); // <= FOUND

```
['[146](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L146-L146)']
```solidity
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET; // <= FOUND

```
['[268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L268-L270)']
```solidity
268:         
269:         require(
270:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getCodeHash(uint256(uint160(_newAddress))) == 0x0, // <= FOUND
271:             "Code hash is non-zero"
272:         );

```
['[273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L273-L274)']
```solidity
273:         
274:         require(NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(_newAddress) == 0x00, "Account is occupied"); // <= FOUND

```
['[350](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L350-L350)']
```solidity
350:             require(value == 0, "The value must be zero if we do not call the constructor"); // <= FOUND

```
['[373](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L373-L373)']
```solidity
373:             require(_maxVirtualBlocksToCreate == 0, "Can not create virtual blocks in the middle of the miniblock"); // <= FOUND

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L29-L30)']
```solidity
29:                 
30:                 encoded[0] = (_val == 0) ? bytes1(uint8(128)) : bytes1(uint8(_val)); // <= FOUND

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L52-L52)']
```solidity
52:         return _bytecodeHash[1] == 0x00; // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L57-L57)']
```solidity
57:         return _bytecodeHash[1] == 0x01; // <= FOUND

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L84-L85)']
```solidity
84:         
85:         require(_bytecode.length % 32 == 0, "po"); // <= FOUND

```
['[92](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L92-L92)']
```solidity
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge"); // <= FOUND

```
['[141](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L141-L141)']
```solidity
141:         require(_amount != 0, "0T");  // <= FOUND

```
['[186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186-L186)']
```solidity
186:         require(amount != 0, "2T");  // <= FOUND

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L208-L208)']
```solidity
208:         require(amount != 0, "6T");  // <= FOUND

```
['[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L122-L122)']
```solidity
122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0"); // <= FOUND

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L30-L30)']
```solidity
30:         isSystemCall = (mask & MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT) != 0; // <= FOUND

```
['[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L85-L85)']
```solidity
85:         require(_value != 0, "Nonce value cannot be set to 0"); // <= FOUND

```
['[332](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L332-L333)']
```solidity
332:         
333:         return (callFlags & 2) != 0; // <= FOUND

```
['[184](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L184-L193)']
```solidity
184:         
185:         
186:         
187:         
188:         
189:         
190:         
191:         
192:         
193:         require(uint256(s) <= 0x7FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF5D576E7357A4501DDFE92F46681B20A0, "Invalid s"); // <= FOUND

```
['[129](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L129-L129)']
```solidity
129:             require(amount > 0, "ShB: 0 amount to transfer"); // <= FOUND

```
['[327](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L327-L327)']
```solidity
327:         require(_amount > 0, "y1"); // <= FOUND

```
['[593](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L593-L593)']
```solidity
593:         return (_bitMap & (1 << _index)) > 0; // <= FOUND

```
['[631](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631-L631)']
```solidity
631:         require(_pubdataCommitments.length > 0, "pl"); // <= FOUND

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L158-L158)']
```solidity
158:         require(s.baseTokenGasPriceMultiplierDenominator > 0, "Mailbox: baseTokenGasPriceDenominator not set"); // <= FOUND

```
['[107](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L107-L107)']
```solidity
107:             require(selectors.length > 0, "B");  // <= FOUND

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L132-L135)']
```solidity
132:         
133:         
134:         
135:         require(_facet.code.length > 0, "G"); // <= FOUND

```
['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L155-L158)']
```solidity
155:         
156:         
157:         
158:         require(_facet.code.length > 0, "K"); // <= FOUND

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L24-L24)']
```solidity
24:         require(pathLength > 0, "xc"); // <= FOUND

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L24-L24)']
```solidity
24:         require(_delegateTo.code.length > 0, "Delegatee is an EOA"); // <= FOUND

```
['[303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L303-L303)']
```solidity
303:         require(knownCodeMarker > 0, "The code hash is not known"); // <= FOUND

```
['[245](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L245-L246)']
```solidity
245:         
246:         require(_l2BlockNumber > 0, "L2 block number is never expected to be zero"); // <= FOUND

```
['[287](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L287-L287)']
```solidity
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block"); // <= FOUND

```
['[355](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L355-L355)']
```solidity
355:             require(_maxVirtualBlocksToCreate > 0, "There must be a virtual block created at the start of the batch"); // <= FOUND

```
['[413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L413-L414)']
```solidity
413:         
414:         require(currentBatchNumber > 0, "The current batch number must be greater than 0"); // <= FOUND

```
['[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L124-L124)']
```solidity
124:         require(_amount > 0, "Amount cannot be zero"); // <= FOUND

```


</details>

## [Gas-47] Use Unchecked for Divisions on Constant or Immutable Values

### Resolution 
When performing divisions in Solidity, the operation costs gas and includes a check for division by zero. However, if you are dividing by a constant or an immutable value that is guaranteed to be non-zero, this check becomes unnecessary, consuming extra gas without adding safety.

**Resolution**: Utilize the `unchecked` block for divisions involving constant or immutable values that are assuredly non-zero. This bypasses the additional safety checks, optimizing gas usage. Ensure thorough testing and code reviews are conducted to verify the non-zero condition of the denominator, preventing any potential division by zero errors and maintaining contract safety.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L51-L51)']
```solidity
51:         return KECCAK_ROUND_GAS_COST * (_length / KECCAK_ROUND_NUMBER_OF_BYTES + 1); // <= FOUND

```
['[62](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L62-L62)']
```solidity
62:         return SHA256_ROUND_GAS_COST * ((_length + 8) / SHA256_ROUND_NUMBER_OF_BYTES + 1); // <= FOUND

```
['[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L180-L180)']
```solidity
180:         deploymentNonce = _rawMinNonce / DEPLOY_NONCE_MULTIPLIER; // <= FOUND

```


</details>

## [Gas-48] Using nested if to save gas

### Resolution 
Using nested `if` statements instead of logical AND (`&&`) operators can potentially save gas in Solidity contracts. When a series of conditions are connected with `&&`, all conditions must be evaluated even if the first one fails. In contrast, nested `if` statements allow for short-circuiting; if the first condition fails, the rest are skipped, saving gas. This approach is more gas-efficient, especially when dealing with complex or gas-intensive conditions. However, it's crucial to balance gas savings with code readability and maintainability, ensuring that the code remains clear and easy to understand.

Num of instances: 20

### Findings 


<details><summary>Click to show findings</summary>

['[361](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361-L361)']
```solidity
361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) { // <= FOUND
362:             delete s.l2SystemContractsUpgradeTxHash;
363:             delete s.l2SystemContractsUpgradeBatchNumber;
364:         }

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L102-L102)']
```solidity
102:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) { // <= FOUND
103:             codeHash = EMPTY_STRING_KECCAK;
104:         }

```
['[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L139-L139)']
```solidity
139:         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) { // <= FOUND
140:             bytes4 selector = bytes4(data[:4]);
141:             
142:             
143:             isSystemCall =
144:                 selector == DEPLOYER_SYSTEM_CONTRACT.create.selector ||
145:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2.selector ||
146:                 selector == DEPLOYER_SYSTEM_CONTRACT.createAccount.selector ||
147:                 selector == DEPLOYER_SYSTEM_CONTRACT.create2Account.selector;
148:         }

```
['[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L88-L88)']
```solidity
88:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) { // <= FOUND
89:             require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");
90:         }

```
['[169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L169-L169)']
```solidity
169:         if (isUsed && !_shouldBeUsed) { // <= FOUND
170:             revert("Reusing the same nonce twice");
171:         }

```
['[277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277-L277)']
```solidity
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) { // <= FOUND
278:             uint128 currentBatchNumber = currentBatchInfo.number;
279: 
280:             
281:             
282:             
283:             virtualBlockInfo.number = currentBatchNumber;
284:             
285:             virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
286: 
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
288:             _maxVirtualBlocksToCreate -= 1;
289:         }

```
['[360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L360-L360)']
```solidity
360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) { // <= FOUND
361:             
362:             
363:             _upgradeL2Blocks(_l2BlockNumber, _expectedPrevL2BlockHash, _isFirstInBatch);
364: 
365:             _setNewL2BlockData(_l2BlockNumber, _l2BlockTimestamp, _expectedPrevL2BlockHash);
366:         }

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76-L76)']
```solidity
75:         require(
76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY), // <= FOUND
77:             "L1SharedBridge: not bridgehub or era chain"
78:         );

```
['[375](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L375-L375)']
```solidity
375:         return (_chainId == ERA_CHAIN_ID) && (_l2BatchNumber < eraFirstPostUpgradeBatch); // <= FOUND

```
['[361](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361-L361)']
```solidity
361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) { // <= FOUND

```
['[669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669-L670)']
```solidity
668:             require(
669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) || // <= FOUND
670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)), // <= FOUND
671:                 "bh"
672:             );

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L105-L105)']
```solidity
102:         
103:         
104:         
105:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) { // <= FOUND

```
['[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L139-L139)']
```solidity
139:         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) { // <= FOUND

```
['[188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188-L188)']
```solidity
188:         return recoveredAddress == address(this) && recoveredAddress != address(0); // <= FOUND

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L76-L76)']
```solidity
76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash"); // <= FOUND

```
['[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L90-L90)']
```solidity
88:         
89:         
90:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) { // <= FOUND

```
['[169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L169-L169)']
```solidity
169:         if (isUsed && !_shouldBeUsed) { // <= FOUND

```
['[171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L171-L171)']
```solidity
171:         } else if (!isUsed && _shouldBeUsed) { // <= FOUND

```
['[277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277-L277)']
```solidity
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) { // <= FOUND

```
['[360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L360-L360)']
```solidity
360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) { // <= FOUND

```


</details>

## [Gas-49] Consider splitting complex if statements into multiple steps

### Resolution 
Splitting complex checks into multiple steps in smart contracts can enhance readability and potentially save gas. Complex conditions often require more computational power, increasing gas costs. By breaking down these conditions into simpler, individual checks, some computations can be avoided, especially if earlier checks fail, leveraging short-circuit evaluation in logical operations. This approach not only makes the code easier to understand and maintain but can also lead to more efficient execution, as unnecessary computations are minimized. Structuring contracts to evaluate conditions in a step-by-step manner can lead to significant gas savings and improved contract performance.

Num of instances: 14

### Findings 


<details><summary>Click to show findings</summary>

['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L237-L238)']
```solidity
237:         
238:         if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) { // <= FOUND

```
['[229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L229-L229)']
```solidity
229:             if (_operation == 0 || _operation == 3) { // <= FOUND

```
['[144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L144-L151)']
```solidity
144:         
145:         
146:         
147:         
148:         
149:         
150:         
151:         if (blockNumber <= _block || blockNumber - _block > 256) { // <= FOUND

```
['[361](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L361-L361)']
```solidity
361:         if (batchWhenUpgradeHappened != 0 && batchWhenUpgradeHappened <= newTotalBatchesExecuted) { // <= FOUND

```
['[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L147-L153)']
```solidity
147:         
148:         
149:         
150:         
151:         if ( // <= FOUND
152:             _newVerifierParams.recursionNodeLevelVkHash == bytes32(0) && // <= FOUND
153:             _newVerifierParams.recursionLeafLevelVkHash == bytes32(0) && // <= FOUND
154:             _newVerifierParams.recursionCircuitsSetVksHash == bytes32(0)
155:         ) {

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L102-L105)']
```solidity
102:         
103:         
104:         
105:         if (codeHash == 0x00 && NONCE_HOLDER_SYSTEM_CONTRACT.getRawNonce(account) > 0) { // <= FOUND

```
['[131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L131-L141)']
```solidity
131:         
132:         
133:         
134:         
135:         
136:         
137:         
138:         
139:         if ( // <= FOUND
140:             uint160(account) > CURRENT_MAX_PRECOMPILE_ADDRESS && // <= FOUND
141:             codeHash != 0x00 && // <= FOUND
142:             !Utils.isContractConstructing(codeHash)
143:         ) {

```
['[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L47-L49)']
```solidity
47:         
48:         if ( // <= FOUND
49:             _address > address(MAX_SYSTEM_CONTRACT_ADDRESS) && // <= FOUND
50:             ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.getRawCodeHash(_address) == 0
51:         ) {

```
['[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L139-L139)']
```solidity
139:         if (to == address(DEPLOYER_SYSTEM_CONTRACT) && data.length >= 4) { // <= FOUND

```
['[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L88-L90)']
```solidity
88:         
89:         
90:         if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) { // <= FOUND

```
['[169](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L169-L169)']
```solidity
169:         if (isUsed && !_shouldBeUsed) { // <= FOUND

```
['[171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L171-L171)']
```solidity
171:         } else if (!isUsed && _shouldBeUsed) { // <= FOUND

```
['[277](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L277-L277)']
```solidity
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) { // <= FOUND

```
['[360](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L360-L360)']
```solidity
360:         if (currentL2BlockNumber == 0 && currentL2BlockTimestamp == 0) { // <= FOUND

```


</details>

## [Gas-50] Optimize Storage with Byte Truncation for Time Related State Variables

### Resolution 
Storage optimization in Solidity contracts is vital for reducing gas costs, especially when storing time-related state variables. Using `uint32` for storing time values like timestamps is often sufficient, given it can represent dates up to the year 2106. By truncating larger default integer types to `uint32`, you significantly save on storage space and consequently on gas costs for deployment and state modifications. However, ensure that the truncation does not lead to overflow issues and that the variable's size is adequate for the application's expected lifespan and precision requirements. Adopting this optimization practice contributes to more efficient and cost-effective smart contract development.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L22-L22)']
```solidity
22: uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1); // <= FOUND

```


</details>

## [Gas-51] Stack variable cost less than state variables while used in emiting event

### Resolution 
When emitting events in Solidity, using stack variables (local variables within a function) instead of state variables can lead to significant gas savings. Stack variables reside in memory only for the duration of the function execution and are less costly to access compared to state variables, which are stored on the blockchain. When an event is emitted, accessing these stack variables requires less gas than fetching data from state variables, which involves reading from the contract's storage - a more expensive operation. Thus, for efficiency, prefer using local variables within functions for event emission, especially in functions that are called frequently.

Num of instances: 7

### Findings 


<details><summary>Click to show findings</summary>

['[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69-L69)']
```solidity
69:         emit NewAdmin(previousAdmin, pendingAdmin); // <= FOUND

```
['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L227-L227)']
```solidity
227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion); // <= FOUND

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L101-L101)']
```solidity
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_); // <= FOUND

```
['[126](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L126-L126)']
```solidity
126:         emit BridgeInitialize(l1Address, _newName, _newSymbol, decimals_); // <= FOUND

```
['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L40)']
```solidity
40:         emit NewPendingAdmin(pendingAdmin, address(0)); // <= FOUND

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L257-L257)']
```solidity
257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil); // <= FOUND

```
['[250](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L250-L250)']
```solidity
250:         emit ChangeMinDelay(minDelay, _newDelay); // <= FOUND

```


</details>

## [Gas-52] Avoid emitting event on every iteration

### Resolution 
Emitting events within a loop can cause significant gas consumption due to repeated I/O operations. Instead, accumulate changes in memory and emit a single event post-loop with aggregated data. This approach improves contract efficiency, reduces gas costs, and simplifies event tracking for event listeners.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L261)']
```solidity
257:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259: 
260:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:             emit BlockCommit( // <= FOUND
262:                 _lastCommittedBatchData.batchNumber,
263:                 _lastCommittedBatchData.batchHash,
264:                 _lastCommittedBatchData.commitment
265:             );
266:         }

```
['[299](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299-L299)']
```solidity
289:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit( // <= FOUND
300:                 _lastCommittedBatchData.batchNumber,
301:                 _lastCommittedBatchData.batchHash,
302:                 _lastCommittedBatchData.commitment
303:             );
304:         }

```
['[353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353)']
```solidity
351:        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352:             _executeOneBatch(_batchesData[i], i);
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment); // <= FOUND
354:         }

```


</details>

## [Gas-53] Low level call can be optimized with assembly

### Resolution 
Optimizing low-level calls using assembly in Solidity can be beneficial, particularly when dealing with function return data. Typically, even if return data from a low-level call is not used, Solidity still allocates memory to store it, which incurs gas costs. By using assembly, developers can bypass the automatic memory allocation for unused return data. This manual optimization involves handling the call at the assembly level and deliberately choosing not to store the return data in memory when it's not needed.

Num of instances: 7

### Findings 


<details><summary>Click to show findings</summary>

['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226-L226)']
```solidity
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data); // <= FOUND

```
['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L63-L63)']
```solidity
63:             (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call( // <= FOUND
64:                 abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65:             );

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L61-L61)']
```solidity
57:         
58:         
59:         
60:         
61:         bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false); // <= FOUND

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226-L226)']
```solidity
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data); // <= FOUND

```
['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L63-L63)']
```solidity
63:             (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call( // <= FOUND
64:                 abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65:             );

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L57-L61)']
```solidity
57:         
58:         
59:         
60:         
61:         bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false); // <= FOUND

```
['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L63-L63)']
```solidity
63:             (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call( // <= FOUND
64:                 abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65:             );

```


</details>

## [Gas-54] Inline modifiers used only once

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

['[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L74-L74)']
```solidity
74:     modifier onlyBridgehubOrEra(uint256 _chainId) { // <= FOUND
75:         require(
76:             msg.sender == address(bridgehub) || (_chainId == ERA_CHAIN_ID && msg.sender == ERA_DIAMOND_PROXY),
77:             "L1SharedBridge: not bridgehub or era chain"
78:         );
79:         _;
80:     }

```
['[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L64-L64)']
```solidity
64:     modifier onlySecurityCouncil() { // <= FOUND
65:         require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
66:         _;
67:     }

```
['[70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L70-L70)']
```solidity
70:     modifier onlyOwnerOrSecurityCouncil() { // <= FOUND
71:         require(
72:             msg.sender == owner() || msg.sender == securityCouncil,
73:             "Only the owner and security council are allowed to call this function"
74:         );
75:         _;
76:     }

```
['[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L44-L44)']
```solidity
44:     modifier onlyValidatorOrStateTransitionManager() { // <= FOUND
45:         require(
46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager,
47:             "StateTransition Chain: Only by validator or state transition manager"
48:         );
49:         _;
50:     }

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L52-L52)']
```solidity
52:     modifier onlyBaseTokenBridge() { // <= FOUND
53:         require(msg.sender == s.baseTokenBridge, "Only shared bridge can call this function");
54:         _;
55:     }

```
['[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L19-L19)']
```solidity
19:     modifier onlyCompressor() { // <= FOUND
20:         require(msg.sender == address(COMPRESSOR_CONTRACT), "Callable only by the compressor");
21:         _;
22:     }

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L30-L30)']
```solidity
30:     modifier onlyCallFromSystemContract() { // <= FOUND
31:         require(
32:             SystemContractHelper.isSystemContract(msg.sender),
33:             "This method require the caller to be system contract"
34:         );
35:         _;
36:     }

```
['[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L54-L54)']
```solidity
54:     modifier onlyCallFromForceDeployer() { // <= FOUND
55:         require(msg.sender == FORCE_DEPLOYER);
56:         _;
57:     }

```
['[134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L134-L134)']
```solidity
134:     modifier onlyNextVersion(uint8 _version) { // <= FOUND
135:         
136:         
137:         require(_version == _getInitializedVersion() + 1, "v");
138:         _;
139:     }

```


</details>

## [Gas-55] Use s.x = s.x + y instead of s.x += y for state variable structs

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[295](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L295-L295)']
```solidity
295:         virtualBlockInfo.number += _maxVirtualBlocksToCreate; // <= FOUND

```


</details>

## [Gas-56] Use s.x = s.x + y instead of s.x += y for memory structs (same for -= etc)

### Resolution 
In Solidity, optimizing gas usage is crucial, particularly for frequently executed operations. For memory structs, using explicit assignment (e.g., `s.x = s.x + y`) instead of shorthand operations (e.g., `s.x += y`) can result in a minor gas saving, around 100 gas. This difference arises from the way the Solidity compiler optimizes bytecode. While such savings might seem small, they can add up in contracts with high transaction volume. This optimization applies to other compound assignment operators like `-=` and `*=` as well. It's a subtle efficiency gain that developers can leverage, especially in complex contracts where every gas unit counts.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L263-L304)']
```solidity
263:     function _setVirtualBlock(
264:         uint128 _l2BlockNumber,
265:         uint128 _maxVirtualBlocksToCreate,
266:         uint128 _newTimestamp
267:     ) internal {
268:         if (virtualBlockUpgradeInfo.virtualBlockFinishL2Block != 0) {
269:             
270:             
271:             currentVirtualL2BlockInfo = currentL2BlockInfo;
272:             return;
273:         }
274: 
275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo;
276: 
277:         if (currentVirtualL2BlockInfo.number == 0 && virtualBlockInfo.timestamp == 0) { // <= FOUND
278:             uint128 currentBatchNumber = currentBatchInfo.number;
279: 
280:             
281:             
282:             
283:             virtualBlockInfo.number = currentBatchNumber; // <= FOUND
284:             
285:             virtualBlockUpgradeInfo.virtualBlockStartBatch = currentBatchNumber;
286: 
287:             require(_maxVirtualBlocksToCreate > 0, "Can't initialize the first virtual block");
288:             _maxVirtualBlocksToCreate -= 1;
289:         } else if (_maxVirtualBlocksToCreate == 0) {
290:             
291:             
292:             return;
293:         }
294: 
295:         virtualBlockInfo.number += _maxVirtualBlocksToCreate; // <= FOUND
296:         virtualBlockInfo.timestamp = _newTimestamp; // <= FOUND
297: 
298:         
299:         
300:         
301:         
302:         if (virtualBlockInfo.number >= _l2BlockNumber) { // <= FOUND
303:             virtualBlockUpgradeInfo.virtualBlockFinishL2Block = _l2BlockNumber;
304:             virtualBlockInfo.number = _l2BlockNumber; // <= FOUND
305:         }
306: 
307:         currentVirtualL2BlockInfo = virtualBlockInfo;
308:     }

```


</details>

## [Gas-57] Time state variables can be truncated to uint32

### Resolution 
Truncating time-related state variables to `uint32` can be a practical optimization in Solidity contracts. Since `uint32` can represent dates far into the future (over 100 years from now), it's often sufficient for time tracking purposes. This approach reduces the storage space required, thereby saving gas costs associated with larger data types like `uint256`. This form of optimization is especially beneficial in scenarios where space efficiency is a priority and the range of `uint32` meets the application's temporal needs.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L22-L22)']
```solidity
22: uint256 internal constant EXECUTED_PROPOSAL_TIMESTAMP = uint256(1); // <= FOUND

```


</details>

## [Gas-58] Constants are cheaper than Enums

### Resolution 
Using constants instead of enums in Solidity can lead to gas savings. Constants, particularly for primitive data types like `uint` or `bool`, are directly substituted by the Solidity compiler at compile time, effectively hardcoding their values into the bytecode. This means that accessing a constant does not incur any runtime gas costs, as no storage or memory access is needed. In contrast, enums, while useful for readability and ensuring valid value ranges, are stored in contract storage or memory, incurring gas costs for reads and writes. For scenarios where an enum's value range aligns with a simple constant (like true/false or small integer ranges), substituting with constants can be a more gas-efficient choice.

Num of instances: 13

### Findings 


<details><summary>Click to show findings</summary>

['[12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L12-L12)']
```solidity
12: enum UpgradeState { // <= FOUND
13:     None,
14:     Transparent,
15:     Shadow
16: }

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L39-L39)']
```solidity
39: enum PubdataPricingMode { // <= FOUND
40:     Rollup,
41:     Validium
42: }

```
['[8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L8-L8)']
```solidity
8: enum SystemLogKey { // <= FOUND
9:     L2_TO_L1_LOGS_TREE_ROOT_KEY,
10:     TOTAL_L2_TO_L1_PUBDATA_KEY,
11:     STATE_DIFF_HASH_KEY,
12:     PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY,
13:     PREV_BATCH_HASH_KEY,
14:     CHAINED_PRIORITY_TXN_HASH_KEY,
15:     NUMBER_OF_LAYER_1_TXS_KEY,
16:     BLOB_ONE_HASH_KEY,
17:     BLOB_TWO_HASH_KEY,
18:     EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY
19: }

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L22-L22)']
```solidity
22: enum PubdataSource { // <= FOUND
23:     Calldata,
24:     Blob
25: }

```
['[8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L8-L8)']
```solidity
8: enum TxStatus { // <= FOUND
9:     Failure,
10:     Success
11: }

```
['[8](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L8-L8)']
```solidity
8: enum SystemLogKey { // <= FOUND
9:     L2_TO_L1_LOGS_TREE_ROOT_KEY,
10:     TOTAL_L2_TO_L1_PUBDATA_KEY,
11:     STATE_DIFF_HASH_KEY,
12:     PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY,
13:     PREV_BATCH_HASH_KEY,
14:     CHAINED_PRIORITY_TXN_HASH_KEY,
15:     NUMBER_OF_LAYER_1_TXS_KEY,
16:     BLOB_ONE_HASH_KEY,
17:     BLOB_TWO_HASH_KEY,
18:     EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY
19: }

```
['[24](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L24-L24)']
```solidity
24: enum Global { // <= FOUND
25:     CalldataPtr,
26:     CallFlags,
27:     ExtraABIData1,
28:     ExtraABIData2,
29:     ReturndataPtr
30: }

```
['[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L20-L20)']
```solidity
20: enum CalldataForwardingMode { // <= FOUND
21:     UseHeap,
22:     ForwardFatPointer,
23:     UseAuxHeap
24: }

```
['[7](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/interfaces/IPaymaster.sol#L7-L7)']
```solidity
7: enum ExecutionResult { // <= FOUND
8:     Revert,
9:     Success
10: }

```
['[80](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L80-L80)']
```solidity
80:     enum Action { // <= FOUND
81:         Add,
82:         Replace,
83:         Remove
84:     }

```
['[14](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/IGovernance.sol#L14-L14)']
```solidity
14:     enum OperationState { // <= FOUND
15:         Unset,
16:         Waiting,
17:         Ready,
18:         Done
19:     }

```
['[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L11-L11)']
```solidity
11:     enum AccountAbstractionVersion { // <= FOUND
12:         None,
13:         Version1
14:     }

```
['[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/IContractDeployer.sol#L23-L23)']
```solidity
23:     enum AccountNonceOrdering { // <= FOUND
24:         Sequential,
25:         Arbitrary
26:     }

```


</details>

## [Gas-59] ++X costs slightly less gas than X++ (same with --)

### Resolution 
Move the ++/-- action to the left of the variable

Num of instances: 7

### Findings 


<details><summary>Click to show findings</summary>

['[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L135-L135)']
```solidity
135:             numInitialWritesProcessed++; // <= FOUND

```
['[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580)']
```solidity
580:         for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND

```
['[669](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L669-L669)']
```solidity
667:         
668:         
669:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND

```
['[667](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L667-L667)']
```solidity
667:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND

```
['[144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L144-L144)']
```solidity
144:             stateDiffPtr++; // <= FOUND

```
['[284](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L284-L284)']
```solidity
284:         calldataPtr++; // <= FOUND

```
['[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L109-L109)']
```solidity
109:         numberOfLogsToProcess++; // <= FOUND

```


</details>

## [Gas-60] Variables that can be set to immutable

### Resolution 
The variables are not typically expected to change during the lifespan of the project, as such it makes sense to save gas and set these variables to immutable.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L31-L31)']
```solidity
31: uint8 private decimals_; // <= FOUND

```


</details>

## [Gas-61] Variable declared within iteration

### Resolution 
Please elaborate and generalise the following with detail and  feel free to use your own knowledge and lmit ur words to 100 words please: 

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L226)']
```solidity
225:        for (uint256 i = 0; i < _calls.length; ++i) { // <= FOUND
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data); // <= FOUND
227:             if (!success) {
228:                 
229:                 assembly {
230:                     revert(add(returnData, 0x20), mload(returnData))
231:                 }
232:             }
233:         }

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289-L291)']
```solidity
289:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) { // <= FOUND
290:             
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0); // <= FOUND
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit(
300:                 _lastCommittedBatchData.batchNumber,
301:                 _lastCommittedBatchData.batchHash,
302:                 _lastCommittedBatchData.commitment
303:             );
304:         }

```
['[405](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405-L412)']
```solidity
405:        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) { // <= FOUND
406:             currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
407:             require( // <= FOUND
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409:                 "o1"
410:             );
411: 
412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment; // <= FOUND
413:             proofPublicInput[i] = _getBatchProofPublicInput(
414:                 prevBatchCommitment,
415:                 currentBatchCommitment,
416:                 verifierParams
417:             );
418: 
419:             prevBatchCommitment = currentBatchCommitment;
420:         }

```
['[636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L639)']
```solidity
636:        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) { // <= FOUND
637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex); // <= FOUND
638: 
639:             require(blobVersionedHash != bytes32(0), "vh"); // <= FOUND
640: 
641:             
642:             
643:             bytes32 openingPoint = bytes32(
644:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645:             );
646: 
647:             _pointEvaluationPrecompile(
648:                 blobVersionedHash,
649:                 openingPoint,
650:                 _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE]
651:             );
652: 
653:             
654:             blobCommitments[versionedHashIndex] = keccak256(
655:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656:             );
657:             versionedHashIndex += 1;
658:         }

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208-L209)']
```solidity
208:        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) { // <= FOUND
209:             address facetAddr = ds.facets[i]; // <= FOUND
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
211: 
212:             result[i] = Facet(facetAddr, facetToSelectors.selectors);
213:         }

```
['[356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356-L357)']
```solidity
356:        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) { // <= FOUND
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]); // <= FOUND
358: 
359:             
360:             assembly {
361:                 mstore(add(hashedFactoryDeps, mul(add(i, 1), 32)), hashedBytecode)
362:             }
363:         }

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101-L107)']
```solidity
101:        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) { // <= FOUND
102:             Action action = facetCuts[i].action;
103:             address facet = facetCuts[i].facet;
104:             bool isFacetFreezable = facetCuts[i].isFreezable; // <= FOUND
105:             bytes4[] memory selectors = facetCuts[i].selectors;
106: 
107:             require(selectors.length > 0, "B");  // <= FOUND
108: 
109:             if (action == Action.Add) {
110:                 _addFunctions(facet, selectors, isFacetFreezable);
111:             } else if (action == Action.Replace) {
112:                 _replaceFunctions(facet, selectors, isFacetFreezable);
113:             } else if (action == Action.Remove) {
114:                 _removeFunctions(facet, selectors);
115:             } else {
116:                 revert("C"); 
117:             }
118:         }

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127-L140)']
```solidity
127:        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) { // <= FOUND
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84);
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++;
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92); // <= FOUND
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch"); // <= FOUND
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144:             stateDiffPtr++;
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206-L206)']
```solidity
206:        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) { // <= FOUND
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }

```


</details>

## [Gas-62] Calling .length in a for loop wastes gas

### Resolution 
Rather than calling .length for an array in a for loop declaration, it is far more gas efficient to cache this length before and use that instead. This will prevent the array length from being called every loop iteration

Num of instances: 11

### Findings 


<details><summary>Click to show findings</summary>

['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L225)']
```solidity
225: for (uint256 i = 0; i < _calls.length; ++i)  // <= FOUND

```
['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116-L116)']
```solidity
116: for (uint256 i = 0; i < _newBatchesData.length; ++i)  // <= FOUND

```
['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116-L116)']
```solidity
116: for (uint256 i = 0; i < _newBatchesData.length; ++i)  // <= FOUND

```
['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116-L116)']
```solidity
116: for (uint256 i = 0; i < _newBatchesData.length; ++i)  // <= FOUND

```
['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L116-L116)']
```solidity
116: for (uint256 i = 0; i < _newBatchesData.length; ++i)  // <= FOUND

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L142)']
```solidity
142: for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE))  // <= FOUND

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257)']
```solidity
257: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc())  // <= FOUND

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257)']
```solidity
257: for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc())  // <= FOUND

```
['[636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636)']
```solidity
636: for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE)  // <= FOUND

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226)']
```solidity
226: for (uint256 i = 0; i < _factoryDeps.length; ++i)  // <= FOUND

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61-L61)']
```solidity
61: for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2)  // <= FOUND

```


</details>

## [Gas-63] Internal functions only used once can be inlined to save gas

### Resolution 
If a internal function is only used once it doesn't make sense to modularise it unless the function which does call the function would be overly long and complex otherwise

Num of instances: 82

### Findings 


<details><summary>Click to show findings</summary>

['[160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160-L160)']
```solidity
160:     function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256)  // <= FOUND

```
['[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L254-L254)']
```solidity
254:     function _getERC20Getters(address _token) internal view returns (bytes memory)  // <= FOUND

```
['[458](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L458-L458)']
```solidity
458:     function _checkWithdrawal( // <= FOUND
459:         uint256 _chainId,
460:         MessageParams memory _messageParams,
461:         bytes calldata _message,
462:         bytes32[] calldata _merkleProof
463:     ) internal view returns (address l1Receiver, address l1Token, uint256 amount) 

```
['[487](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L487-L487)']
```solidity
487:     function _parseL2WithdrawalMessage( // <= FOUND
488:         uint256 _chainId,
489:         bytes memory _l2ToL1message
490:     ) internal view returns (address l1Receiver, address l1Token, uint256 amount) 

```
['[177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L177)']
```solidity
177:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal  // <= FOUND

```
['[103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L103-L103)']
```solidity
103:     function _verifyBatchTimestamp( // <= FOUND
104:         uint256 _packedBatchAndL2BlockTimestamp,
105:         uint256 _expectedBatchTimestamp,
106:         uint256 _previousBatchTimestamp
107:     ) internal view 

```
['[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L130-L130)']
```solidity
130:     function _processL2Logs( // <= FOUND
131:         CommitBatchInfo calldata _newBatch,
132:         bytes32 _expectedSystemContractUpgradeTxHash
133:     ) internal pure returns (LogProcessingOutput memory logOutput) 

```
['[253](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L253-L253)']
```solidity
253:     function _commitBatchesWithoutSystemContractsUpgrade( // <= FOUND
254:         StoredBatchInfo memory _lastCommittedBatchData,
255:         CommitBatchInfo[] calldata _newBatchesData
256:     ) internal 

```
['[273](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L273-L273)']
```solidity
273:     function _commitBatchesWithSystemContractsUpgrade( // <= FOUND
274:         StoredBatchInfo memory _lastCommittedBatchData,
275:         CommitBatchInfo[] calldata _newBatchesData,
276:         bytes32 _systemContractUpgradeTxHash
277:     ) internal 

```
['[308](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L308-L308)']
```solidity
308:     function _collectOperationsFromPriorityQueue(uint256 _nPriorityOps) internal returns (bytes32 concatHash)  // <= FOUND

```
['[321](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L321-L321)']
```solidity
321:     function _executeOneBatch(StoredBatchInfo memory _storedBatch, uint256 _executedBatchIdx) internal  // <= FOUND

```
['[453](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L453-L453)']
```solidity
453:     function _getBatchProofPublicInput( // <= FOUND
454:         bytes32 _prevBatchCommitment,
455:         bytes32 _currentBatchCommitment,
456:         VerifierParams memory _verifierParams
457:     ) internal pure returns (uint256) 

```
['[500](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L500-L500)']
```solidity
500:     function _createBatchCommitment( // <= FOUND
501:         CommitBatchInfo calldata _newBatchData,
502:         bytes32 _stateDiffHash,
503:         bytes32[] memory _blobCommitments,
504:         bytes32[] memory _blobHashes
505:     ) internal view returns (bytes32) 

```
['[515](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L515-L515)']
```solidity
515:     function _batchPassThroughData(CommitBatchInfo calldata _batch) internal pure returns (bytes memory)  // <= FOUND

```
['[525](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L525-L525)']
```solidity
525:     function _batchMetaParameters() internal view returns (bytes memory)  // <= FOUND

```
['[537](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L537-L537)']
```solidity
537:     function _batchAuxiliaryOutput( // <= FOUND
538:         CommitBatchInfo calldata _batch,
539:         bytes32 _stateDiffHash,
540:         bytes32[] memory _blobCommitments,
541:         bytes32[] memory _blobHashes
542:     ) internal pure returns (bytes memory) 

```
['[561](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L561-L561)']
```solidity
561:     function _encodeBlobAuxilaryOutput( // <= FOUND
562:         bytes32[] memory _blobCommitments,
563:         bytes32[] memory _blobHashes
564:     ) internal pure returns (bytes32[] memory blobAuxOutputWords) 

```
['[592](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L592-L592)']
```solidity
592:     function _checkBit(uint256 _bitMap, uint8 _index) internal pure returns (bool)  // <= FOUND

```
['[597](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L597-L597)']
```solidity
597:     function _setBit(uint256 _bitMap, uint8 _index) internal pure returns (uint256)  // <= FOUND

```
['[605](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605-L605)']
```solidity
605:     function _pointEvaluationPrecompile( // <= FOUND
606:         bytes32 _versionedHash,
607:         bytes32 _openingPoint,
608:         bytes calldata _openingValueCommitmentProof
609:     ) internal view 

```
['[625](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L625-L625)']
```solidity
625:     function _verifyBlobInformation( // <= FOUND
626:         bytes calldata _pubdataCommitments,
627:         bytes32[] memory _blobHashes
628:     ) internal view returns (bytes32[] memory blobCommitments) 

```
['[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L130-L130)']
```solidity
130:     function _L2MessageToLog(L2Message memory _message) internal pure returns (L2Log memory)  // <= FOUND

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L289)']
```solidity
289:     function _serializeL2Transaction( // <= FOUND
290:         WritePriorityOpParams memory _priorityOpParams,
291:         bytes memory _calldata,
292:         bytes[] memory _factoryDeps
293:     ) internal pure returns (L2CanonicalTransaction memory transaction) 

```
['[316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L316-L316)']
```solidity
316:     function _writePriorityOp( // <= FOUND
317:         WritePriorityOpParams memory _priorityOpParams,
318:         bytes memory _calldata,
319:         bytes[] memory _factoryDeps
320:     ) internal returns (bytes32 canonicalTxHash) 

```
['[353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353-L353)']
```solidity
353:     function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps)  // <= FOUND

```
['[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/L2ContractHelper.sol#L90-L90)']
```solidity
90:     function sendMessageToL1(bytes memory _message) internal returns (bytes32)  // <= FOUND

```
['[17](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UncheckedMath.sol#L17-L17)']
```solidity
17:     function uncheckedAdd(uint256 _lhs, uint256 _rhs) internal pure returns (uint256)  // <= FOUND

```
['[19](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/UnsafeBytes.sol#L19-L19)']
```solidity
19:     function readUint32(bytes memory _bytes, uint256 _start) internal pure returns (uint32 result, uint256 offset)  // <= FOUND

```
['[26](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/UnsafeBytesCalldata.sol#L26-L26)']
```solidity
26:     function readUint32(bytes calldata _bytes, uint256 _start) internal pure returns (uint32 result)  // <= FOUND

```
['[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L18-L18)']
```solidity
18:     function calculateRoot( // <= FOUND
19:         bytes32[] calldata _path,
20:         uint256 _index,
21:         bytes32 _itemHash
22:     ) internal pure returns (bytes32) 

```
['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L97-L97)']
```solidity
97:     function getFirstUnprocessedPriorityTx() external view returns (uint256)  // <= FOUND

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L35-L35)']
```solidity
35:     function getFirstUnprocessedPriorityTx(Queue storage _queue) internal view returns (uint256)  // <= FOUND

```
['[45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45-L45)']
```solidity
45:     function getSize(Queue storage _queue) internal view returns (uint256)  // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55-L55)']
```solidity
55:     function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal  // <= FOUND

```
['[64](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L64-L64)']
```solidity
64:     function front(Queue storage _queue) internal view returns (PriorityOperation memory)  // <= FOUND

```
['[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L72-L72)']
```solidity
72:     function popFront(Queue storage _queue) internal returns (PriorityOperation memory priorityOperation)  // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L46-L46)']
```solidity
46:     function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure  // <= FOUND

```
['[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L69-L69)']
```solidity
69:     function getMinimalPriorityTransactionGasLimit( // <= FOUND
70:         uint256 _encodingLength,
71:         uint256 _numberOfFactoryDependencies,
72:         uint256 _l2GasPricePerPubdata
73:     ) internal pure returns (uint256) 

```
['[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L109-L109)']
```solidity
109:     function getTransactionBodyGasLimit( // <= FOUND
110:         uint256 _totalGasLimit,
111:         uint256 _encodingLength
112:     ) internal pure returns (uint256 txBodyGasLimit) 

```
['[128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L128-L128)']
```solidity
128:     function getOverheadForTransaction( // <= FOUND
129:         uint256 _encodingLength
130:     ) internal pure returns (uint256 batchOverheadForTransaction) 

```
['[44](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L44-L44)']
```solidity
44:     function encodeLegacyTransactionHash(Transaction calldata _transaction) internal view returns (bytes32 txHash)  // <= FOUND

```
['[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L139-L139)']
```solidity
139:     function encodeEIP2930TransactionHash(Transaction calldata _transaction) internal view returns (bytes32)  // <= FOUND

```
['[229](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/BootloaderUtilities.sol#L229-L229)']
```solidity
229:     function encodeEIP1559TransactionHash(Transaction calldata _transaction) internal view returns (bytes32)  // <= FOUND

```
['[197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L197-L197)']
```solidity
197:     function _decodeRawBytecode( // <= FOUND
198:         bytes calldata _rawCompressedData
199:     ) internal pure returns (bytes calldata dictionary, bytes calldata encodedData) 

```
['[283](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L283-L283)']
```solidity
283:     function _performDeployOnAddress( // <= FOUND
284:         bytes32 _bytecodeHash,
285:         address _newAddress,
286:         AccountAbstractionVersion _aaVersion,
287:         bytes calldata _input
288:     ) internal 

```
['[309](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L309-L309)']
```solidity
309:     function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal  // <= FOUND

```
['[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L78-L78)']
```solidity
78:     function _validateTransaction( // <= FOUND
79:         bytes32 _suggestedSignedHash,
80:         Transaction calldata _transaction
81:     ) internal returns (bytes4 magic) 

```
['[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L159-L159)']
```solidity
159:     function _isValidSignature(bytes32 _hash, bytes memory _signature) internal view returns (bool)  // <= FOUND

```
['[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L74-L74)']
```solidity
74:     function _validateBytecode(bytes32 _bytecodeHash) internal pure  // <= FOUND

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L61-L61)']
```solidity
61:     function sha256GasCost(uint256 _length) internal pure returns (uint256)  // <= FOUND

```
['[117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L117-L117)']
```solidity
117:     function _getExtendedWithdrawMessage( // <= FOUND
118:         address _to,
119:         uint256 _amount,
120:         address _sender,
121:         bytes memory _additionalData
122:     ) internal pure returns (bytes memory) 

```
['[221](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L221-L221)']
```solidity
221:     function _calculateL2BlockHash( // <= FOUND
222:         uint128 _blockNumber,
223:         uint128 _blockTimestamp,
224:         bytes32 _prevL2BlockHash,
225:         bytes32 _blockTxsRollingHash
226:     ) internal pure returns (bytes32) 

```
['[233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L233-L233)']
```solidity
233:     function _calculateLegacyL2BlockHash(uint128 _blockNumber) internal pure returns (bytes32)  // <= FOUND

```
['[241](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L241-L241)']
```solidity
241:     function _upgradeL2Blocks(uint128 _l2BlockNumber, bytes32 _expectedPrevL2BlockHash, bool _isFirstInBatch) internal  // <= FOUND

```
['[263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L263-L263)']
```solidity
263:     function _setVirtualBlock( // <= FOUND
264:         uint128 _l2BlockNumber,
265:         uint128 _maxVirtualBlocksToCreate,
266:         uint128 _newTimestamp
267:     ) internal 

```
['[427](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L427-L427)']
```solidity
427:     function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view  // <= FOUND

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L105-L105)']
```solidity
105:     function mimicCall( // <= FOUND
106:         uint256 _gas,
107:         address _address,
108:         bytes calldata _data,
109:         address _whoToMimic,
110:         bool _isConstructor,
111:         bool _isSystem
112:     ) internal returns (bytes memory returnData) 

```
['[159](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L159-L159)']
```solidity
159:     function rawStaticCall(uint256 _gas, address _address, bytes calldata _data) internal view returns (bool success)  // <= FOUND

```
['[173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L173-L173)']
```solidity
173:     function rawDelegateCall(uint256 _gas, address _address, bytes calldata _data) internal returns (bool success)  // <= FOUND

```
['[191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L191-L191)']
```solidity
191:     function rawMimicCall( // <= FOUND
192:         uint256 _gas,
193:         address _address,
194:         bytes calldata _data,
195:         address _whoToMimic,
196:         bool _isConstructor,
197:         bool _isSystem
198:     ) internal returns (bool success) 

```
['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L63-L63)']
```solidity
63:     function getCodeAddress() internal view returns (address addr)  // <= FOUND

```
['[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L74-L74)']
```solidity
74:     function loadCalldataIntoActivePtr() internal view  // <= FOUND

```
['[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L85-L85)']
```solidity
85:     function ptrPackIntoActivePtr(uint256 _farCallAbi) internal view  // <= FOUND

```
['[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L94-L94)']
```solidity
94:     function ptrAddIntoActive(uint32 _value) internal view  // <= FOUND

```
['[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L106-L106)']
```solidity
106:     function ptrShrinkIntoActive(uint32 _shrink) internal view  // <= FOUND

```
['[148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L148-L148)']
```solidity
148:     function unsafePrecompileCall( // <= FOUND
149:         uint256 _rawParams,
150:         uint32 _gasToBurn,
151:         uint32 _pubdataToSpend
152:     ) internal view returns (bool success) 

```
['[168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L168-L168)']
```solidity
168:     function setValueForNextFarCall(uint128 _value) internal returns (bool success)  // <= FOUND

```
['[203](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L203-L203)']
```solidity
203:     function getZkSyncMetaBytes() internal view returns (uint256 meta)  // <= FOUND

```
['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L227-L227)']
```solidity
227:     function getPubdataPublishedFromMeta(uint256 meta) internal pure returns (uint32 pubdataPublished)  // <= FOUND

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L237-L237)']
```solidity
237:     function getHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 heapSize)  // <= FOUND

```
['[246](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L246-L246)']
```solidity
246:     function getAuxHeapSizeFromMeta(uint256 meta) internal pure returns (uint32 auxHeapSize)  // <= FOUND

```
['[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L254-L254)']
```solidity
254:     function getShardIdFromMeta(uint256 meta) internal pure returns (uint8 shardId)  // <= FOUND

```
['[263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L263-L263)']
```solidity
263:     function getCallerShardIdFromMeta(uint256 meta) internal pure returns (uint8 callerShardId)  // <= FOUND

```
['[272](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L272-L272)']
```solidity
272:     function getCodeShardIdFromMeta(uint256 meta) internal pure returns (uint8 codeShardId)  // <= FOUND

```
['[296](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L296-L296)']
```solidity
296:     function getCallFlags() internal view returns (uint256 callFlags)  // <= FOUND

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L76-L76)']
```solidity
76:     function systemCallWithReturndata( // <= FOUND
77:         uint32 gasLimit,
78:         address to,
79:         uint128 value,
80:         bytes memory data
81:     ) internal returns (bool success, bytes memory returnData) 

```
['[362](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L362-L362)']
```solidity
362:     function processPaymasterInput(Transaction calldata _transaction) internal  // <= FOUND

```
['[395](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L395-L395)']
```solidity
395:     function payToTheBootloader(Transaction calldata _transaction) internal returns (bool success)  // <= FOUND

```
['[20](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L20-L20)']
```solidity
20:     function safeCastToU128(uint256 _x) internal pure returns (uint128)  // <= FOUND

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L51-L51)']
```solidity
51:     function isContractConstructed(bytes32 _bytecodeHash) internal pure returns (bool)  // <= FOUND

```
['[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L109-L109)']
```solidity
109:     function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address)  // <= FOUND

```
['[164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L164-L164)']
```solidity
164:     function _deployBeaconProxy(bytes32 salt) internal returns (BeaconProxy proxy)  // <= FOUND

```


</details>

## [Gas-64] Constructors can be marked as payable to save deployment gas

Num of instances: 10

### Findings 


<details><summary>Click to show findings</summary>

['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L55-L55)']
```solidity
55:     constructor(IL1SharedBridge _sharedBridge) reentrancyGuardInitializer {
56:         sharedBridge = _sharedBridge;
57:     }

```
['[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90-L90)']
```solidity
90:     constructor(
91:         address _l1WethAddress,
92:         IBridgehub _bridgehub,
93:         IL1ERC20Bridge _legacyBridge
94:     ) reentrancyGuardInitializer {
95:         _disableInitializers();
96:         l1WethAddress = _l1WethAddress;
97:         bridgehub = _bridgehub;
98:         legacyBridge = _legacyBridge;
99:     }

```
['[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38-L38)']
```solidity
38:     constructor() reentrancyGuardInitializer {}

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L41-L41)']
```solidity
41:     constructor(address _admin, address _securityCouncil, uint256 _minDelay) {
42:         require(_admin != address(0), "Admin should be non zero address");
43: 
44:         _transferOwnership(_admin);
45: 
46:         securityCouncil = _securityCouncil;
47:         emit ChangeSecurityCouncil(address(0), _securityCouncil);
48: 
49:         minDelay = _minDelay;
50:         emit ChangeMinDelay(0, _minDelay);
51:     }

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58-L58)']
```solidity
58:     constructor(address _bridgehub) reentrancyGuardInitializer {
59:         bridgehub = _bridgehub;
60:     }

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L55-L55)']
```solidity
55:     constructor(address _initialOwner, uint32 _executionDelay) {
56:         _transferOwnership(_initialOwner);
57:         executionDelay = _executionDelay;
58:     }

```
['[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L38-L38)']
```solidity
38:     constructor() reentrancyGuardInitializer {}

```
['[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L11-L11)']
```solidity
11:     constructor(uint256 _chainId, Diamond.DiamondCutData memory _diamondCut) {
12:         
13:         
14:         require(_chainId == block.chainid, "pr");
15:         Diamond.diamondCut(_diamondCut);
16:     }

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L41-L41)']
```solidity
41:     constructor() {
42:         _disableInitializers();
43:     }

```
['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L40-L40)']
```solidity
40:     constructor() {
41:         
42:         _disableInitializers();
43:     }

```


</details>

## [Gas-65] Merge events to save gas

### Resolution 
Consolidating multiple event emissions into a single event in Solidity can result in significant gas savings. Each event emission in Ethereum involves a gas cost, specifically for the topics logged with the event. By merging sequential events into a singular event, you can save on the Glogtopic cost, which is incurred for each topic of each event. This approach can save around 375 gas per additional topic. This strategy is particularly beneficial in functions where multiple related events are emitted in sequence. However, it's crucial to balance gas optimization with the clarity and utility of the event data for off-chain consumers.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L60-L69)']
```solidity
60:     function acceptAdmin() external {
61:         address currentPendingAdmin = pendingAdmin;
62:         require(msg.sender == currentPendingAdmin, "n42"); 
63: 
64:         address previousAdmin = admin;
65:         admin = currentPendingAdmin;
66:         delete pendingAdmin;
67: 
68:         emit NewPendingAdmin(currentPendingAdmin, address(0)); // <= FOUND
69:         emit NewAdmin(previousAdmin, pendingAdmin); // <= FOUND
70:     }

```
['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L60-L69)']
```solidity
60:     function acceptAdmin() external {
61:         address currentPendingAdmin = pendingAdmin;
62:         require(msg.sender == currentPendingAdmin, "n42"); 
63: 
64:         address previousAdmin = admin;
65:         admin = currentPendingAdmin;
66:         delete pendingAdmin;
67: 
68:         emit NewPendingAdmin(currentPendingAdmin, address(0)); // <= FOUND
69:         emit NewAdmin(previousAdmin, pendingAdmin); // <= FOUND
70:     }

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L32-L41)']
```solidity
32:     function acceptAdmin() external {
33:         address pendingAdmin = s.pendingAdmin;
34:         require(msg.sender == pendingAdmin, "n4"); 
35: 
36:         address previousAdmin = s.admin;
37:         s.admin = pendingAdmin;
38:         delete s.pendingAdmin;
39: 
40:         emit NewPendingAdmin(pendingAdmin, address(0)); // <= FOUND
41:         emit NewAdmin(previousAdmin, pendingAdmin); // <= FOUND
42:     }

```


</details>

## [Gas-66] Use assembly scratch space to build calldata for external calls

### Resolution 
Using Solidity's assembly scratch space for constructing calldata in external calls with one or two arguments can be a gas-efficient approach. This method leverages the designated memory area (the first 64 bytes of memory) for temporary data storage during assembly operations. By directly writing arguments into this scratch space, it eliminates the need for additional memory allocation typically required for calldata preparation. This technique can lead to notable gas savings, especially in high-frequency or gas-sensitive operations. However, it requires careful implementation to avoid data corruption and should be used with a thorough understanding of low-level EVM operations and memory handling. Proper testing and validation are crucial when employing such optimizations.

Num of instances: 9

### Findings 


<details><summary>Click to show findings</summary>

['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L63-L63)']
```solidity
63:             (bool success, ) = address(REAL_BASE_TOKEN_SYSTEM_CONTRACT).call( // <= FOUND
64:                 abi.encodeCall(REAL_BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo, (msg.sender, to, value))
65:             );

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L57-L61)']
```solidity
57:         
58:         
59:         
60:         
61:         bytes memory returnData = EfficientCall.call(gasleft(), _to, msg.value, _data, false); // <= FOUND

```
['[283](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L283-L284)']
```solidity
283:             
284:             (bool success, bytes memory data) = _init.delegatecall(_calldata); // <= FOUND

```
['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ComplexUpgrader.sol#L25-L25)']
```solidity
25:         (bool success, bytes memory returnData) = _delegateTo.delegatecall(_calldata); // <= FOUND

```
['[262](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L262-L262)']
```solidity
262:         (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ())); // <= FOUND

```
['[263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L263-L263)']
```solidity
263:         (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ())); // <= FOUND

```
['[264](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L264-L264)']
```solidity
264:         (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ())); // <= FOUND

```
['[612](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L612-L612)']
```solidity
612:         (bool success, bytes memory data) = POINT_EVALUATION_PRECOMPILE_ADDR.staticcall(precompileInput); // <= FOUND

```
['[680](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L680-L680)']
```solidity
680:         (bool success, bytes memory data) = s.blobVersionedHashRetriever.staticcall(abi.encode(_index)); // <= FOUND

```


</details>

## [Gas-67] Same cast is done multiple times

### Resolution 
Repeatedly casting the same variable to the same type within a function is redundant and can be optimized for better gas efficiency and code readability. Each unnecessary cast operation, while minor, adds to the gas cost and clutters the code. To optimize, the best practice is to perform the cast once and store the result in a temporary variable, which can then be used wherever needed in the function.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L194)']
```solidity
177:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
178:         bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
179:         uint256[] memory uintEmptyArray;
180:         bytes[] memory bytesEmptyArray;
181: 
182:         L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
183:             txType: SYSTEM_UPGRADE_L2_TX_TYPE,
184:             from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
185:             to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
186:             gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
187:             gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
188:             maxFeePerGas: uint256(0), // <= FOUND 'int256(0)'
189:             maxPriorityFeePerGas: uint256(0), // <= FOUND 'int256(0)'
190:             paymaster: uint256(0), // <= FOUND 'int256(0)'
191:             
192:             nonce: protocolVersion,
193:             value: 0,
194:             reserved: [uint256(0), 0, 0, 0], // <= FOUND 'int256(0)'
195:             data: systemContextCalldata,
196:             signature: new bytes(0),
197:             factoryDeps: uintEmptyArray,
198:             paymasterInput: new bytes(0),
199:             reservedDynamic: new bytes(0)
200:         });
201: 
202:         ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
203:             l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
204:             factoryDeps: bytesEmptyArray,
205:             bootloaderHash: bytes32(0),
206:             defaultAccountHash: bytes32(0),
207:             verifier: address(0),
208:             verifierParams: VerifierParams({
209:                 recursionNodeLevelVkHash: bytes32(0),
210:                 recursionLeafLevelVkHash: bytes32(0),
211:                 recursionCircuitsSetVksHash: bytes32(0)
212:             }),
213:             l1ContractsUpgradeCalldata: new bytes(0),
214:             postUpgradeCalldata: new bytes(0),
215:             upgradeTimestamp: 0,
216:             newProtocolVersion: protocolVersion
217:         });
218: 
219:         Diamond.FacetCut[] memory emptyArray;
220:         Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
221:             facetCuts: emptyArray,
222:             initAddress: genesisUpgrade,
223:             initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
224:         });
225: 
226:         IAdmin(_chainContract).executeUpgrade(cutData);
227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
228:     }

```
['[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L130-L173)']
```solidity
130:     function _processL2Logs(
131:         CommitBatchInfo calldata _newBatch,
132:         bytes32 _expectedSystemContractUpgradeTxHash
133:     ) internal pure returns (LogProcessingOutput memory logOutput) {
134:         
135:         bytes memory emittedL2Logs = _newBatch.systemLogs;
136: 
137:         
138:         
139:         uint256 processedLogs;
140: 
141:         
142:         for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
143:             
144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
147: 
148:             
149:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");
150:             processedLogs = _setBit(processedLogs, uint8(logKey));
151: 
152:             
153:             if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
154:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
155:                 logOutput.l2LogsTreeRoot = logValue;
156:             } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
157:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
158:                 logOutput.pubdataHash = logValue;
159:             } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
160:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
161:                 logOutput.stateDiffHash = logValue;
162:             } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
163:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
164:                 logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue); // <= FOUND 'int256(logValue)'
165:             } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
166:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
167:                 logOutput.previousBatchHash = logValue;
168:             } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
169:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
170:                 logOutput.chainedPriorityTxsHash = logValue;
171:             } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
172:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
173:                 logOutput.numberOfLayer1Txs = uint256(logValue); // <= FOUND 'int256(logValue)'
174:             } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
175:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
176:                 logOutput.blob1Hash = logValue;
177:             } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
178:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
179:                 logOutput.blob2Hash = logValue;
180:             } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
181:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
182:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
183:             } else {
184:                 revert("ul");
185:             }
186:         }
187: 
188:         
189:         
190:         
191:         if (_expectedSystemContractUpgradeTxHash == bytes32(0)) {
192:             require(processedLogs == 511, "b7");
193:         } else {
194:             require(processedLogs == 1023, "b8");
195:         }
196:     }

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L302)']
```solidity
289:     function _serializeL2Transaction(
290:         WritePriorityOpParams memory _priorityOpParams,
291:         bytes memory _calldata,
292:         bytes[] memory _factoryDeps
293:     ) internal pure returns (L2CanonicalTransaction memory transaction) {
294:         transaction = L2CanonicalTransaction({
295:             txType: PRIORITY_OPERATION_L2_TX_TYPE,
296:             from: uint256(uint160(_priorityOpParams.sender)),
297:             to: uint256(uint160(_priorityOpParams.contractAddressL2)),
298:             gasLimit: _priorityOpParams.l2GasLimit,
299:             gasPerPubdataByteLimit: _priorityOpParams.l2GasPricePerPubdata,
300:             maxFeePerGas: uint256(_priorityOpParams.l2GasPrice),
301:             maxPriorityFeePerGas: uint256(0), // <= FOUND 'int256(0)'
302:             paymaster: uint256(0), // <= FOUND 'int256(0)'
303:             
304:             nonce: uint256(_priorityOpParams.txId),
305:             value: _priorityOpParams.l2Value,
306:             reserved: [_priorityOpParams.valueToMint, uint256(uint160(_priorityOpParams.refundRecipient)), 0, 0],
307:             data: _calldata,
308:             signature: new bytes(0),
309:             factoryDeps: _hashFactoryDeps(_factoryDeps),
310:             paymasterInput: new bytes(0),
311:             reservedDynamic: new bytes(0)
312:         });
313:     }

```
['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L60-L72)']
```solidity
60:     function _encodeLength(uint64 _len, uint256 _offset) private pure returns (bytes memory encoded) {
61:         unchecked {
62:             if (_len < 56) {
63:                 encoded = new bytes(1);
64:                 encoded[0] = bytes1(uint8(_len + _offset));
65:             } else {
66:                 uint256 hbs = _highestByteSet(uint256(_len)); // <= FOUND 'int256(_len)'
67: 
68:                 encoded = new bytes(hbs + 2);
69:                 encoded[0] = bytes1(uint8(_offset + hbs + 56));
70: 
71:                 uint256 lbs = 31 - hbs;
72:                 uint256 shiftedVal = uint256(_len) << (lbs * 8); // <= FOUND 'int256(_len)'
73: 
74:                 assembly {
75:                     mstore(add(encoded, 0x21), shiftedVal)
76:                 }
77:             }
78:         }
79:     }

```
['[63](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L63-L67)']
```solidity
63:     function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
64:         require(msg.sender == address(sharedBridge), "Not shared bridge"); // <= FOUND 'address(sharedBridge)'
65:         uint256 amount = IERC20(_token).balanceOf(address(this));
66:         require(amount == _amount, "Incorrect amount");
67:         IERC20(_token).safeTransfer(address(sharedBridge), amount); // <= FOUND 'address(sharedBridge)'
68:     }

```
['[160](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160-L163)']
```solidity
160:     function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
161:         uint256 balanceBefore = _token.balanceOf(address(sharedBridge)); // <= FOUND 'address(sharedBridge)'
162:         _token.safeTransferFrom(_from, address(sharedBridge), _amount); // <= FOUND 'address(sharedBridge)'
163:         uint256 balanceAfter = _token.balanceOf(address(sharedBridge)); // <= FOUND 'address(sharedBridge)'
164: 
165:         return balanceAfter - balanceBefore;
166:     }

```
['[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L114-L140)']
```solidity
114:     function createNewChain(
115:         uint256 _chainId,
116:         address _stateTransitionManager,
117:         address _baseToken,
118:         uint256, 
119:         address _admin,
120:         bytes calldata _initData
121:     ) external onlyOwnerOrAdmin nonReentrant returns (uint256 chainId) {
122:         require(_chainId != 0, "Bridgehub: chainId cannot be 0");
123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large");
124: 
125:         require(
126:             stateTransitionManagerIsRegistered[_stateTransitionManager],
127:             "Bridgehub: state transition not registered"
128:         );
129:         require(tokenIsRegistered[_baseToken], "Bridgehub: token not registered");
130:         require(address(sharedBridge) != address(0), "Bridgehub: weth bridge not set"); // <= FOUND 'address(sharedBridge)'
131: 
132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered");
133: 
134:         stateTransitionManager[_chainId] = _stateTransitionManager;
135:         baseToken[_chainId] = _baseToken;
136: 
137:         IStateTransitionManager(_stateTransitionManager).createNewChain(
138:             _chainId,
139:             _baseToken,
140:             address(sharedBridge), // <= FOUND 'address(sharedBridge)'
141:             _admin,
142:             _initData
143:         );
144: 
145:         emit NewChain(_chainId, _stateTransitionManager, _admin);
146:         return _chainId;
147:     }

```
['[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L109-L115)']
```solidity
109:     function _deployL2Token(address _l1Token, bytes calldata _data) internal returns (address) {
110:         bytes32 salt = _getCreate2Salt(_l1Token);
111: 
112:         BeaconProxy l2Token = _deployBeaconProxy(salt);
113:         L2StandardERC20(address(l2Token)).bridgeInitialize(_l1Token, _data); // <= FOUND 'address(l2Token)'
114: 
115:         return address(l2Token); // <= FOUND 'address(l2Token)'
116:     }

```


</details>

## [Gas-68] Assigning to structs can be more efficient

### Resolution 
Rather defining the struct in a single line, it is more efficient to declare an empty struct and then assign each struct element individually. This can net quite a large gas saving of 130 per instance.

Num of instances: 16

### Findings 


<details><summary>Click to show findings</summary>

['[182](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L182-L219)']
```solidity
182:     function bridgehubDeposit(
183:         uint256 _chainId,
184:         address _prevMsgSender,
185:         uint256, 
186:         bytes calldata _data
187:     ) external payable override onlyBridgehub returns (L2TransactionRequestTwoBridgesInner memory request) {
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed");
189: 
190:         (address _l1Token, uint256 _depositAmount, address _l2Receiver) = abi.decode(
191:             _data,
192:             (address, uint256, address)
193:         );
194:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported");
195:         require(bridgehub.baseToken(_chainId) != _l1Token, "ShB: baseToken deposit not supported");
196: 
197:         uint256 amount;
198:         if (_l1Token == ETH_TOKEN_ADDRESS) {
199:             amount = msg.value;
200:             require(_depositAmount == 0, "ShB wrong withdraw amount");
201:         } else {
202:             require(msg.value == 0, "ShB m.v > 0 for BH d.it 2");
203:             amount = _depositAmount;
204: 
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); 
207:         }
208:         require(amount != 0, "6T"); 
209: 
210:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, amount));
211:         if (!hyperbridgingEnabled[_chainId]) {
212:             chainBalance[_chainId][_l1Token] += amount;
213:         }
214: 
215:         {
216:             
217:             bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, amount);
218: 
219:             request = L2TransactionRequestTwoBridgesInner({ // <= FOUND
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId],
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0),
224:                 txDataHash: txDataHash
225:             });
226:         }
227:         emit BridgehubDepositInitiated(_chainId, txDataHash, _prevMsgSender, _l2Receiver, _l1Token, amount);
228:     }

```
['[409](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L409-L430)']
```solidity
409:     function _finalizeWithdrawal(
410:         uint256 _chainId,
411:         uint256 _l2BatchNumber,
412:         uint256 _l2MessageIndex,
413:         uint16 _l2TxNumberInBatch,
414:         bytes calldata _message,
415:         bytes32[] calldata _merkleProof
416:     ) internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;
419: 
420:         
421:         if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
422:             
423:             bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
424:                 _l2BatchNumber,
425:                 _l2MessageIndex
426:             );
427:             require(!alreadyFinalized, "Withdrawal is already finalized 2");
428:         }
429: 
430:         MessageParams memory messageParams = MessageParams({ // <= FOUND
431:             l2BatchNumber: _l2BatchNumber,
432:             l2MessageIndex: _l2MessageIndex,
433:             l2TxNumberInBatch: _l2TxNumberInBatch
434:         });
435:         (l1Receiver, l1Token, amount) = _checkWithdrawal(_chainId, messageParams, _message, _merkleProof);
436: 
437:         if (!hyperbridgingEnabled[_chainId]) {
438:             
439:             require(chainBalance[_chainId][l1Token] >= amount, "ShB not enough funds 2"); 
440:             chainBalance[_chainId][l1Token] -= amount;
441:         }
442: 
443:         if (l1Token == ETH_TOKEN_ADDRESS) {
444:             bool callSuccess;
445:             
446:             assembly {
447:                 callSuccess := call(gas(), l1Receiver, amount, 0, 0, 0, 0)
448:             }
449:             require(callSuccess, "ShB: withdraw failed");
450:         } else {
451:             
452:             IERC20(l1Token).safeTransfer(l1Receiver, amount);
453:         }
454:         emit WithdrawalFinalizedSharedBridge(_chainId, l1Receiver, l1Token, amount);
455:     }

```
['[458](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L458-L470)']
```solidity
458:     function _checkWithdrawal(
459:         uint256 _chainId,
460:         MessageParams memory _messageParams,
461:         bytes calldata _message,
462:         bytes32[] calldata _merkleProof
463:     ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
464:         (l1Receiver, l1Token, amount) = _parseL2WithdrawalMessage(_chainId, _message);
465:         L2Message memory l2ToL1Message;
466:         {
467:             bool baseTokenWithdrawal = (l1Token == bridgehub.baseToken(_chainId));
468:             address l2Sender = baseTokenWithdrawal ? L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR : l2BridgeAddress[_chainId];
469: 
470:             l2ToL1Message = L2Message({ // <= FOUND
471:                 txNumberInBatch: _messageParams.l2TxNumberInBatch,
472:                 sender: l2Sender,
473:                 data: _message
474:             });
475:         }
476: 
477:         bool success = bridgehub.proveL2MessageInclusion(
478:             _chainId,
479:             _messageParams.l2BatchNumber,
480:             _messageParams.l2MessageIndex,
481:             l2ToL1Message,
482:             _merkleProof
483:         );
484:         require(success, "ShB withd w proof"); 
485:     }

```
['[554](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554-L584)']
```solidity
554:     function depositLegacyErc20Bridge(
555:         address _prevMsgSender,
556:         address _l2Receiver,
557:         address _l1Token,
558:         uint256 _amount,
559:         uint256 _l2TxGasLimit,
560:         uint256 _l2TxGasPerPubdataByte,
561:         address _refundRecipient
562:     ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
564:         require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");
565: 
566:         
567:         if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
568:             chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
569:         }
570: 
571:         bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);
572: 
573:         {
574:             
575:             
576:             
577:             address refundRecipient = _refundRecipient;
578:             if (_refundRecipient == address(0)) {
579:                 refundRecipient = _prevMsgSender != tx.origin
580:                     ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
581:                     : _prevMsgSender;
582:             }
583: 
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({ // <= FOUND
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
587:                 mintValue: msg.value, 
588:                 l2Value: 0, 
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0),
593:                 refundRecipient: refundRecipient
594:             });
595:             l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
596:         }
597: 
598:         bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
599:         
600:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;
601: 
602:         emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
603:     }

```
['[217](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L217-L238)']
```solidity
217:     function requestL2TransactionDirect(
218:         L2TransactionRequestDirect calldata _request
219:     ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
220:         {
221:             address token = baseToken[_request.chainId];
222:             if (token == ETH_TOKEN_ADDRESS) {
223:                 require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");
224:             } else {
225:                 require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
226:             }
227: 
228:             sharedBridge.bridgehubDepositBaseToken{value: msg.value}(
229:                 _request.chainId,
230:                 msg.sender,
231:                 token,
232:                 _request.mintValue
233:             );
234:         }
235: 
236:         address stateTransition = getStateTransition(_request.chainId);
237:         address refundRecipient = _actualRefundRecipient(_request.refundRecipient);
238:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction( // <= FOUND
239:             BridgehubL2TransactionRequest({
240:                 sender: msg.sender,
241:                 contractL2: _request.l2Contract,
242:                 mintValue: _request.mintValue,
243:                 l2Value: _request.l2Value,
244:                 l2Calldata: _request.l2Calldata,
245:                 l2GasLimit: _request.l2GasLimit,
246:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
247:                 factoryDeps: _request.factoryDeps,
248:                 refundRecipient: refundRecipient
249:             })
250:         );
251:     }

```
['[262](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L262-L304)']
```solidity
262:     function requestL2TransactionTwoBridges(
263:         L2TransactionRequestTwoBridgesOuter calldata _request
264:     ) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
265:         {
266:             address token = baseToken[_request.chainId];
267:             uint256 baseTokenMsgValue;
268:             if (token == ETH_TOKEN_ADDRESS) {
269:                 require(
270:                     msg.value == _request.mintValue + _request.secondBridgeValue,
271:                     "Bridgehub: msg.value mismatch 2"
272:                 );
273:                 baseTokenMsgValue = _request.mintValue;
274:             } else {
275:                 require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");
276:                 baseTokenMsgValue = 0;
277:             }
278:             sharedBridge.bridgehubDepositBaseToken{value: baseTokenMsgValue}(
279:                 _request.chainId,
280:                 msg.sender,
281:                 token,
282:                 _request.mintValue
283:             );
284:         }
285: 
286:         address stateTransition = getStateTransition(_request.chainId);
287: 
288:         L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)
289:             .bridgehubDeposit{value: _request.secondBridgeValue}(
290:             _request.chainId,
291:             msg.sender,
292:             _request.l2Value,
293:             _request.secondBridgeCalldata
294:         );
295: 
296:         require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");
297: 
298:         address refundRecipient = _actualRefundRecipient(_request.refundRecipient);
299: 
300:         require(
301:             _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
302:             "Bridgehub: second bridge address too low"
303:         ); 
304:         canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction( // <= FOUND
305:             BridgehubL2TransactionRequest({
306:                 sender: _request.secondBridgeAddress,
307:                 contractL2: outputRequest.l2Contract,
308:                 mintValue: _request.mintValue,
309:                 l2Value: _request.l2Value,
310:                 l2Calldata: outputRequest.l2Calldata,
311:                 l2GasLimit: _request.l2GasLimit,
312:                 l2GasPerPubdataByteLimit: _request.l2GasPerPubdataByteLimit,
313:                 factoryDeps: outputRequest.factoryDeps,
314:                 refundRecipient: refundRecipient
315:             })
316:         );
317: 
318:         IL1SharedBridge(_request.secondBridgeAddress).bridgehubConfirmL2Transaction(
319:             _request.chainId,
320:             outputRequest.txDataHash,
321:             canonicalTxHash
322:         );
323:     }

```
['[177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L182)']
```solidity
177:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal { // <= FOUND
178:         bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
179:         uint256[] memory uintEmptyArray;
180:         bytes[] memory bytesEmptyArray;
181: 
182:         L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({ // <= FOUND
183:             txType: SYSTEM_UPGRADE_L2_TX_TYPE,
184:             from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
185:             to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
186:             gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
187:             gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
188:             maxFeePerGas: uint256(0),
189:             maxPriorityFeePerGas: uint256(0),
190:             paymaster: uint256(0),
191:             
192:             nonce: protocolVersion,
193:             value: 0,
194:             reserved: [uint256(0), 0, 0, 0],
195:             data: systemContextCalldata,
196:             signature: new bytes(0),
197:             factoryDeps: uintEmptyArray,
198:             paymasterInput: new bytes(0),
199:             reservedDynamic: new bytes(0)
200:         });
201: 
202:         ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
203:             l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
204:             factoryDeps: bytesEmptyArray,
205:             bootloaderHash: bytes32(0),
206:             defaultAccountHash: bytes32(0),
207:             verifier: address(0),
208:             verifierParams: VerifierParams({
209:                 recursionNodeLevelVkHash: bytes32(0),
210:                 recursionLeafLevelVkHash: bytes32(0),
211:                 recursionCircuitsSetVksHash: bytes32(0)
212:             }),
213:             l1ContractsUpgradeCalldata: new bytes(0),
214:             postUpgradeCalldata: new bytes(0),
215:             upgradeTimestamp: 0,
216:             newProtocolVersion: protocolVersion
217:         });
218: 
219:         Diamond.FacetCut[] memory emptyArray;
220:         Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
221:             facetCuts: emptyArray,
222:             initAddress: genesisUpgrade,
223:             initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
224:         });
225: 
226:         IAdmin(_chainContract).executeUpgrade(cutData);
227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
228:     }

```
['[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L74-L92)']
```solidity
74:     function proveL1ToL2TransactionStatus(
75:         bytes32 _l2TxHash,
76:         uint256 _l2BatchNumber,
77:         uint256 _l2MessageIndex,
78:         uint16 _l2TxNumberInBatch,
79:         bytes32[] calldata _merkleProof,
80:         TxStatus _status
81:     ) public view returns (bool) {
82:         
83:         
84:         
85:         
86:         
87:         
88:         
89:         
90:         
91:         
92:         L2Log memory l2Log = L2Log({ // <= FOUND
93:             l2ShardId: 0,
94:             isService: true,
95:             txNumberInBatch: _l2TxNumberInBatch,
96:             sender: L2_BOOTLOADER_ADDRESS,
97:             key: _l2TxHash,
98:             value: bytes32(uint256(_status))
99:         });
100:         return _proveL2LogInclusion(_l2BatchNumber, _l2MessageIndex, l2Log, _merkleProof);
101:     }

```
['[197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L197-L207)']
```solidity
197:     function requestL2Transaction(
198:         address _contractL2,
199:         uint256 _l2Value,
200:         bytes calldata _calldata,
201:         uint256 _l2GasLimit,
202:         uint256 _l2GasPerPubdataByteLimit,
203:         bytes[] calldata _factoryDeps,
204:         address _refundRecipient
205:     ) external payable returns (bytes32 canonicalTxHash) {
206:         require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
207:         canonicalTxHash = _requestL2TransactionSender( // <= FOUND
208:             BridgehubL2TransactionRequest({
209:                 sender: msg.sender,
210:                 contractL2: _contractL2,
211:                 mintValue: msg.value,
212:                 l2Value: _l2Value,
213:                 l2GasLimit: _l2GasLimit,
214:                 l2Calldata: _calldata,
215:                 l2GasPerPubdataByteLimit: _l2GasPerPubdataByteLimit,
216:                 factoryDeps: _factoryDeps,
217:                 refundRecipient: _refundRecipient
218:             })
219:         );
220:         IL1SharedBridge(s.baseTokenBridge).bridgehubDepositBaseToken{value: msg.value}(
221:             s.chainId,
222:             msg.sender,
223:             ETH_TOKEN_ADDRESS,
224:             msg.value
225:         );
226:     }

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L294)']
```solidity
289:     function _serializeL2Transaction(
290:         WritePriorityOpParams memory _priorityOpParams,
291:         bytes memory _calldata,
292:         bytes[] memory _factoryDeps
293:     ) internal pure returns (L2CanonicalTransaction memory transaction) {
294:         transaction = L2CanonicalTransaction({ // <= FOUND
295:             txType: PRIORITY_OPERATION_L2_TX_TYPE,
296:             from: uint256(uint160(_priorityOpParams.sender)),
297:             to: uint256(uint160(_priorityOpParams.contractAddressL2)),
298:             gasLimit: _priorityOpParams.l2GasLimit,
299:             gasPerPubdataByteLimit: _priorityOpParams.l2GasPricePerPubdata,
300:             maxFeePerGas: uint256(_priorityOpParams.l2GasPrice),
301:             maxPriorityFeePerGas: uint256(0),
302:             paymaster: uint256(0),
303:             
304:             nonce: uint256(_priorityOpParams.txId),
305:             value: _priorityOpParams.l2Value,
306:             reserved: [_priorityOpParams.valueToMint, uint256(uint160(_priorityOpParams.refundRecipient)), 0, 0],
307:             data: _calldata,
308:             signature: new bytes(0),
309:             factoryDeps: _hashFactoryDeps(_factoryDeps),
310:             paymasterInput: new bytes(0),
311:             reservedDynamic: new bytes(0)
312:         });
313:     }

```
['[205](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L205-L218)']
```solidity
205:     function _addOneFunction(address _facet, bytes4 _selector, bool _isSelectorFreezable) private { // <= FOUND
206:         DiamondStorage storage ds = getDiamondStorage();
207: 
208:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16();
209: 
210:         
211:         
212:         
213:         if (selectorPosition != 0) {
214:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
215:             require(_isSelectorFreezable == ds.selectorToFacet[selector0].isFreezable, "J1");
216:         }
217: 
218:         ds.selectorToFacet[_selector] = SelectorToFacet({ // <= FOUND
219:             facetAddress: _facet,
220:             selectorPosition: selectorPosition,
221:             isFreezable: _isSelectorFreezable
222:         });
223:         ds.facetToSelectors[_facet].selectors.push(_selector);
224:     }

```
['[70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L70-L75)']
```solidity
70:     function sendL2ToL1Log(
71:         bool _isService,
72:         bytes32 _key,
73:         bytes32 _value
74:     ) external onlyCallFromSystemContract returns (uint256 logIdInMerkleTree) {
75:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({ // <= FOUND
76:             l2ShardId: 0,
77:             isService: _isService,
78:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
79:             sender: msg.sender,
80:             key: _key,
81:             value: _value
82:         });
83:         logIdInMerkleTree = _processL2ToL1Log(l2ToL1Log);
84: 
85:         
86:         
87:         
88:         
89:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) + 2 * keccakGasCost(64);
90:         SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), 0);
91:     }

```
['[116](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L116-L125)']
```solidity
116:     function sendToL1(bytes calldata _message) external override returns (bytes32 hash) { // <= FOUND
117:         uint256 gasBeforeMessageHashing = gasleft();
118:         hash = EfficientCall.keccak(_message);
119:         uint256 gasSpentOnMessageHashing = gasBeforeMessageHashing - gasleft();
120: 
121:         
122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash));
123: 
124:         
125:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({ // <= FOUND
126:             l2ShardId: 0,
127:             isService: true,
128:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
129:             sender: address(this),
130:             key: bytes32(uint256(uint160(msg.sender))),
131:             value: hash
132:         });
133:         _processL2ToL1Log(l2ToL1Log);
134: 
135:         
136:         uint256 pubdataLen;
137:         unchecked {
138:             
139:             
140:             pubdataLen = 4 + _message.length + L2_TO_L1_LOG_SERIALIZE_SIZE;
141:         }
142: 
143:         
144:         
145:         
146:         
147:         
148:         uint256 gasToPay = keccakGasCost(L2_TO_L1_LOG_SERIALIZE_SIZE) +
149:             3 *
150:             keccakGasCost(64) +
151:             gasSpentOnMessageHashing +
152:             COMPUTATIONAL_PRICE_FOR_PUBDATA *
153:             pubdataLen;
154:         SystemContractHelper.burnGas(Utils.safeCastToU32(gasToPay), uint32(pubdataLen));
155: 
156:         emit L1MessageSent(msg.sender, hash, _message);
157:     }

```
['[314](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L314-L316)']
```solidity
314:     function _setNewL2BlockData(uint128 _l2BlockNumber, uint128 _l2BlockTimestamp, bytes32 _prevL2BlockHash) internal { // <= FOUND
315:         
316:         currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp}); // <= FOUND
317: 
318:         
319:         _setL2BlockHash(_l2BlockNumber - 1, _prevL2BlockHash);
320: 
321:         
322:         currentL2BlockTxsRollingHash = bytes32(0);
323:     }

```
['[444](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L444-L459)']
```solidity
444:     function setNewBatch(
445:         bytes32 _prevBatchHash,
446:         uint128 _newTimestamp,
447:         uint128 _expectedNewNumber,
448:         uint256 _baseFee
449:     ) external onlyCallFromBootloader {
450:         (uint128 previousBatchNumber, uint128 previousBatchTimestamp) = getBatchNumberAndTimestamp();
451:         require(_newTimestamp > previousBatchTimestamp, "Timestamps should be incremental");
452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453: 
454:         _ensureBatchConsistentWithL2Block(_newTimestamp);
455: 
456:         batchHashes[previousBatchNumber] = _prevBatchHash;
457: 
458:         
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp}); // <= FOUND
460: 
461:         currentBatchInfo = newBlockInfo;
462: 
463:         baseFee = _baseFee;
464: 
465:         
466:         SystemContractHelper.toL1(false, bytes32(uint256(SystemLogKey.PREV_BATCH_HASH_KEY)), _prevBatchHash);
467:     }

```
['[471](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L471-L476)']
```solidity
471:     function unsafeOverrideBatch(
472:         uint256 _newTimestamp,
473:         uint256 _number,
474:         uint256 _baseFee
475:     ) external onlyCallFromBootloader {
476:         BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)}); // <= FOUND
477:         currentBatchInfo = newBlockInfo;
478: 
479:         baseFee = _baseFee;
480:     }

```


</details>

## [Gas-69] An inefficient way of checking if a integer is even is being used (X % 2 == 0)

### Resolution 
Checking if an integer is even in Solidity can be optimized for gas efficiency. Commonly, developers use the modulus operator (%), as in X % 2 == 0. However, this approach may not be the most gas-efficient due to the cost of arithmetic operations in Solidity. A more efficient method is to use the modulus with uint(1), such as X % uint(1) == 0. This approach takes advantage of Solidity's handling of the modulus operation with smaller integers, potentially resulting in lower gas usage. 

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30-L30)']
```solidity
30:             currentHash = (_index % 2 == 0) // <= FOUND
31:                 ? _efficientHash(currentHash, _path[i])
32:                 : _efficientHash(_path[i], currentHash);

```


</details>

## [Gas-70] Internal functions never used once can be removed

### Resolution 
Internal functions which are never used use unnecessary gas and should be safely removed.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[25](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L25-L25)']
```solidity
25:     function _getAbiParams() internal view returns (uint256 value, bool isSystemCall, address to)  // <= FOUND

```
['[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L88-L88)']
```solidity
88:     function delegateCall( // <= FOUND
89:         uint256 _gas,
90:         address _address,
91:         bytes calldata _data
92:     ) internal returns (bytes memory returnData) 

```
['[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L124-L124)']
```solidity
124:     function packPrecompileParams( // <= FOUND
125:         uint32 _inputMemoryOffset,
126:         uint32 _inputMemoryLength,
127:         uint32 _outputMemoryOffset,
128:         uint32 _outputMemoryLength,
129:         uint64 _perPrecompileInterpreted
130:     ) internal pure returns (uint256 rawParams) 

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L181-L181)']
```solidity
181:     function eventInitialize(uint256 initializer, uint256 value1) internal  // <= FOUND

```
['[191](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L191-L191)']
```solidity
191:     function eventWrite(uint256 value1, uint256 value2) internal  // <= FOUND

```
['[307](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L307-L307)']
```solidity
307:     function getCalldataPtr() internal view returns (uint256 ptr)  // <= FOUND

```
['[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L94-L94)']
```solidity
94:     function isEthToken(uint256 _addr) internal pure returns (bool)  // <= FOUND

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L32-L32)']
```solidity
32:     function safeCastToU24(uint256 _x) internal pure returns (uint24)  // <= FOUND

```


</details>

## [Gas-71] Empty functions should be removed to save gas

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60-L60)']
```solidity
60:     function initialize() external reentrancyGuardInitializer {}

```


</details>

## [Gas-72] There are comparisons to boolean literals (true and false), these can be simplified to save gas

### Resolution 
In Solidity, gas optimization is crucial due to the cost associated with executing operations on the Ethereum network. Simplifying comparisons to boolean literals is one such optimization technique. Instead of explicitly comparing a boolean expression to true or false, you can use the expression directly or its negation. For example, replace if (x == true) with if (x) and if (x == false) with if (!x). This simplification reduces the bytecode size of the contract, thereby saving gas. It also enhances code readability and clarity.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L68)']
```solidity
68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator"); // <= FOUND

```


</details>

## [Gas-73] Only emit event in setter function if the state variable was changed

### Resolution 
Emitting events in setter functions of smart contracts only when state variables change saves gas. This is because emitting events consumes gas, and unnecessary events, where no actual state change occurs, lead to wasteful consumption.

Num of instances: 13

### Findings 


<details><summary>Click to show findings</summary>

['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51-L56)']
```solidity
51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin { // <= FOUND
52:         
53:         address oldPendingAdmin = pendingAdmin;
54:         
55:         pendingAdmin = _newPendingAdmin;
56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin); // <= FOUND
57:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51-L56)']
```solidity
51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin { // <= FOUND
52:         
53:         address oldPendingAdmin = pendingAdmin;
54:         
55:         pendingAdmin = _newPendingAdmin;
56:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin); // <= FOUND
57:     }

```
['[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96-L98)']
```solidity
96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner { // <= FOUND
97:         executionDelay = _executionDelay;
98:         emit NewExecutionDelay(_executionDelay); // <= FOUND
99:     }

```
['[23](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23-L28)']
```solidity
23:     function setPendingAdmin(address _newPendingAdmin) external onlyAdmin { // <= FOUND
24:         
25:         address oldPendingAdmin = s.pendingAdmin;
26:         
27:         s.pendingAdmin = _newPendingAdmin;
28:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin); // <= FOUND
29:     }

```
['[45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45-L47)']
```solidity
45:     function setValidator(address _validator, bool _active) external onlyStateTransitionManager { // <= FOUND
46:         s.validators[_validator] = _active;
47:         emit ValidatorStatusUpdate(_validator, _active); // <= FOUND
48:     }

```
['[51](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L51-L54)']
```solidity
51:     function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager { // <= FOUND
52:         
53:         s.zkPorterIsAvailable = _zkPorterIsAvailable;
54:         emit IsPorterAvailableStatusUpdate(_zkPorterIsAvailable); // <= FOUND
55:     }

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L58-L63)']
```solidity
58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager { // <= FOUND
59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
60: 
61:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;
62:         s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit); // <= FOUND
64:     }

```
['[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79-L86)']
```solidity
79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager { // <= FOUND
80:         uint128 oldNominator = s.baseTokenGasPriceMultiplierNominator;
81:         uint128 oldDenominator = s.baseTokenGasPriceMultiplierDenominator;
82: 
83:         s.baseTokenGasPriceMultiplierNominator = _nominator;
84:         s.baseTokenGasPriceMultiplierDenominator = _denominator;
85: 
86:         emit NewBaseTokenMultiplier(oldNominator, oldDenominator, _nominator, _denominator); // <= FOUND
87:     }

```
['[177](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L227)']
```solidity
177:     function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal { // <= FOUND
178:         bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
179:         uint256[] memory uintEmptyArray;
180:         bytes[] memory bytesEmptyArray;
181: 
182:         L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
183:             txType: SYSTEM_UPGRADE_L2_TX_TYPE,
184:             from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
185:             to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
186:             gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
187:             gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
188:             maxFeePerGas: uint256(0),
189:             maxPriorityFeePerGas: uint256(0),
190:             paymaster: uint256(0),
191:             
192:             nonce: protocolVersion,
193:             value: 0,
194:             reserved: [uint256(0), 0, 0, 0],
195:             data: systemContextCalldata,
196:             signature: new bytes(0),
197:             factoryDeps: uintEmptyArray,
198:             paymasterInput: new bytes(0),
199:             reservedDynamic: new bytes(0)
200:         });
201: 
202:         ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
203:             l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
204:             factoryDeps: bytesEmptyArray,
205:             bootloaderHash: bytes32(0),
206:             defaultAccountHash: bytes32(0),
207:             verifier: address(0),
208:             verifierParams: VerifierParams({
209:                 recursionNodeLevelVkHash: bytes32(0),
210:                 recursionLeafLevelVkHash: bytes32(0),
211:                 recursionCircuitsSetVksHash: bytes32(0)
212:             }),
213:             l1ContractsUpgradeCalldata: new bytes(0),
214:             postUpgradeCalldata: new bytes(0),
215:             upgradeTimestamp: 0,
216:             newProtocolVersion: protocolVersion
217:         });
218: 
219:         Diamond.FacetCut[] memory emptyArray;
220:         Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
221:             facetCuts: emptyArray,
222:             initAddress: genesisUpgrade,
223:             initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
224:         });
225: 
226:         IAdmin(_chainContract).executeUpgrade(cutData);
227:         emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion); // <= FOUND
228:     }

```
['[249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249-L250)']
```solidity
249:     function updateDelay(uint256 _newDelay) external onlySelf { // <= FOUND
250:         emit ChangeMinDelay(minDelay, _newDelay); // <= FOUND
251:         minDelay = _newDelay;
252:     }

```
['[256](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256-L257)']
```solidity
256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf { // <= FOUND
257:         emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil); // <= FOUND
258:         securityCouncil = _newSecurityCouncil;
259:     }

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L65-L68)']
```solidity
65:     function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall { // <= FOUND
66:         accountInfo[msg.sender].supportedAAVersion = _version;
67: 
68:         emit AccountVersionUpdated(msg.sender, _version); // <= FOUND
69:     }

```
['[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67-L75)']
```solidity
67:     function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager { // <= FOUND
68:         
69:         
70:         require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");
71: 
72:         FeeParams memory oldFeeParams = s.feeParams;
73:         s.feeParams = _newFeeParams;
74: 
75:         emit NewFeeParams(oldFeeParams, _newFeeParams); // <= FOUND
76:     }

```


</details>

## [Gas-74] It is a waste of GAS to emit variable literals

### Resolution 
Emitting variable literals (true, false, 'hello', 1 etc...) in events is inefficient, as it consumes extra gas without providing added value. These literals are fixed values that can be accessed or hardcoded elsewhere in the smart contract or application, making their inclusion in events redundant and an unnecessary drain on resources during transaction execution.

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68-L68)']
```solidity
68:         emit NewPendingAdmin(currentPendingAdmin, address(0)); // <= FOUND

```
['[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L47-L47)']
```solidity
47:         emit ChangeSecurityCouncil(address(0), _securityCouncil); // <= FOUND

```
['[50](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L50-L50)']
```solidity
50:         emit ChangeMinDelay(0, _minDelay); // <= FOUND

```
['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L40)']
```solidity
40:         emit NewPendingAdmin(pendingAdmin, address(0)); // <= FOUND

```


</details>

## [Gas-75] Short circuit before external calls

### Resolution 
Short-circuit evaluation in programming optimizes conditional statements by evaluating expressions in order of least computational complexity. Applying this to smart contracts, especially those on blockchain networks where computation costs gas, can significantly reduce unnecessary operations and associated costs. Prioritizing checks against constants, literals, and local state over function calls ensures that if a condition can be resolved without interacting with function calls, it is.

Num of instances: 2

### Findings 


<details><summary>Click to show findings</summary>

['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87-L90)']
```solidity
87:         
88:         require( // <= FOUND
89:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge || // <= FOUND
90:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge, // <= FOUND
91:             "mq"
92:         );

```
['[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/interfaces/ISystemContract.sol#L21-L23)']
```solidity
21:         require( // <= FOUND
22:             SystemContractHelper.isSystemCall() || SystemContractHelper.isSystemContract(msg.sender), // <= FOUND
23:             "This method require system call flag" // <= FOUND
24:         );

```


</details>

## [Gas-76] Use OZ Array.unsafeAccess() to avoid repeated array length checks

### Resolution 
The OpenZeppelin Array.unsafeAccess() method is a optimization strategy for Solidity, aimed at reducing gas costs by bypassing automatic length checks on storage array accesses. In Solidity, every access to an array element involves a hidden gas cost due to a length check, ensuring that accesses do not exceed the array bounds. However, if a developer has already verified the array's bounds earlier in the function or knows through logic that the access is safe, directly accessing the array elements without redundant length checks can save gas. This approach requires careful consideration to avoid out-of-bounds errors, as it trades off safety checks for efficiency.

Num of instances: 156

### Findings 


<details><summary>Click to show findings</summary>

['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226-L226)']
```solidity
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data); // <= FOUND

```
['[117](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117-L117)']
```solidity
117:                 committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp); // <= FOUND

```
['[136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L136-L136)']
```solidity
136:                 committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp); // <= FOUND

```
['[186](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186-L187)']
```solidity
186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
187:                     _newBatchesData[i].batchNumber // <= FOUND
188:                 );

```
['[210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210-L210)']
```solidity
210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber); // <= FOUND

```
['[258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L258-L258)']
```solidity
258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0)); // <= FOUND

```
['[292](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L292-L294)']
```solidity
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i], // <= FOUND
295:                 expectedUpgradeTxHash
296:             );

```
['[352](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L352-L352)']
```solidity
352:             _executeOneBatch(_batchesData[i], i); // <= FOUND

```
['[353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353)']
```solidity
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment); // <= FOUND

```
['[407](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L407-L408)']
```solidity
407:             require(
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified], // <= FOUND
409:                 "o1"
410:             );

```
['[412](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L412-L412)']
```solidity
412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment; // <= FOUND

```
['[413](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L413-L413)']
```solidity
413:             proofPublicInput[i] = _getBatchProofPublicInput( // <= FOUND
414:                 prevBatchCommitment,
415:                 currentBatchCommitment,
416:                 verifierParams
417:             );

```
['[581](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581-L581)']
```solidity
581:             blobAuxOutputWords[i * 2] = _blobHashes[i]; // <= FOUND

```
['[582](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L582-L582)']
```solidity
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i]; // <= FOUND

```
['[668](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L668-L670)']
```solidity
668:             require(
669:                 (_blobHashes[i] == bytes32(0) && blobCommitments[i] == bytes32(0)) || // <= FOUND
670:                     (_blobHashes[i] != bytes32(0) && blobCommitments[i] != bytes32(0)), // <= FOUND
671:                 "bh"
672:             );

```
['[209](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L209-L209)']
```solidity
209:             address facetAddr = ds.facets[i]; // <= FOUND

```
['[212](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L212-L212)']
```solidity
212:             result[i] = Facet(facetAddr, facetToSelectors.selectors); // <= FOUND

```
['[357](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L357-L357)']
```solidity
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]); // <= FOUND

```
['[227](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L227-L228)']
```solidity
227:             require(
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]), // <= FOUND
229:                 "Wrong factory dep hash"
230:             );

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L102-L102)']
```solidity
102:             Action action = facetCuts[i].action; // <= FOUND

```
['[103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103-L103)']
```solidity
103:             address facet = facetCuts[i].facet; // <= FOUND

```
['[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L104-L104)']
```solidity
104:             bool isFacetFreezable = facetCuts[i].isFreezable; // <= FOUND

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105-L105)']
```solidity
105:             bytes4[] memory selectors = facetCuts[i].selectors; // <= FOUND

```
['[139](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L139-L139)']
```solidity
139:             bytes4 selector = _selectors[i]; // <= FOUND

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30-L32)']
```solidity
30:             currentHash = (_index % 2 == 0)
31:                 ? _efficientHash(currentHash, _path[i]) // <= FOUND
32:                 : _efficientHash(_path[i], currentHash); // <= FOUND

```
['[249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L249-L249)']
```solidity
249:             sumOfValues += _deployments[i].value; // <= FOUND

```
['[254](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L254-L254)']
```solidity
254:             this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender); // <= FOUND

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L39-L39)']
```solidity
39:                 uint256 index = _immutables[i].index; // <= FOUND

```
['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L40-L40)']
```solidity
40:                 bytes32 value = _immutables[i].value; // <= FOUND

```
['[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L31-L31)']
```solidity
31:                 _markBytecodeAsPublished(_hashes[i], _shouldSendToL1); // <= FOUND

```
['[211](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L211-L211)']
```solidity
211:             l2ToL1LogsTreeArray[i] = hashedLog; // <= FOUND

```
['[219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L219-L219)']
```solidity
219:             l2ToL1LogsTreeArray[i] = L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH; // <= FOUND

```
['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L225-L225)']
```solidity
225:                 l2ToL1LogsTreeArray[i] = keccak256( // <= FOUND
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L52-L52)']
```solidity
52:             blobHashes[i] = blobHash; // <= FOUND

```
['[215](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L215-L215)']
```solidity
215:         require(!isWithdrawalFinalized[_l2BatchNumber][_l2MessageIndex], "pw"); // <= FOUND

```
['[417](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L417-L417)']
```solidity
417:         require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized"); // <= FOUND

```
['[418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418-L418)']
```solidity
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true; // <= FOUND

```
['[154](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L154-L154)']
```solidity
154:         depositAmount[msg.sender][_l1Token][l2TxHash] = _amount; // <= FOUND

```
['[185](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L185-L185)']
```solidity
185:         uint256 amount = depositAmount[_depositSender][_l1Token][_l2TxHash]; // <= FOUND

```
['[187](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L187-L187)']
```solidity
187:         delete depositAmount[_depositSender][_l1Token][_l2TxHash]; // <= FOUND

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L237-L237)']
```solidity
237:         require(depositHappened[_chainId][_txHash] == 0x00, "ShB tx hap"); // <= FOUND

```
['[238](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L238-L238)']
```solidity
238:         depositHappened[_chainId][_txHash] = _txDataHash; // <= FOUND

```
['[340](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340-L340)']
```solidity
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash]; // <= FOUND

```
['[343](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L343-L343)']
```solidity
343:                 delete depositHappened[_chainId][_l2TxHash]; // <= FOUND

```
['[600](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L600-L601)']
```solidity
600:         
601:         depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash; // <= FOUND

```
['[76](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L76-L76)']
```solidity
76:         return IStateTransitionManager(stateTransitionManager[_chainId]).stateTransition(_chainId); // <= FOUND

```
['[132](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L132-L132)']
```solidity
132:         require(stateTransitionManager[_chainId] == address(0), "Bridgehub: chainId already registered"); // <= FOUND

```
['[134](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L134-L134)']
```solidity
134:         stateTransitionManager[_chainId] = _stateTransitionManager; // <= FOUND

```
['[112](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L112-L112)']
```solidity
112:         l2BridgeAddress[ERA_CHAIN_ID] = ERA_ERC20_BRIDGE_ADDRESS; // <= FOUND

```
['[143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143-L143)']
```solidity
143:         l2BridgeAddress[_chainId] = _l2BridgeAddress; // <= FOUND

```
['[188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L188-L188)']
```solidity
188:         require(l2BridgeAddress[_chainId] != address(0), "ShB l2 bridge not deployed"); // <= FOUND

```
['[219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L219-L223)']
```solidity
219:             request = L2TransactionRequestTwoBridgesInner({
220:                 magicValue: TWO_BRIDGES_MAGIC_VALUE,
221:                 l2Contract: l2BridgeAddress[_chainId], // <= FOUND
222:                 l2Calldata: l2TxCalldata,
223:                 factoryDeps: new bytes[](0), // <= FOUND
224:                 txDataHash: txDataHash
225:             });

```
['[468](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L468-L468)']
```solidity
468:             address l2Sender = baseTokenWithdrawal ? L2_BASE_TOKEN_SYSTEM_CONTRACT_ADDR : l2BridgeAddress[_chainId]; // <= FOUND

```
['[563](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L563-L563)']
```solidity
563:         require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep"); // <= FOUND

```
['[584](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L584-L592)']
```solidity
584:             L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
585:                 chainId: ERA_CHAIN_ID,
586:                 l2Contract: l2BridgeAddress[ERA_CHAIN_ID], // <= FOUND
587:                 mintValue: msg.value, 
588:                 l2Value: 0, 
589:                 l2Calldata: l2TxCalldata,
590:                 l2GasLimit: _l2TxGasLimit,
591:                 l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
592:                 factoryDeps: new bytes[](0), // <= FOUND
593:                 refundRecipient: refundRecipient
594:             });

```
['[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L106-L106)']
```solidity
106:         uint256 timestamp = timestamps[_id]; // <= FOUND

```
['[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L156-L156)']
```solidity
156:         delete timestamps[_id]; // <= FOUND

```
['[179](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L179-L180)']
```solidity
179:         
180:         timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP; // <= FOUND

```
['[219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L219-L219)']
```solidity
219:         timestamps[_id] = block.timestamp + _delay; // <= FOUND

```
['[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L180-L180)']
```solidity
180:         bytes[] memory bytesEmptyArray; // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L68)']
```solidity
68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator"); // <= FOUND

```
['[79](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L79-L79)']
```solidity
79:         if (validators[_chainId][_newValidator]) { // <= FOUND

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82-L82)']
```solidity
82:         validators[_chainId][_newValidator] = true; // <= FOUND

```
['[88](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L88-L88)']
```solidity
88:         if (!validators[_chainId][_validator]) { // <= FOUND

```
['[91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91-L91)']
```solidity
91:         validators[_chainId][_validator] = false; // <= FOUND

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L39-L39)']
```solidity
39:         s.validators[_initializeData.validatorTimelock] = true; // <= FOUND

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L41-L41)']
```solidity
41:         s.storedBatchHashes[0] = _initializeData.storedBatchZero; // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L46-L46)']
```solidity
46:         s.validators[_validator] = _active; // <= FOUND

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L39-L39)']
```solidity
39:         uint8 pubdataSource = uint8(bytes1(_newBatch.pubdataCommitments[0])); // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L55-L57)']
```solidity
55:             
56:             
57:             blobHashes[0] = logOutput.blob1Hash; // <= FOUND

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L56-L56)']
```solidity
56:             blobHashes[1] = logOutput.blob2Hash; // <= FOUND

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L58-L59)']
```solidity
58:             
59:             blobCommitments = _verifyBlobInformation(_newBatch.pubdataCommitments[1:], blobHashes); // <= FOUND

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L61-L64)']
```solidity
61:             
62:             require(
63:                 logOutput.pubdataHash ==
64:                     keccak256(_newBatch.pubdataCommitments[1:_newBatch.pubdataCommitments.length - 32]), // <= FOUND
65:                 "wp"
66:             );

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L55-L55)']
```solidity
55:             blobHashes[0] = logOutput.blob1Hash; // <= FOUND

```
['[67](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L67-L68)']
```solidity
67:             blobCommitments[0] = bytes32( // <= FOUND
68:                 _newBatch.pubdataCommitments[_newBatch.pubdataCommitments.length - 32:_newBatch // <= FOUND
69:                     .pubdataCommitments
70:                     .length]
71:             );

```
['[233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L233-L234)']
```solidity
233:         
234:         require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i");  // <= FOUND

```
['[260](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L260-L260)']
```solidity
260:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData); // <= FOUND

```
['[324](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L324-L325)']
```solidity
324:         require(
325:             _hashStoredBatchInfo(_storedBatch) == s.storedBatchHashes[currentBatchNumber], // <= FOUND
326:             "exe10" 
327:         );

```
['[333](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L333-L334)']
```solidity
333:         
334:         s.l2LogsRootHashes[currentBatchNumber] = _storedBatch.l2LogsTreeRoot; // <= FOUND

```
['[402](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L402-L403)']
```solidity
402:         
403:         require(_hashStoredBatchInfo(_prevBatch) == s.storedBatchHashes[currentTotalBatchesVerified], "t1"); // <= FOUND

```
['[643](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L643-L646)']
```solidity
643:             
644:             
645:             bytes32 openingPoint = bytes32(
646:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET]))) // <= FOUND
647:             );

```
['[647](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L647-L650)']
```solidity
647:             _pointEvaluationPrecompile(
648:                 blobVersionedHash,
649:                 openingPoint,
650:                 _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE] // <= FOUND
651:             );

```
['[654](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L654-L656)']
```solidity
654:             
655:             blobCommitments[versionedHashIndex] = keccak256( // <= FOUND
656:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET]) // <= FOUND
657:             );

```
['[113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L113-L113)']
```solidity
113:         return s.validators[_address]; // <= FOUND

```
['[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L118-L118)']
```solidity
118:         return s.l2LogsRootHashes[_batchNumber]; // <= FOUND

```
['[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L123-L123)']
```solidity
123:         return s.storedBatchHashes[_batchNumber]; // <= FOUND

```
['[168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L168-L170)']
```solidity
168:         
169:         
170:         uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length; // <= FOUND

```
['[214](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L214-L214)']
```solidity
214:             bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0]; // <= FOUND

```
['[210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210-L210)']
```solidity
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr]; // <= FOUND

```
['[219](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L219-L219)']
```solidity
219:         return ds.facetToSelectors[_facet].selectors; // <= FOUND

```
['[223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L223-L224)']
```solidity
223:     
224:     function facetAddresses() external view returns (address[] memory) { // <= FOUND

```
['[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L124-L124)']
```solidity
124:         bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber]; // <= FOUND

```
['[197](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L197-L204)']
```solidity
197:     
198:     function requestL2Transaction(
199:         address _contractL2,
200:         uint256 _l2Value,
201:         bytes calldata _calldata,
202:         uint256 _l2GasLimit,
203:         uint256 _l2GasPerPubdataByteLimit,
204:         bytes[] calldata _factoryDeps, // <= FOUND
205:         address _refundRecipient
206:     ) external payable returns (bytes32 canonicalTxHash) {

```
['[258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L262)']
```solidity
258:     function _requestL2Transaction(
259:         uint256 _mintValue,
260:         WritePriorityOpParams memory _params,
261:         bytes memory _calldata,
262:         bytes[] memory _factoryDeps // <= FOUND
263:     ) internal returns (bytes32 canonicalTxHash) {

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L289-L292)']
```solidity
289:     function _serializeL2Transaction(
290:         WritePriorityOpParams memory _priorityOpParams,
291:         bytes memory _calldata,
292:         bytes[] memory _factoryDeps // <= FOUND
293:     ) internal pure returns (L2CanonicalTransaction memory transaction) {

```
['[316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L316-L320)']
```solidity
316:     
317:     function _writePriorityOp(
318:         WritePriorityOpParams memory _priorityOpParams,
319:         bytes memory _calldata,
320:         bytes[] memory _factoryDeps // <= FOUND
321:     ) internal returns (bytes32 canonicalTxHash) {

```
['[353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L353-L354)']
```solidity
353:     
354:     function _hashFactoryDeps(bytes[] memory _factoryDeps) internal pure returns (uint256[] memory hashedFactoryDeps) { // <= FOUND

```
['[22](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L22-L22)']
```solidity
22:         require(s.validators[msg.sender], "StateTransition Chain: not validator"); // <= FOUND

```
['[45](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L45-L46)']
```solidity
45:         require(
46:             s.validators[msg.sender] || msg.sender == s.stateTransitionManager, // <= FOUND
47:             "StateTransition Chain: Only by validator or state transition manager"
48:         );

```
['[18](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L18-L18)']
```solidity
18:     bytes[] factoryDeps; // <= FOUND

```
['[180](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L180-L186)']
```solidity
180:     
184:     function _setL2SystemContractUpgrade(
185:         L2CanonicalTransaction calldata _l2ProtocolUpgradeTx,
186:         bytes[] calldata _factoryDeps, // <= FOUND
187:         uint256 _newProtocolVersion
188:     ) internal returns (bytes32) {

```
['[222](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L222-L225)']
```solidity
222:     
225:     function _verifyFactoryDeps(bytes[] calldata _factoryDeps, uint256[] calldata _expectedHashes) private pure { // <= FOUND

```
['[53](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L53-L53)']
```solidity
53:         address[] facets; // <= FOUND

```
['[192](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L192-L192)']
```solidity
192:         uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length; // <= FOUND

```
['[195](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L195-L195)']
```solidity
195:             ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16(); // <= FOUND

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L208-L208)']
```solidity
208:         uint16 selectorPosition = (ds.facetToSelectors[_facet].selectors.length).toUint16(); // <= FOUND

```
['[223](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L223-L223)']
```solidity
223:         ds.facetToSelectors[_facet].selectors.push(_selector); // <= FOUND

```
['[233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L233-L233)']
```solidity
233:         uint256 lastSelectorPosition = ds.facetToSelectors[_facet].selectors.length - 1; // <= FOUND

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L237-L237)']
```solidity
237:             bytes4 lastSelector = ds.facetToSelectors[_facet].selectors[lastSelectorPosition]; // <= FOUND

```
['[239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L239-L239)']
```solidity
239:             ds.facetToSelectors[_facet].selectors[selectorPosition] = lastSelector; // <= FOUND

```
['[244](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L244-L245)']
```solidity
244:         
245:         ds.facetToSelectors[_facet].selectors.pop(); // <= FOUND

```
['[261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L261-L262)']
```solidity
261:         
262:         uint256 facetPosition = ds.facetToSelectors[_facet].facetPosition; // <= FOUND

```
['[266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L266-L266)']
```solidity
266:             address lastFacet = ds.facets[lastFacetPosition]; // <= FOUND

```
['[268](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L268-L268)']
```solidity
268:             ds.facets[facetPosition] = lastFacet; // <= FOUND

```
['[269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L269-L269)']
```solidity
269:             ds.facetToSelectors[lastFacet].facetPosition = facetPosition.toUint16(); // <= FOUND

```
['[136](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IGetters.sol#L136-L137)']
```solidity
136:     
137:     function facetAddresses() external view returns (address[] memory facets); // <= FOUND

```
['[128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L128-L128)']
```solidity
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE]; // <= FOUND

```
['[143](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L143-L143)']
```solidity
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr])); // <= FOUND

```
['[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L147-L151)']
```solidity
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len] // <= FOUND
152:             );

```
['[168](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L168-L169)']
```solidity
168:             uint256 compressedEnumIndex = _sliceToUint256(
169:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + _enumerationIndexSize] // <= FOUND
170:             );

```
['[200](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L200-L201)']
```solidity
200:         
201:         uint32 numberOfL2ToL1Logs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND

```
['[207](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L207-L208)']
```solidity
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE] // <= FOUND
209:             );

```
['[233](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L233-L234)']
```solidity
233:         
234:         uint32 numberOfMessages = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND

```
['[237](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L237-L237)']
```solidity
237:             uint32 currentMessageLength = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND

```
['[239](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L239-L240)']
```solidity
239:             bytes32 hashedMessage = EfficientCall.keccak(
240:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentMessageLength] // <= FOUND
241:             );

```
['[251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L251-L252)']
```solidity
251:         
252:         uint32 numberOfBytecodes = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND

```
['[255](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L255-L256)']
```solidity
255:             uint32 currentBytecodeLength = uint32(
256:                 bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4]) // <= FOUND
257:             );

```
['[259](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L259-L263)']
```solidity
259:             reconstructedChainedL1BytecodesRevealDataHash = keccak256(
260:                 abi.encode(
261:                     reconstructedChainedL1BytecodesRevealDataHash,
262:                     Utils.hashL2Bytecode(
263:                         _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + currentBytecodeLength] // <= FOUND
264:                     )
265:                 )
266:             );

```
['[279](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L279-L285)']
```solidity
279:         
280:         
281:         
282:         
283:         
284:         require(
285:             uint256(uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr]))) == // <= FOUND
286:                 STATE_DIFF_COMPRESSION_VERSION_NUMBER,
287:             "state diff compression version mismatch"
288:         );

```
['[286](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L286-L286)']
```solidity
286:         uint24 compressedStateDiffSize = uint24(bytes3(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 3])); // <= FOUND

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L289-L289)']
```solidity
289:         uint8 enumerationIndexSize = uint8(bytes1(_totalL2ToL1PubdataAndStateDiffs[calldataPtr])); // <= FOUND

```
['[292](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L292-L292)']
```solidity
292:         bytes calldata compressedStateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + // <= FOUND
293:             compressedStateDiffSize];

```
['[296](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L296-L296)']
```solidity
296:         bytes calldata totalL2ToL1Pubdata = _totalL2ToL1PubdataAndStateDiffs[:calldataPtr]; // <= FOUND

```
['[300](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L300-L300)']
```solidity
300:         uint32 numberOfStateDiffs = uint32(bytes4(_totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + 4])); // <= FOUND

```
['[303](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L303-L303)']
```solidity
303:         bytes calldata stateDiffs = _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + // <= FOUND
304:             (numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE)];

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L48-L48)']
```solidity
48:         (, uint256 minNonce) = _splitRawNonce(rawNonces[addressAsKey]); // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L59-L59)']
```solidity
59:         return rawNonces[addressAsKey]; // <= FOUND

```
['[69](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L69-L69)']
```solidity
69:         uint256 oldRawNonce = rawNonces[addressAsKey]; // <= FOUND

```
['[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L72-L72)']
```solidity
72:             rawNonces[addressAsKey] = (oldRawNonce + _value); // <= FOUND

```
['[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L94-L94)']
```solidity
94:         nonceValues[addressAsKey][_key] = _value; // <= FOUND

```
['[104](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L104-L104)']
```solidity
104:         return nonceValues[addressAsKey][_key]; // <= FOUND

```
['[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L118-L118)']
```solidity
118:             rawNonces[addressAsKey] = oldRawNonce + 1; // <= FOUND

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L127-L127)']
```solidity
127:         (deploymentNonce, ) = _splitRawNonce(rawNonces[addressAsKey]); // <= FOUND

```
['[144](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L144-L144)']
```solidity
144:             rawNonces[addressAsKey] = (oldRawNonce + DEPLOY_NONCE_MULTIPLIER); // <= FOUND

```
['[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L156-L156)']
```solidity
156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0); // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L55-L55)']
```solidity
55:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_ONE_HASH_KEY)), blobHashes[0]); // <= FOUND

```
['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L56-L56)']
```solidity
56:         SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_TWO_HASH_KEY)), blobHashes[1]); // <= FOUND

```
['[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L149-L151)']
```solidity
149:             
150:             
151:             hash = batchHashes[_block]; // <= FOUND

```
['[167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L167-L167)']
```solidity
167:         hash = batchHashes[_batchNumber]; // <= FOUND

```
['[456](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L456-L456)']
```solidity
456:         batchHashes[previousBatchNumber] = _prevBatchHash; // <= FOUND

```
['[510](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L510-L510)']
```solidity
510:         hash = batchHashes[_blockNumber]; // <= FOUND

```
['[95](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L95-L95)']
```solidity
95:         address currentL1Token = l1TokenAddress[expectedL2Token]; // <= FOUND

```
['[99](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L99-L99)']
```solidity
99:             l1TokenAddress[expectedL2Token] = _l1Token; // <= FOUND

```
['[128](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L128-L128)']
```solidity
128:         address l1Token = l1TokenAddress[_l2Token]; // <= FOUND

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L206-L206)']
```solidity
206:         return l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE]; // <= FOUND

```
['[213](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L213-L213)']
```solidity
213:         l2BlockHash[_block % MINIBLOCK_HASHES_TO_STORE] = _hash; // <= FOUND

```


</details>

## [Gas-77] State variable written in a loop

### Resolution 
To optimize gas consumption in smart contracts, especially when dealing with loops that write to state variables, a recommended approach is to use a local (memory) variable within the loop for calculations and then update the state variable only once after the loop completes. This method reduces the number of state changes, each of which costs gas, thereby making the operation more gas-efficient.

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[150](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L150-L173)']
```solidity
142:        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) {
143:             
144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
147: 
148:             
149:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");
150:             processedLogs = _setBit(processedLogs, uint8(logKey)); // <= FOUND
151: 
152:             
153:             if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
154:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
155:                 logOutput.l2LogsTreeRoot = logValue;
156:             } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
157:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
158:                 logOutput.pubdataHash = logValue;
159:             } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
160:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
161:                 logOutput.stateDiffHash = logValue;
162:             } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
163:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
164:                 logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
165:             } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
166:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
167:                 logOutput.previousBatchHash = logValue;
168:             } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
169:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
170:                 logOutput.chainedPriorityTxsHash = logValue;
171:             } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
172:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
173:                 logOutput.numberOfLayer1Txs = uint256(logValue); // <= FOUND
174:             } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
175:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
176:                 logOutput.blob1Hash = logValue;
177:             } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
178:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
179:                 logOutput.blob2Hash = logValue;
180:             } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
181:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
182:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
183:             } else {
184:                 revert("ul");
185:             }
186:         }

```
['[210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210-L210)']
```solidity
208:        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) {
209:             address facetAddr = ds.facets[i];
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr]; // <= FOUND
211: 
212:             result[i] = Facet(facetAddr, facetToSelectors.selectors);
213:         }

```
['[105](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L105-L105)']
```solidity
101:        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {
102:             Action action = facetCuts[i].action;
103:             address facet = facetCuts[i].facet;
104:             bool isFacetFreezable = facetCuts[i].isFreezable;
105:             bytes4[] memory selectors = facetCuts[i].selectors; // <= FOUND
106: 
107:             require(selectors.length > 0, "B"); 
108: 
109:             if (action == Action.Add) {
110:                 _addFunctions(facet, selectors, isFacetFreezable);
111:             } else if (action == Action.Replace) {
112:                 _replaceFunctions(facet, selectors, isFacetFreezable);
113:             } else if (action == Action.Remove) {
114:                 _removeFunctions(facet, selectors);
115:             } else {
116:                 revert("C"); 
117:             }
118:         }

```
['[249](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L249-L249)']
```solidity
248:        for (uint256 i = 0; i < deploymentsLength; ++i) {
249:             sumOfValues += _deployments[i].value; // <= FOUND
250:         }

```


</details>

## [Gas-78] State variable read in a loop

### Resolution 
Reading a state variable inside a loop in a smart contract can unnecessarily increase gas consumption, as each read operation from the blockchain state is costly. This inefficiency becomes pronounced in loops with many iterations. To optimize gas usage, it's advisable to read the state variable once before the loop starts, store its value in a local (memory) variable, and then use this local variable within the loop. This approach minimizes the number of state read operations, thereby reducing the gas cost associated with executing the contract function, making the smart contract more efficient and cost-effective to run.

Num of instances: 7

### Findings 


<details><summary>Click to show findings</summary>

['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101-L115)']
```solidity
101:        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) { // <= FOUND
102:             Action action = facetCuts[i].action; // <= FOUND
103:             address facet = facetCuts[i].facet; // <= FOUND
104:             bool isFacetFreezable = facetCuts[i].isFreezable; // <= FOUND
105:             bytes4[] memory selectors = facetCuts[i].selectors; // <= FOUND
106: 
107:             require(selectors.length > 0, "B");  // <= FOUND
108: 
109:             if (action == Action.Add) {
110:                 _addFunctions(facet, selectors, isFacetFreezable); // <= FOUND
111:             } else if (action == Action.Replace) { // <= FOUND
112:                 _replaceFunctions(facet, selectors, isFacetFreezable); // <= FOUND
113:             } else if (action == Action.Remove) { // <= FOUND
114:                 _removeFunctions(facet, selectors); // <= FOUND
115:             } else { // <= FOUND
116:                 revert("C"); 
117:             }
118:         }

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138-L143)']
```solidity
138:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) { // <= FOUND
139:             bytes4 selector = _selectors[i]; // <= FOUND
140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]; // <= FOUND
141:             require(oldFacet.facetAddress == address(0), "J");  // <= FOUND
142: 
143:             _addOneFunction(_facet, selector, _isFacetFreezable); // <= FOUND
144:         }

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158-L166)']
```solidity
158:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) { // <= FOUND
159:             bytes4 selector = _selectors[i]; // <= FOUND
160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]; // <= FOUND
161:             require(oldFacet.facetAddress != address(0), "L");  // <= FOUND
162: 
163:             _removeOneFunction(oldFacet.facetAddress, selector); // <= FOUND
164:             
165:             _saveFacetIfNew(_facet); // <= FOUND
166:             _addOneFunction(_facet, selector, _isFacetFreezable); // <= FOUND
167:         }

```
['[178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178-L183)']
```solidity
178:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) { // <= FOUND
179:             bytes4 selector = _selectors[i]; // <= FOUND
180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector]; // <= FOUND
181:             require(oldFacet.facetAddress != address(0), "a2");  // <= FOUND
182: 
183:             _removeOneFunction(oldFacet.facetAddress, selector); // <= FOUND
184:         }

```
['[311](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311-L313)']
```solidity
311:        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) { // <= FOUND
312:             PriorityOperation memory priorityOp = s.priorityQueue.popFront(); // <= FOUND
313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash)); // <= FOUND
314:         }

```
['[405](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405-L416)']
```solidity
405:        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) { // <= FOUND
406:             currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc(); // <= FOUND
407:             require(
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified], // <= FOUND
409:                 "o1"
410:             );
411: 
412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment; // <= FOUND
413:             proofPublicInput[i] = _getBatchProofPublicInput(
414:                 prevBatchCommitment,
415:                 currentBatchCommitment,
416:                 verifierParams // <= FOUND
417:             );
418: 
419:             prevBatchCommitment = currentBatchCommitment;
420:         }

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127-L153)']
```solidity
127:        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) { // <= FOUND
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE]; // <= FOUND
129:             uint64 enumIndex = stateDiff.readUint64(84); // <= FOUND
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++; // <= FOUND
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52); // <= FOUND
138:             uint256 initValue = stateDiff.readUint256(92); // <= FOUND
139:             uint256 finalValue = stateDiff.readUint256(124); // <= FOUND
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch"); // <= FOUND
141:             stateDiffPtr += 32; // <= FOUND
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr])); // <= FOUND
144:             stateDiffPtr++; // <= FOUND
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression( // <= FOUND
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len] // <= FOUND
152:             );
153:             stateDiffPtr += len; // <= FOUND
154:         }

```


</details>

## [Gas-79] Use uint256(1)/uint256(2) instead of true/false to save gas for changes

### Resolution 
In Solidity, the use of `uint256` values instead of boolean for certain state variables can result in gas savings. This is due to how Ethereum's storage optimization works: changing a variable from `0` to a non-zero value (like flipping `false` to `true`) incurs a higher gas cost compared to modifying an already non-zero value. By using `uint256` with values `1` and `2` instead of `true` and `false`, you avoid the higher cost associated with the `0` to non-zero change, since `1` and `2` are both non-zero. This approach is notably used in OpenZeppelin's `ReentrancyGuard` as a gas optimization technique. However, this should be applied where it makes sense and where gas optimization is critical, as it can decrease code readability.

Num of instances: 13

### Findings 


<details><summary>Click to show findings</summary>

['[418](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L418-L418)']
```solidity
418:         isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true; // <= FOUND

```
['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L87-L87)']
```solidity
87:         stateTransitionManagerIsRegistered[_stateTransitionManager] = true; // <= FOUND

```
['[103](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103-L103)']
```solidity
103:         tokenIsRegistered[_token] = true; // <= FOUND

```
['[68](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L68-L68)']
```solidity
68:         require(validators[_chainId][msg.sender] == true, "ValidatorTimelock: only validator"); // <= FOUND

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L82-L82)']
```solidity
82:         validators[_chainId][_newValidator] = true; // <= FOUND

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L39-L39)']
```solidity
39:         s.validators[_initializeData.validatorTimelock] = true; // <= FOUND

```
['[137](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L137-L137)']
```solidity
137:         diamondStorage.isFrozen = true; // <= FOUND

```
['[78](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L78-L78)']
```solidity
78:             getters.ignoreName = true; // <= FOUND

```
['[84](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L84-L84)']
```solidity
84:             getters.ignoreSymbol = true; // <= FOUND

```
['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L97-L97)']
```solidity
97:             getters.ignoreDecimals = true; // <= FOUND

```
['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97-L97)']
```solidity
97:         stateTransitionManagerIsRegistered[_stateTransitionManager] = false; // <= FOUND

```
['[91](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91-L91)']
```solidity
91:         validators[_chainId][_validator] = false; // <= FOUND

```
['[147](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L147-L147)']
```solidity
147:         diamondStorage.isFrozen = false; // <= FOUND

```


</details>

## [Gas-80] Avoid emitting events in loops

### Resolution 
Emitting events inside loops can significantly increase gas costs in Ethereum smart contracts, as each event emission consumes gas. This practice can quickly escalate transaction fees, especially with a high number of iterations. To optimize for efficiency and cost, it's advisable to minimize event emissions within loops, possibly aggregating data to emit a single event post-loop or reconsidering the design to reduce looped emissions. This approach helps maintain manageable transaction costs and enhances contract performance.

Num of instances: 3

### Findings 


<details><summary>Click to show findings</summary>

['[261](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L261-L261)']
```solidity
257:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259: 
260:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:             emit BlockCommit( // <= FOUND
262:                 _lastCommittedBatchData.batchNumber,
263:                 _lastCommittedBatchData.batchHash,
264:                 _lastCommittedBatchData.commitment
265:             );
266:         }

```
['[299](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L299-L299)']
```solidity
289:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit( // <= FOUND
300:                 _lastCommittedBatchData.batchNumber,
301:                 _lastCommittedBatchData.batchHash,
302:                 _lastCommittedBatchData.commitment
303:             );
304:         }

```
['[353](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L353-L353)']
```solidity
351:        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) {
352:             _executeOneBatch(_batchesData[i], i);
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment); // <= FOUND
354:         }

```


</details>

## [Gas-81] Call msg.XYZ directly rather than caching the value to save gas

Num of instances: 5

### Findings 


<details><summary>Click to show findings</summary>

['[329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L329-L329)']
```solidity
328:             
329:             _recipient = msg.sender == tx.origin ? msg.sender : AddressAliasHelper.applyL1ToL2Alias(msg.sender); // <= FOUND

```
['[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54-L54)']
```solidity
54:         l2Bridge = msg.sender; // <= FOUND

```
['[199](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L199-L199)']
```solidity
199:             amount = msg.value; // <= FOUND

```
['[329](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L329-L329)']
```solidity
329:         uint256 value = msg.value; // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L100-L100)']
```solidity
100:         amount = msg.value; // <= FOUND

```


</details>

## [Gas-82] Consider pre-calculating the address of address(this) to save gas

### Resolution 
Consider saving the address(this) value within a constant using foundry's script.sol or solady's LibRlp.sol to save gas

Num of instances: 21

### Findings 


<details><summary>Click to show findings</summary>

['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65-L65)']
```solidity
65:         uint256 amount = IERC20(_token).balanceOf(address(this)); // <= FOUND

```
['[118](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L118-L118)']
```solidity
118:             uint256 balanceBefore = address(this).balance; // <= FOUND

```
['[120](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L120-L120)']
```solidity
120:             uint256 balanceAfter = address(this).balance; // <= FOUND

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L127-L127)']
```solidity
127:             uint256 balanceBefore = IERC20(_token).balanceOf(address(this)); // <= FOUND

```
['[131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L131-L131)']
```solidity
131:             uint256 balanceAfter = IERC20(_token).balanceOf(address(this)); // <= FOUND

```
['[174](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L174-L174)']
```solidity
174:         uint256 balanceBefore = _token.balanceOf(address(this)); // <= FOUND

```
['[175](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L175-L175)']
```solidity
175:         _token.safeTransferFrom(_from, address(this), _amount); // <= FOUND

```
['[176](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L176-L176)']
```solidity
176:         uint256 balanceAfter = _token.balanceOf(address(this)); // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59-L59)']
```solidity
59:         require(msg.sender == address(this), "Only governance contract itself is allowed to call this function"); // <= FOUND

```
['[266](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L266-L266)']
```solidity
261:         
262:         initData = bytes.concat(
263:             IDiamondInit.initialize.selector,
264:             bytes32(_chainId),
265:             bytes32(uint256(uint160(bridgehub))),
266:             bytes32(uint256(uint160(address(this)))), // <= FOUND
267:             bytes32(uint256(protocolVersion)),
268:             bytes32(uint256(uint160(_admin))),
269:             bytes32(uint256(uint160(validatorTimelock))),
270:             bytes32(uint256(uint160(_baseToken))),
271:             bytes32(uint256(uint160(_sharedBridge))),
272:             bytes32(storedBatchZero),
273:             diamondCut.initCalldata
274:         );

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41-L41)']
```solidity
41:         uint256 amount = address(this).balance; // <= FOUND

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L29-L29)']
```solidity
29:         require(msg.sender == address(this), "Callable only by self"); // <= FOUND

```
['[333](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L333-L333)']
```solidity
333:                 BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value); // <= FOUND

```
['[47](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L47-L47)']
```solidity
47:         if (codeAddress != address(this)) { // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L100-L100)']
```solidity
100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value"); // <= FOUND

```
['[188](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L188-L188)']
```solidity
188:         return recoveredAddress == address(this) && recoveredAddress != address(0); // <= FOUND

```
['[130](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L130-L130)']
```solidity
125:         
126:         L2ToL1Log memory l2ToL1Log = L2ToL1Log({
127:             l2ShardId: 0,
128:             isService: true,
129:             txNumberInBlock: SYSTEM_CONTEXT_CONTRACT.txNumberInBlock(),
130:             sender: address(this), // <= FOUND
131:             key: bytes32(uint256(uint160(msg.sender))),
132:             value: hash
133:         });

```
['[108](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L108-L108)']
```solidity
106:             
107:             
108:             balance[address(this)] -= amount; // <= FOUND

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L61-L61)']
```solidity
60:         
61:         require(to != address(this), "MsgValueSimulator calls itself"); // <= FOUND

```
['[377](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L377-L377)']
```solidity
377:             uint256 currentAllowance = IERC20(token).allowance(address(this), paymaster); // <= FOUND

```
['[153](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L153-L153)']
```solidity
152:         return
153:             L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash); // <= FOUND

```


</details>

## [Gas-83] Use of memory instead of storage for struct/array state variables

### Resolution 
In Solidity, choosing between `memory` and `storage` for variables, especially when dealing with structs or arrays, is crucial for optimizing gas costs. Variables declared as `storage` are pointers to the blockchain data, leading to lower gas consumption when fields are accessed or modified, as they don't require reading the entire structure. In contrast, `memory` variables copy the entire struct or array from `storage`, incurring significant gas costs, especially for large or complex structures. Therefore, use `storage` for state variables or when working within functions to manipulate existing contract data. Reserve `memory` for temporary data or when data needs to be passed to external functions as copies, ensuring efficient use of gas and avoiding unnecessary costs.

Num of instances: 6

### Findings 


<details><summary>Click to show findings</summary>

['[173](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L173-L173)']
```solidity
173:         BlockInfo memory batchInfo = currentBatchInfo; // <= FOUND

```
['[181](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L181-L181)']
```solidity
181:         BlockInfo memory blockInfo = currentL2BlockInfo; // <= FOUND

```
['[275](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L275-L275)']
```solidity
275:         BlockInfo memory virtualBlockInfo = currentVirtualL2BlockInfo; // <= FOUND

```
['[135](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L135-L135)']
```solidity
135:         VirtualBlockUpgradeInfo memory currentVirtualBlockUpgradeInfo = virtualBlockUpgradeInfo; // <= FOUND

```
['[41](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L41-L41)']
```solidity
41:         AccountInfo memory info = accountInfo[_address]; // <= FOUND

```
['[75](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L75-L75)']
```solidity
75:         AccountInfo memory currentInfo = accountInfo[msg.sender]; // <= FOUND

```


</details>

## [Gas-84] Mappings are cheaper than arrays for state variable iteration

### Resolution 
Where possible use mappings in place of arrays as they are far cheaper during iterations and are easier to use. There are instances such as struct arrays where arrays make more sense.

Num of instances: 1

### Findings 


<details><summary>Click to show findings</summary>

['[70](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L70-L70)']
```solidity
70: bytes32[MINIBLOCK_HASHES_TO_STORE] internal l2BlockHash; // <= FOUND

```


</details>

## [Gas-85] Public functions not called internally

### Resolution 
Public functions that aren't used internally in Solidity contracts should be made external to optimize gas usage and improve contract efficiency. External functions can only be called from outside the contract, and their arguments are directly read from the calldata, which is more gas-efficient than loading them into memory, as is the case for public functions. By using external visibility, developers can reduce gas consumption for external calls and ensure that the contract operates more cost-effectively for users. Moreover, setting the appropriate visibility level for functions also enhances code readability and maintainability, promoting a more secure and well-structured contract design.

Num of instances: 8

### Findings 


<details><summary>Click to show findings</summary>

['[40](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L40-L40)']
```solidity
40:     function extendedAccountVersion(address _address) public view returns (AccountAbstractionVersion) 

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L65-L65)']
```solidity
65:     function increaseMinNonce(uint256 _value) public onlySystemCall returns (uint256 oldMinNonce) 

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L82-L82)']
```solidity
82:     function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall 

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L102-L102)']
```solidity
102:     function getValueUnderNonce(uint256 _key) public view returns (uint256) 

```
['[190](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L190-L190)']
```solidity
190:     function getBlockNumber() public view returns (uint128) 

```
['[198](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L198-L198)']
```solidity
198:     function getBlockTimestamp() public view returns (uint128) 

```
['[140](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L140-L140)']
```solidity
140:     function decimals() external pure override returns (uint8) 

```
['[171](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L171-L171)']
```solidity
171:     function decimals() public view override returns (uint8) 

```


</details>

## [Gas-86] do-while is cheaper than for-loops when the initial check can be skipped

### Resolution 
In smart contract optimization, do-while loops can outperform for-loops cost-wise when the initial iteration's condition check is unnecessary. By deferring the condition check to the loop's end, do-while ensures the loop body executes at least once, saving gas when initial conditions are already met, a crucial aspect for Web3 auditors focusing on efficiency. These however should be used carefully as if an input array has a length of 0, the while loop shouldn't run, as such this should only ne utilized if it is known for a fact the contents of the iteration will be run at least once.

Num of instances: 21

### Findings 


<details><summary>Click to show findings</summary>

['[225](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L225)']
```solidity
225:        for (uint256 i = 0; i < _calls.length; ++i) { // <= FOUND
226:             (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
227:             if (!success) {
228:                 
229:                 assembly {
230:                     revert(add(returnData, 0x20), mload(returnData))
231:                 }
232:             }
233:         }

```
['[142](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L142-L142)']
```solidity
142:        for (uint256 i = 0; i < emittedL2Logs.length; i = i.uncheckedAdd(L2_TO_L1_LOG_SERIALIZE_SIZE)) { // <= FOUND
143:             
144:             (address logSender, ) = UnsafeBytes.readAddress(emittedL2Logs, i + L2_LOG_ADDRESS_OFFSET);
145:             (uint256 logKey, ) = UnsafeBytes.readUint256(emittedL2Logs, i + L2_LOG_KEY_OFFSET);
146:             (bytes32 logValue, ) = UnsafeBytes.readBytes32(emittedL2Logs, i + L2_LOG_VALUE_OFFSET);
147: 
148:             
149:             require(!_checkBit(processedLogs, uint8(logKey)), "kp");
150:             processedLogs = _setBit(processedLogs, uint8(logKey));
151: 
152:             
153:             if (logKey == uint256(SystemLogKey.L2_TO_L1_LOGS_TREE_ROOT_KEY)) {
154:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lm");
155:                 logOutput.l2LogsTreeRoot = logValue;
156:             } else if (logKey == uint256(SystemLogKey.TOTAL_L2_TO_L1_PUBDATA_KEY)) {
157:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "ln");
158:                 logOutput.pubdataHash = logValue;
159:             } else if (logKey == uint256(SystemLogKey.STATE_DIFF_HASH_KEY)) {
160:                 require(logSender == L2_TO_L1_MESSENGER_SYSTEM_CONTRACT_ADDR, "lb");
161:                 logOutput.stateDiffHash = logValue;
162:             } else if (logKey == uint256(SystemLogKey.PACKED_BATCH_AND_L2_BLOCK_TIMESTAMP_KEY)) {
163:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sc");
164:                 logOutput.packedBatchAndL2BlockTimestamp = uint256(logValue);
165:             } else if (logKey == uint256(SystemLogKey.PREV_BATCH_HASH_KEY)) {
166:                 require(logSender == L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR, "sv");
167:                 logOutput.previousBatchHash = logValue;
168:             } else if (logKey == uint256(SystemLogKey.CHAINED_PRIORITY_TXN_HASH_KEY)) {
169:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bl");
170:                 logOutput.chainedPriorityTxsHash = logValue;
171:             } else if (logKey == uint256(SystemLogKey.NUMBER_OF_LAYER_1_TXS_KEY)) {
172:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bk");
173:                 logOutput.numberOfLayer1Txs = uint256(logValue);
174:             } else if (logKey == uint256(SystemLogKey.BLOB_ONE_HASH_KEY)) {
175:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pc");
176:                 logOutput.blob1Hash = logValue;
177:             } else if (logKey == uint256(SystemLogKey.BLOB_TWO_HASH_KEY)) {
178:                 require(logSender == L2_PUBDATA_CHUNK_PUBLISHER_ADDR, "pd");
179:                 logOutput.blob2Hash = logValue;
180:             } else if (logKey == uint256(SystemLogKey.EXPECTED_SYSTEM_CONTRACT_UPGRADE_TX_HASH_KEY)) {
181:                 require(logSender == L2_BOOTLOADER_ADDRESS, "bu");
182:                 require(_expectedSystemContractUpgradeTxHash == logValue, "ut");
183:             } else {
184:                 revert("ul");
185:             }
186:         }

```
['[257](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L257-L257)']
```solidity
257:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) { // <= FOUND
258:             _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));
259: 
260:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
261:             emit BlockCommit(
262:                 _lastCommittedBatchData.batchNumber,
263:                 _lastCommittedBatchData.batchHash,
264:                 _lastCommittedBatchData.commitment
265:             );
266:         }

```
['[289](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289-L289)']
```solidity
289:        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) { // <= FOUND
290:             
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
297: 
298:             s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
299:             emit BlockCommit(
300:                 _lastCommittedBatchData.batchNumber,
301:                 _lastCommittedBatchData.batchHash,
302:                 _lastCommittedBatchData.commitment
303:             );
304:         }

```
['[311](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L311-L311)']
```solidity
311:        for (uint256 i = 0; i < _nPriorityOps; i = i.uncheckedInc()) { // <= FOUND
312:             PriorityOperation memory priorityOp = s.priorityQueue.popFront();
313:             concatHash = keccak256(abi.encode(concatHash, priorityOp.canonicalTxHash));
314:         }

```
['[351](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L351-L351)']
```solidity
351:        for (uint256 i = 0; i < nBatches; i = i.uncheckedInc()) { // <= FOUND
352:             _executeOneBatch(_batchesData[i], i);
353:             emit BlockExecution(_batchesData[i].batchNumber, _batchesData[i].batchHash, _batchesData[i].commitment);
354:         }

```
['[405](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L405-L405)']
```solidity
405:        for (uint256 i = 0; i < committedBatchesLength; i = i.uncheckedInc()) { // <= FOUND
406:             currentTotalBatchesVerified = currentTotalBatchesVerified.uncheckedInc();
407:             require(
408:                 _hashStoredBatchInfo(_committedBatches[i]) == s.storedBatchHashes[currentTotalBatchesVerified],
409:                 "o1"
410:             );
411: 
412:             bytes32 currentBatchCommitment = _committedBatches[i].commitment;
413:             proofPublicInput[i] = _getBatchProofPublicInput(
414:                 prevBatchCommitment,
415:                 currentBatchCommitment,
416:                 verifierParams
417:             );
418: 
419:             prevBatchCommitment = currentBatchCommitment;
420:         }

```
['[580](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L580-L580)']
```solidity
580:        for (uint i = 0; i < MAX_NUMBER_OF_BLOBS; i++) { // <= FOUND
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
583:         }

```
['[636](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L636-L636)']
```solidity
636:        for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) { // <= FOUND
637:             bytes32 blobVersionedHash = _getBlobVersionedHash(versionedHashIndex);
638: 
639:             require(blobVersionedHash != bytes32(0), "vh");
640: 
641:             
642:             
643:             bytes32 openingPoint = bytes32(
644:                 uint256(uint128(bytes16(_pubdataCommitments[i:i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET])))
645:             );
646: 
647:             _pointEvaluationPrecompile(
648:                 blobVersionedHash,
649:                 openingPoint,
650:                 _pubdataCommitments[i + PUBDATA_COMMITMENT_CLAIMED_VALUE_OFFSET:i + PUBDATA_COMMITMENT_SIZE]
651:             );
652: 
653:             
654:             blobCommitments[versionedHashIndex] = keccak256(
655:                 abi.encodePacked(blobVersionedHash, _pubdataCommitments[i:i + PUBDATA_COMMITMENT_COMMITMENT_OFFSET])
656:             );
657:             versionedHashIndex += 1;
658:         }

```
['[208](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L208-L208)']
```solidity
208:        for (uint256 i = 0; i < facetsLen; i = i.uncheckedInc()) { // <= FOUND
209:             address facetAddr = ds.facets[i];
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr];
211: 
212:             result[i] = Facet(facetAddr, facetToSelectors.selectors);
213:         }

```
['[356](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356-L356)']
```solidity
356:        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) { // <= FOUND
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
358: 
359:             
360:             assembly {
361:                 mstore(add(hashedFactoryDeps, mul(add(i, 1), 32)), hashedBytecode)
362:             }
363:         }

```
['[226](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L226-L226)']
```solidity
226:        for (uint256 i = 0; i < _factoryDeps.length; ++i) { // <= FOUND
227:             require(
228:                 L2ContractHelper.hashL2Bytecode(_factoryDeps[i]) == bytes32(_expectedHashes[i]),
229:                 "Wrong factory dep hash"
230:             );
231:         }

```
['[101](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L101-L101)']
```solidity
101:        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) { // <= FOUND
102:             Action action = facetCuts[i].action;
103:             address facet = facetCuts[i].facet;
104:             bool isFacetFreezable = facetCuts[i].isFreezable;
105:             bytes4[] memory selectors = facetCuts[i].selectors;
106: 
107:             require(selectors.length > 0, "B"); 
108: 
109:             if (action == Action.Add) {
110:                 _addFunctions(facet, selectors, isFacetFreezable);
111:             } else if (action == Action.Replace) {
112:                 _replaceFunctions(facet, selectors, isFacetFreezable);
113:             } else if (action == Action.Remove) {
114:                 _removeFunctions(facet, selectors);
115:             } else {
116:                 revert("C"); 
117:             }
118:         }

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L138-L138)']
```solidity
138:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) { // <= FOUND
139:             bytes4 selector = _selectors[i];
140:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
141:             require(oldFacet.facetAddress == address(0), "J"); 
142: 
143:             _addOneFunction(_facet, selector, _isFacetFreezable);
144:         }

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L158-L158)']
```solidity
158:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) { // <= FOUND
159:             bytes4 selector = _selectors[i];
160:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
161:             require(oldFacet.facetAddress != address(0), "L"); 
162: 
163:             _removeOneFunction(oldFacet.facetAddress, selector);
164:             
165:             _saveFacetIfNew(_facet);
166:             _addOneFunction(_facet, selector, _isFacetFreezable);
167:         }

```
['[178](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L178-L178)']
```solidity
178:        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) { // <= FOUND
179:             bytes4 selector = _selectors[i];
180:             SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
181:             require(oldFacet.facetAddress != address(0), "a2"); 
182: 
183:             _removeOneFunction(oldFacet.facetAddress, selector);
184:         }

```
['[29](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L29-L29)']
```solidity
29:        for (uint256 i; i < pathLength; i = i.uncheckedInc()) { // <= FOUND
30:             currentHash = (_index % 2 == 0)
31:                 ? _efficientHash(currentHash, _path[i])
32:                 : _efficientHash(_path[i], currentHash);
33:             _index /= 2;
34:         }

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L127-L127)']
```solidity
127:        for (uint256 i = 0; i < _numberOfStateDiffs * STATE_DIFF_ENTRY_SIZE; i += STATE_DIFF_ENTRY_SIZE) { // <= FOUND
128:             bytes calldata stateDiff = _stateDiffs[i:i + STATE_DIFF_ENTRY_SIZE];
129:             uint64 enumIndex = stateDiff.readUint64(84);
130:             if (enumIndex != 0) {
131:                 
132:                 continue;
133:             }
134: 
135:             numInitialWritesProcessed++;
136: 
137:             bytes32 derivedKey = stateDiff.readBytes32(52);
138:             uint256 initValue = stateDiff.readUint256(92);
139:             uint256 finalValue = stateDiff.readUint256(124);
140:             require(derivedKey == _compressedStateDiffs.readBytes32(stateDiffPtr), "iw: initial key mismatch");
141:             stateDiffPtr += 32;
142: 
143:             uint8 metadata = uint8(bytes1(_compressedStateDiffs[stateDiffPtr]));
144:             stateDiffPtr++;
145:             uint8 operation = metadata & OPERATION_BITMASK;
146:             uint8 len = operation == 0 ? 32 : metadata >> LENGTH_BITS_OFFSET;
147:             _verifyValueCompression(
148:                 initValue,
149:                 finalValue,
150:                 operation,
151:                 _compressedStateDiffs[stateDiffPtr:stateDiffPtr + len]
152:             );
153:             stateDiffPtr += len;
154:         }

```
['[248](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L248-L248)']
```solidity
248:        for (uint256 i = 0; i < deploymentsLength; ++i) { // <= FOUND
249:             sumOfValues += _deployments[i].value;
250:         }

```
['[206](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L206-L206)']
```solidity
206:        for (uint256 i = 0; i < numberOfL2ToL1Logs; ++i) { // <= FOUND
207:             bytes32 hashedLog = EfficientCall.keccak(
208:                 _totalL2ToL1PubdataAndStateDiffs[calldataPtr:calldataPtr + L2_TO_L1_LOG_SERIALIZE_SIZE]
209:             );
210:             calldataPtr += L2_TO_L1_LOG_SERIALIZE_SIZE;
211:             l2ToL1LogsTreeArray[i] = hashedLog;
212:             reconstructedChainedLogsHash = keccak256(abi.encode(reconstructedChainedLogsHash, hashedLog));
213:         }

```
['[224](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L224-L224)']
```solidity
224:            for (uint256 i = 0; i < nodesOnCurrentLevel; ++i) { // <= FOUND
225:                 l2ToL1LogsTreeArray[i] = keccak256(
226:                     abi.encode(l2ToL1LogsTreeArray[2 * i], l2ToL1LogsTreeArray[2 * i + 1])
227:                 );
228:             }

```


</details>

## [Gas-87] Empty blocks should be removed or emit something

### Resolution 
Empty code blocks (i.e., {}) in a Solidity contract can be harmful as they can lead to ambiguity, misinterpretation, and unintended behavior. When developers encounter empty code blocks, it may be unclear whether the absence of code is intentional or the result of an oversight. This uncertainty can cause confusion during development, testing, and debugging, increasing the likelihood of introducing errors or vulnerabilities. Moreover, empty code blocks may give a false impression of implemented functionality or security measures, creating a misleading sense of assurance. To ensure clarity and maintainability, it is essential to avoid empty code blocks and explicitly document the intended behavior or any intentional omissions.

Num of instances: 4

### Findings 


<details><summary>Click to show findings</summary>

['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L60-L60)']
```solidity
60:     function initialize() external reentrancyGuardInitializer {}

```
['[263](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L263-L263)']
```solidity
263:     function _upgradeL1Contract(bytes calldata _customCallDataForUpgrade) internal virtual {}

```
['[269](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L269-L269)']
```solidity
269:     function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}

```
['[125](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L125-L125)']
```solidity
125:     function executeTransactionFromOutside(Transaction calldata _transaction) external payable override {
126:         
127:     }

```


</details>

## [Gas-88] Use assembly to write address/contract storage values

Num of instances: 73

### Findings 


<details><summary>Click to show findings</summary>

['[56](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L56-L56)']
```solidity
56:         sharedBridge = _sharedBridge; // <= FOUND

```
['[96](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L96-L96)']
```solidity
96:         l1WethAddress = _l1WethAddress; // <= FOUND

```
['[59](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L59-L59)']
```solidity
59:         bridgehub = _bridgehub; // <= FOUND

```
['[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L98-L98)']
```solidity
98:         legacyBridge = _legacyBridge; // <= FOUND

```
['[111](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L111-L111)']
```solidity
111:         eraFirstPostUpgradeBatch = _eraFirstPostUpgradeBatch; // <= FOUND

```
['[430](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L430-L430)']
```solidity
430:         MessageParams memory messageParams = MessageParams({ // <= FOUND

```
['[477](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L477-L477)']
```solidity
477:         bool success = bridgehub.proveL2MessageInclusion( // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L55-L55)']
```solidity
55:         pendingAdmin = _newPendingAdmin; // <= FOUND

```
['[65](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L65-L65)']
```solidity
65:         admin = currentPendingAdmin; // <= FOUND

```
['[109](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109-L109)']
```solidity
109:         sharedBridge = IL1SharedBridge(_sharedBridge); // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L46-L46)']
```solidity
46:         securityCouncil = _securityCouncil; // <= FOUND

```
['[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L49-L49)']
```solidity
49:         minDelay = _minDelay; // <= FOUND

```
['[251](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251-L251)']
```solidity
251:         minDelay = _newDelay; // <= FOUND

```
['[258](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258-L258)']
```solidity
258:         securityCouncil = _newSecurityCouncil; // <= FOUND

```
['[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L85-L85)']
```solidity
85:         genesisUpgrade = _initializeData.genesisUpgrade; // <= FOUND

```
['[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L86-L86)']
```solidity
86:         protocolVersion = _initializeData.protocolVersion; // <= FOUND

```
['[87](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L87-L87)']
```solidity
87:         validatorTimelock = _initializeData.validatorTimelock; // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100-L100)']
```solidity
100:         storedBatchZero = keccak256(abi.encode(batchZero)); // <= FOUND

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102-L102)']
```solidity
102:         initialCutHash = keccak256(abi.encode(_initializeData.diamondCut)); // <= FOUND

```
['[133](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L133-L133)']
```solidity
133:         validatorTimelock = _validatorTimelock; // <= FOUND

```
['[138](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138-L138)']
```solidity
138:         initialCutHash = keccak256(abi.encode(_diamondCut)); // <= FOUND

```
['[148](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L148-L148)']
```solidity
148:         protocolVersion = _newProtocolVersion; // <= FOUND

```
['[57](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L57-L57)']
```solidity
57:         executionDelay = _executionDelay; // <= FOUND

```
['[74](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L74-L74)']
```solidity
74:         stateTransitionManager = _stateTransitionManager; // <= FOUND

```
['[30](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L30-L30)']
```solidity
30:         s.chainId = _initializeData.chainId; // <= FOUND

```
['[31](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L31-L31)']
```solidity
31:         s.bridgehub = _initializeData.bridgehub; // <= FOUND

```
['[32](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L32-L32)']
```solidity
32:         s.stateTransitionManager = _initializeData.stateTransitionManager; // <= FOUND

```
['[35](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L35-L35)']
```solidity
35:         s.protocolVersion = _initializeData.protocolVersion; // <= FOUND

```
['[38](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L38-L38)']
```solidity
38:         s.admin = _initializeData.admin; // <= FOUND

```
['[42](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L42-L42)']
```solidity
42:         s.verifierParams = _initializeData.verifierParams; // <= FOUND

```
['[46](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L46-L46)']
```solidity
46:         s.feeParams = _initializeData.feeParams; // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L27-L27)']
```solidity
27:         s.pendingAdmin = _newPendingAdmin; // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L37-L37)']
```solidity
37:         s.admin = pendingAdmin; // <= FOUND

```
['[72](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L72-L72)']
```solidity
72:         FeeParams memory oldFeeParams = s.feeParams; // <= FOUND

```
['[73](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L73-L73)']
```solidity
73:         s.feeParams = _newFeeParams; // <= FOUND

```
['[58](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L58-L58)']
```solidity
58:             blobCommitments = _verifyBlobInformation(_newBatch.pubdataCommitments[1:], blobHashes); // <= FOUND

```
['[396](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L396-L396)']
```solidity
396:         VerifierParams memory verifierParams = s.verifierParams; // <= FOUND

```
['[158](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L158-L158)']
```solidity
158:         Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage(); // <= FOUND

```
['[210](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L210-L210)']
```solidity
210:             Diamond.FacetToSelectors memory facetToSelectors = ds.facetToSelectors[facetAddr]; // <= FOUND

```
['[157](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L157-L157)']
```solidity
157:         FeeParams memory feeParams = s.feeParams; // <= FOUND

```
['[155](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155-L155)']
```solidity
155:         VerifierParams memory oldVerifierParams = s.verifierParams; // <= FOUND

```
['[156](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L156-L156)']
```solidity
156:         s.verifierParams = _newVerifierParams; // <= FOUND

```
['[39](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L39-L39)']
```solidity
39:         s.protocolVersion = _newProtocolVersion; // <= FOUND

```
['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L97-L97)']
```solidity
97:         FacetCut[] memory facetCuts = _diamondCut.facetCuts; // <= FOUND

```
['[127](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L127-L127)']
```solidity
127:         DiamondStorage storage ds = getDiamondStorage(); // <= FOUND

```
['[149](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L149-L149)']
```solidity
149:         bool success = EfficientCall.rawCall(gas, to, value, data, isSystemCall); // <= FOUND

```
['[201](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L201-L201)']
```solidity
201:         bool success = _transaction.payToTheBootloader(); // <= FOUND

```
['[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L106-L106)']
```solidity
106:         chainedLogsHash = keccak256(abi.encode(chainedLogsHash, hashedLog)); // <= FOUND

```
['[122](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L122-L122)']
```solidity
122:         chainedMessagesHash = keccak256(abi.encode(chainedMessagesHash, hash)); // <= FOUND

```
['[164](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L164-L164)']
```solidity
164:         chainedL1BytecodesRevealDataHash = keccak256(abi.encode(chainedL1BytecodesRevealDataHash, _bytecodeHash)); // <= FOUND

```
['[330](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L330-L330)']
```solidity
330:         numberOfLogsToProcess = 0; // <= FOUND

```
['[85](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L85-L85)']
```solidity
85:         chainId = _newChainId; // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L100-L100)']
```solidity
100:         origin = _newOrigin; // <= FOUND

```
['[106](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L106-L106)']
```solidity
106:         gasPrice = _gasPrice; // <= FOUND

```
['[113](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L113-L113)']
```solidity
113:         basePubdataSpent = _basePubdataSpent; // <= FOUND

```
['[114](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L114-L114)']
```solidity
114:         gasPerPubdataByte = _gasPerPubdataByte; // <= FOUND

```
['[271](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L271-L271)']
```solidity
271:             currentVirtualL2BlockInfo = currentL2BlockInfo; // <= FOUND

```
['[307](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L307-L307)']
```solidity
307:         currentVirtualL2BlockInfo = virtualBlockInfo; // <= FOUND

```
['[316](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L316-L316)']
```solidity
316:         currentL2BlockInfo = BlockInfo({number: _l2BlockNumber, timestamp: _l2BlockTimestamp}); // <= FOUND

```
['[403](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L403-L403)']
```solidity
403:         currentL2BlockTxsRollingHash = keccak256(abi.encode(currentL2BlockTxsRollingHash, _txHash)); // <= FOUND

```
['[461](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L461-L461)']
```solidity
461:         currentBatchInfo = newBlockInfo; // <= FOUND

```
['[463](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L463-L463)']
```solidity
463:         baseFee = _baseFee; // <= FOUND

```
['[487](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L487-L487)']
```solidity
487:         txNumberInBlock = 0; // <= FOUND

```
['[131](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L131-L131)']
```solidity
131:         rawParams = _inputMemoryOffset; // <= FOUND

```
['[345](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L345-L345)']
```solidity
345:         bool precompileCallSuccess = unsafePrecompileCall( // <= FOUND

```
['[82](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/SystemContractsCaller.sol#L82-L82)']
```solidity
82:         success = systemCall(gasLimit, to, value, data); // <= FOUND

```
['[60](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60-L60)']
```solidity
60:         l1Bridge = _l1Bridge; // <= FOUND

```
['[61](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L61-L61)']
```solidity
61:         l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash; // <= FOUND

```
['[52](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L52-L52)']
```solidity
52:         l1Address = _l1Address; // <= FOUND

```
['[54](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L54-L54)']
```solidity
54:         l2Bridge = msg.sender; // <= FOUND

```
['[97](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L97-L97)']
```solidity
97:             getters.ignoreDecimals = true; // <= FOUND

```
['[100](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L100-L100)']
```solidity
100:         availableGetters = getters; // <= FOUND

```
['[124](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L124-L124)']
```solidity
124:         availableGetters = _availableGetters; // <= FOUND

```


</details>

## [Gas-89] Use constants instead of type(uint<n>).max

### Resolution 
In smart contract development, utilizing constants for known maximum or minimum values, rather than computing `type(uint<n>).max` or assuming `0` for `.min`, can significantly reduce gas costs. Constants require less runtime computation and storage, optimizing contract efficiency—a crucial strategy for developers aiming for cost-effective and performant code.

Num of instances: 18

### Findings 


<details><summary>Click to show findings</summary>

['[123](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L123-L123)']
```solidity
123:         require(_chainId <= type(uint48).max, "Bridgehub: chainId too large"); // <= FOUND

```
['[48](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L48-L48)']
```solidity
48:         require(_transaction.from <= type(uint16).max, "ua"); // <= FOUND

```
['[49](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L49-L49)']
```solidity
49:         require(_transaction.to <= type(uint160).max, "ub"); // <= FOUND

```
['[55](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L55-L55)']
```solidity
55:         require(_transaction.reserved[1] <= type(uint160).max, "uf"); // <= FOUND

```
['[115](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L115-L115)']
```solidity
115: address constant BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS = address(uint160(type(uint16).max)); // <= FOUND

```
['[37](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L37-L37)']
```solidity
37:     uint256 public blockGasLimit = type(uint32).max; // <= FOUND

```
['[86](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L86-L86)']
```solidity
86:             if (_number > type(uint128).max) { // <= FOUND

```
['[90](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L90-L90)']
```solidity
90:             if (_number > type(uint64).max) { // <= FOUND

```
['[94](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L94-L94)']
```solidity
94:             if (_number > type(uint32).max) { // <= FOUND

```
['[98](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L98-L98)']
```solidity
98:             if (_number > type(uint16).max) { // <= FOUND

```
['[102](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/RLPEncoder.sol#L102-L102)']
```solidity
102:             if (_number > type(uint8).max) { // <= FOUND

```
['[9](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L9-L9)']
```solidity
9: uint256 constant UINT32_MASK = type(uint32).max; // <= FOUND

```
['[10](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L10-L10)']
```solidity
10: uint256 constant UINT64_MASK = type(uint64).max; // <= FOUND

```
['[11](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L11-L11)']
```solidity
11: uint256 constant UINT128_MASK = type(uint128).max; // <= FOUND

```
['[12](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L12-L12)']
```solidity
12: uint256 constant ADDRESS_MASK = type(uint160).max; // <= FOUND

```
['[27](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L27-L27)']
```solidity
27:         require(_x <= type(uint32).max, "Overflow"); // <= FOUND

```
['[21](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L21-L21)']
```solidity
21:         require(_x <= type(uint128).max, "Overflow"); // <= FOUND

```
['[33](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L33-L33)']
```solidity
33:         require(_x <= type(uint24).max, "Overflow"); // <= FOUND

```


</details>
