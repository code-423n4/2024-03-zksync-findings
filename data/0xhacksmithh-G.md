### [Gas-] via `re-organizing elements` in struct extra storage slot ca saved [Gas saved upto 3 storage slot = 3 * 2000 = 6000]

1. here bool `zkPorterIsAvailable` consume a whole slot, so moving it to near smaller storage like `address` 1 whole storage slot can saved

2. By reducing size of `uint256 protocolVersion` and `uint256 chainId` to `uint128` and packing them into single slot, result in saving 1 extra storage slot

3. If you reduce above 2 further like to `uint64` and packing them with a `address` type so 2 whole storage slot saved
```diff
struct ZkSyncStateTransitionStorage {
....
....
    /// @dev Used as an input to zkp-circuit.
-   bool zkPorterIsAvailable;   // @audit G:: re-arrange to save gas
    /// @dev The maximum number of the L2 gas that a user can request for L1 -> L2 transactions
    /// @dev This is the maximum number of L2 gas that is available for the "body" of the transaction, i.e.
    /// without overhead for proving the batch.
...
...
-   uint256 protocolVersion;   // @audit G:: decrease size
    /// @dev Hash of the system contract upgrade transaction. If 0, then no upgrade transaction needs to be done.
    bytes32 l2SystemContractsUpgradeTxHash;
    /// @dev Batch number where the upgrade transaction has happened. If 0, then no upgrade transaction has happened
    /// yet.
    uint256 l2SystemContractsUpgradeBatchNumber;
    /// @dev Address which will exercise non-critical changes to the Diamond 
...
...
-   uint256 chainId;   // @audit G:: could decrease in size
    /// @dev The address of the bridgehub
    address bridgehub;
...
...
}
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L103

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L123

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L140

### [Gas-N1] Optimize Modifiers
The code of modifiers is placed in a modified function, and modifier code is copied in all instances where it’s used. This will increase bytecode size and gas usage.

Below is one way to optimize modifier gas cost.

Before:
```diff
modifier onlyOwner(){
   require(owner() == mag.sender, "Ownable: Caller is not the owner");
   _;
}
```
After:
```diff
modifier onlyOwner() {
   _checkOwner();
   _;
}

function _checkOwner() internal view virtual{
   require(owner() == msg.sender, "Ownable: Caller is not the owner");
}
```
In this example, a refractor is done to the internal function _checkOwner(), allowing the internal function to be reused in modifiers. This method saves bytecode size and gas cost

```diff
 modifier onlySecurityCouncil() {
        require(msg.sender == securityCouncil, "Only security council is allowed to call this function");
        _;
    }

    /// @notice Checks that the message sender is an active owner or an active security council.
    modifier onlyOwnerOrSecurityCouncil() {
        require(
            msg.sender == owner() || msg.sender == securityCouncil,   // @audit G :: 
            "Only the owner and security council are allowed to call this function"
        );
        _;
    }
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L62-L68

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L75-L77

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L70
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L38

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/ZkSyncStateTransitionBase.sol#L46

### [Gas-N2] Use `delete` instead of setting variable value to `default`
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L91

### [Gas-N3] Instead of chaching `block.timestamp` prefer to directly used in code base
```diff
        unchecked {
            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
            // It is safe to cast.
-           uint32 timestamp = uint32(block.timestamp);
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
         
 - committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);  

 + committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, block.timestamp); 
            }  
        }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L117

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L134


### [Gas-N4] create `memory` variable outside the loop, and with each iteration override it, so that creation gas cost saved (Gas saved = creation cost * no.of iteration of loop)
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L186

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L210

```diff
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356

```diff
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356

### [Gas-N5] By moving less gas consuming check to up and more gas consuming check to below(Re-ordering) a significant amount of gas can saved during check failure
```diff
    function _schedule(bytes32 _id, uint256 _delay) internal {
-       require(!isOperation(_id), "Operation with this proposal id already exists");  
-       require(_delay >= minDelay, "Proposed delay is less than minimum delay");

 
+       require(_delay >= minDelay, "Proposed delay is less than minimum delay");
+       require(!isOperation(_id), "Operation with this proposal id already exists"); 

        timestamps[_id] = block.timestamp + _delay;
    }
```
Here we clearly see that first require check made a function call and then negeting its result
```solidity
    function isOperationDone(bytes32 _id) public view returns (bool) {
        return getOperationState(_id) == OperationState.Done;
    }
```
which futher call another function and check its result with a `enum` state variable

But 2nd `require()` just made a simple comparision check with a state variable `minDelay`
```solidity
require(_delay >= minDelay,
```

Its clear that 2nd one consume less gas, so it should move to top

No failure of this check, a significant amount of gas can saved as function will not need to run 1st expensive check

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L216-L217

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31


### [Gas-N6] `require( || )` should be split into individual `require` as it will be more gas efficient.
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L76


### [Gas-N7] Functions which have `onlySelf`, should be `payable` 
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L256

### [Gas-N8] `receive()` should emit something, or do something when it receive funds
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L262

### [Gas-N9]
```diff
    function _depositFundsToSharedBridge(address _from, IERC20 _token, uint256 _amount) internal returns (uint256) {
        uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
        _token.safeTransferFrom(_from, address(sharedBridge), _amount);
-       uint256 balanceAfter = _token.balanceOf(address(sharedBridge));   

-       return balanceAfter - balanceBefore;

+       return _token.balanceOf(address(sharedBridge)) - balanceBefore;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L160-L166

### [Gas-N10] `(msg.sender == address(bridgehub)` type of checks should done using `assembl`
```diff
        require(msg.sender == address(bridgehub), "ShB not BH");  // @audit G:: assembly
        _;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L69

### [Gas-N11] Refactoring `transferFundsFromLegacy()`
```diff
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
        if (_token == ETH_TOKEN_ADDRESS) {
            uint256 balanceBefore = address(this).balance;
            IMailbox(_target).transferEthToSharedBridge();

+           uint256 res = self.balance() - balanceBefore;
+           if(res != 0){
+           chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
+               chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] + res
+           }
-           uint256 balanceAfter = address(this).balance; 
-           require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
-           chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
-               chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
-               balanceAfter -
-               balanceBefore;
        } else {
            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
            require(amount > 0, "ShB: 0 amount to transfer");
            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
-           uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
-           require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");  

+           require(IERC20(_token).balanceOf(address(this)) - balanceBefore == amount, "ShB: wrong amount transferred");  
            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
        }
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116-L134


### [Gas-N12] `msg.value == _amount` check should preform using `assembly`
```diff
 require(msg.value == _amount,
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L155
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L158
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L202

### [Gas-N13] Instead of using `arbitary no.` in code those could stored in `const` 
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L258

### [Gas-N14] Instead of cahing we could preform direct comparision
```diff
            if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
-               bytes32 dataHash = depositHappened[_chainId][_l2TxHash];  
-               bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
-               require(dataHash == txDataHash, "ShB: d.it not hap");

+               require(depositHappened[_chainId][_l2TxHash] == keccak256(abi.encode(_depositSender, _l1Token, _amount)), "ShB: d.it not hap");
                delete depositHappened[_chainId][_l2TxHash];
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340-L342

### [Gas-N15] Reading Storage Mappings double time, those could be reduced to one time.
```diff
        if (!hyperbridgingEnabled[_chainId]) {
            // check that the chain has sufficient balance
+           uint256 res = chainBalance[_chainId][_l1Token];
-           require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");   
-           chainBalance[_chainId][_l1Token] -= _amount;

+           require(res >= _amount, "ShB n funds");   
+           chainBalance[_chainId][_l1Token] = res - _amount;
        }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L349-L350

### [Gas-N16] Struct could tightly packed (by reducing some elements size)
```
    struct MessageParams {
-       uint256 l2BatchNumber;   
-       uint256 l2MessageIndex;

+       uint128 l2BatchNumber;   
+       uint128 l2MessageIndex;
        uint16 l2TxNumberInBatch;
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L402-L403

### [Gas-N17] Instead of creating new `memory` variable we can simly override function input parameter for more convince.
```
    function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
        ....
        ....
            address refundRecipient = _refundRecipient;  
            if (_refundRecipient == address(0)) {
                refundRecipient = _prevMsgSender != tx.origin
                    ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
                    : _prevMsgSender;
            }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L577-L582

### [Gas-0]
```
```
```
```

### [Gas-N18] Both `stateTransitionManager` & `baseToken` mapping behave same way i.e first one tracking `chainId -> address(stateTransitionManager) and second one tracking `chainId -> address(baseToken)`, so both could be included each other via struct i.e `chainId -> struct(containing both stateTransitionManager, baseToken)
```diff
    mapping(address _token => bool) public tokenIsRegistered;

    /// @notice chainID => StateTransitionManager contract address, storing StateTransitionManager
    mapping(uint256 _chainId => address) public stateTransitionManager;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L26-29

### [Gas-N19] Optimizing event emission
Here by re-ordering `event` emmision gas used for `memory` variable creation and value assigning seved
```diff
    function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {  
        // Save previous value into the stack to put it into the event later
+       emit NewPendingAdmin(pendingAdmin, _newPendingAdmin);
-       address oldPendingAdmin = pendingAdmin;
        // Change pending admin
        pendingAdmin = _newPendingAdmin;
-       emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);  
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L115

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L62

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L86

### [Gas-N20] Instaed of setting variable to `default` use `delete`
```diff
    function removeStateTransitionManager(address _stateTransitionManager) external onlyOwner {
        require(
            stateTransitionManagerIsRegistered[_stateTransitionManager],
            "Bridgehub: state transition not registered yet"
        );
-       stateTransitionManagerIsRegistered[_stateTransitionManager] = false; 

+       delete stateTransitionManagerIsRegistered[_stateTransitionManager] ;
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L97

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L147

### [Gas-N21] Via decreasing size of `chainId` & `l2GasLimit` & tight packing we can save extra storage slot in struct `L2TransactionRequestDirect` & `L2TransactionRequestTwoBridgesOuter` (Gas saved -> 2 SLOT = 2*2000)

```diff
struct L2TransactionRequestDirect {
-   uint256 chainId;  // @audit G::
+   uint128 chainId;
+   uint128 l2GasLmit
    uint256 mintValue;
    address l2Contract;
    uint256 l2Value;
    bytes l2Calldata;
-   uint256 l2GasLimit;  // @audit G::
    uint256 l2GasPerPubdataByteLimit;
    bytes[] factoryDeps;
    address refundRecipient;
}

struct L2TransactionRequestTwoBridgesOuter {
-   uint256 chainId;  // @audit G::
+   uint128 chainId;
+   uint128 l2GasLmit
    uint256 mintValue;
    uint256 l2Value;
-   uint256 l2GasLimit; // @audit G::
    uint256 l2GasPerPubdataByteLimit;
    address refundRecipient;
    address secondBridgeAddress;
    uint256 secondBridgeValue;
    bytes secondBridgeCalldata;
}
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L10-L19

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/IBridgehub.sol#L22-L31

### [Gas-N22] `constant` should be a value rather than `expression`
```
bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2"); 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12


### [Gas-N23] `keccak256(` should be a `immutable` rather than `constant`
```
bytes32 private constant CREATE2_PREFIX = keccak256("zksyncCreate2"); 
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L12

### [Gas-N24] `facetCuts[i]` should cached in `memory` rather than calling it 5 times.
```diff
    function diamondCut(DiamondCutData memory _diamondCut) internal {
...
...
        for (uint256 i = 0; i < facetCutsLength; i = i.uncheckedInc()) {  // @audit G:: default initialization
            Action action = facetCuts[i].action;  // @audit G:: facetCuts[i] could cached rather calling 5 times
            address facet = facetCuts[i].facet;
            bool isFacetFreezable = facetCuts[i].isFreezable;   // @audit G:: 
            bytes4[] memory selectors = facetCuts[i].selectors;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L97-L105

### [Gas-N25] `memory` variable should create outside of loop and with each iteration it get overriden.
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L103-L105

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L139

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L159

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L179

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L35

### [Gas-N26] `ds.selectorToFacet[_selector]` mapping call should be cached in `memory` rater than calling it multiple times
```diff
    function _removeOneFunction(address _facet, bytes4 _selector) private {
        DiamondStorage storage ds = getDiamondStorage();

        // Get index of `FacetToSelectors.selectors` of the selector and last element of array
        uint256 selectorPosition = ds.selectorToFacet[_selector].selectorPosition;
        uint256 lastSelectorPosition = ds.facetToSelectors[_facet].selectors.length - 1;

        // If the selector is not at the end of the array then move the last element to the selector position
        if (selectorPosition != lastSelectorPosition) {
            bytes4 lastSelector = ds.facetToSelectors[_facet].selectors[lastSelectorPosition];   // @audit G:: ds.facetToSelectors[_facet] cache

            ds.facetToSelectors[_facet].selectors[selectorPosition] = lastSelector;
            ds.selectorToFacet[lastSelector].selectorPosition = selectorPosition.toUint16();
        }

        // Remove last element from the selectors array
        ds.facetToSelectors[_facet].selectors.pop();

        // Finally, clean up the association with facet
        delete ds.selectorToFacet[_selector];

        // If there are no selectors for facet then remove the facet from the list of known facets
        if (lastSelectorPosition == 0) {
            _removeFacet(_facet);
        }
    }
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L228-L247

### [Gas-N27] 2 events could be enclosed
```diff
 admin = currentPendingAdmin;
        delete pendingAdmin;

        emit NewPendingAdmin(currentPendingAdmin, address(0));  // @audit G:: both event could combined
        emit NewAdmin(previousAdmin, pendingAdmin);
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127-128

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40-L41

### [Gas-N28] Instead of dynamic storage like `string` try to use some fixed type storage like `bytes32`
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L25

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L28


### [Gas-N29] Operation `%` can be optimizable via using `asembly` as follows
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30




### [Gas-N30]
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L

### [Gas-N31]
#### `protocolVersion` could cached in memory
```
        L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
...
...
            nonce: protocolVersion, // @audit G:: state variable chache
            value: 0,
            reserved: [uint256(0), 0, 0, 0],
...
...
        });

        ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
....
....
            newProtocolVersion: protocolVersion  // @audit G:: 
        });
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L192

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L216

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L111


### [Gas-N34] Instead of `address(this).balance` try to use `self.balance`

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41

### [Gas-1] Stack variable is only used once
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L65

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L192

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L206
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L467

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L135

### [Gas-2] Use assembly for Efficient Event Emission
```
```
```
```



### [Gas-3] Assembly: Check msg.sender using xor and the scratch space
```
```
```
```

### [Gas-4] Assembly: Use scratch space when building emitted events with two data arguments
```
```
```
```

### [Gas-5] Use assembly to write mutable storage values
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L74

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L143

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L143

### [Gas-6] Avoid Zero to Non-Zero Storage Writes Where Possible
```
```
```
```

### [Gas-7] Use unchecked for division which do not divide by -X sonce they can't overflow
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L23
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/LibMap.sol#L43

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L7

### [Gas-8] Use unchecked for %
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L8

### [Gas-9] abi.encodePacked is more gas efficient than abi.encode
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L58

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100-L102

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L323

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104

### [Gas-10] Multiple address/ID mappings can be combined into a single mapping of an address/ID to a struct
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L27

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L32

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L51

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L52

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L57

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L65

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L114


### [Gas-11] Use solady library where possible to save gas
```
```
```
```

### [Gas-12] Cache multiple accesses of mapping/array values
```
```
```
```

### [Gas-13] Cache state variables accessed multiple times in the same function
```
```
```
```

### [Gas-14] Mappings are cheaper to use than storage arrays
```
```
```
```

### [Gas-15] Nesting if-statements is cheaper than using &&
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L41

### [Gas-16] Redundant state variable getters
```
```
```
```


### [Gas-17] Redundant type conversion
```
```
```
```

### [Gas-18] Replace OpenZeppelin components with Solady equivalents to save gas
```
```
```
```

### [Gas-19] Simple checks for zero can be done using assembly to save gas
```diff
```

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L186

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L279

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L19

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L185

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L19

### [Gas-20] The result of function calls should be cached rather than re-calling the function
```
```
```
```
### [Gas-21] Use calldata instead of memory for function arguments that are read only
```
```
```
```


### [Gas-22] Assembly: Use scratch space for calculating small keccak256 hashes
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L205

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L598

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L100
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L102
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L138
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L156

### [Gas-23] Assembly: Use scratch space when building emitted events with two data arguments
```
```
```
```


### [Gas-24] Use assembly to check for address(0)
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L42

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L33

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L108
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L118
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L237


```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L109

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L30

### [Gas-25] Optimize Gas by Using Only Named Returns
```
```
```
```

### [Gas-26] Simple checks for zero uint can be done using assembly to save gas
```
```
```
```

### [Gas-27] Use Assembly for Efficient Memory Management in Multiple External Calls
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L43

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L226

### [Gas-28] Use Assembly for Hash Calculations
```
```
```
```

### [Gas-29] Use unchecked for Math Operations if they already checked
```
```
```
```

### [Gas-30] Avoid transferring amounts of zero in order to save gas
```
```
```
```

### [Gas-31] Reduce deployment costs by tweaking contracts' metadata
```
```
```
```

### [Gas-32] Constructors can be marked payable
```
```
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L90

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L90



### [Gas-33] Use unchecked for Non-Loop Increment/Decrement Operations
```
```
```
```

### [Gas-34] Call msg.sender directly instead of caching it
```
```
```
```

### [Gas-35] Consider pre-calculating the address of address(this) to save gas
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L59


### [Gas-36] Use more recent OpenZeppelin version for gas boost
```
```
```
```

### [Gas-37] Enable IR-based code generation
```
```
```
```

### [Gas-38] Avoid updating storage when the value hasn't changed
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L258

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L251

### [Gas-39] Optimize External Calls with Assembly for Memory Efficiency
```
```
```
```

### [Gas-40] Use named return parameters
```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L65


```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L73

```
```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L147

### [Gas-41] Optimize names to save gas
```
```
```
```

### [Gas-42] Inline modifiers that are only used once, to save gas
```
```
```
```

### [Gas-43] Inline internal functions that are only called once
```
```
```
```


### [Gas-44] PreIncreament (++i) costs less than PostIncrement(i++)
```
```
```
```

### [Gas-45] Some state variable could be `private` rather than `public`
```
```

https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L35
