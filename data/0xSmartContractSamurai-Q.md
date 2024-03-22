0. QA/LOW: Unless it is intended functionality, it seems indeed possible to remove a current/old facet and add back the same old facet during the same `_replaceFunctions()` function call when passing the old facet address `oldFacet.facetAddress` as the `_facet` parameter value.

https://github.com/code-423n4/2024-03-zksync/blob/e3668e0e4cfdb6d6bbb77f1e9822394998b7eb18/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L147-L168

It will effectively remove the old facet via `_removeOneFunction(oldFacet.facetAddress, selector)` and then add it back again via `_addOneFunction(_facet, selector, _isFacetFreezable)`.

```solidity
    /// @dev Change associated facets to already known function selectors
    /// NOTE: expect but NOT enforce that `_selectors` is NON-EMPTY array
    function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
        DiamondStorage storage ds = getDiamondStorage();

        // Facet with no code cannot be added.
        // This check also verifies that the facet does not have zero address, since it is the
        // address with which 0x00000000 selector is associated.
        require(_facet.code.length > 0, "K");

        uint256 selectorsLength = _selectors.length;
        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

            _removeOneFunction(oldFacet.facetAddress, selector);
            // Add facet to the list of facets if the facet address is a new one
            _saveFacetIfNew(_facet);
            _addOneFunction(_facet, selector, _isFacetFreezable);
        }
    }
```
# IMPACT:
- should be QA/LOW impact, although we want to avoid unlikely scenarios where the relevant privileged account mistakenly passes the old facet address instead of another/new facet address and then no one is any wiser until sometime after. So for this reason alone, should rather be on the safe side.

# PoC:

Check the "Recommendation" section at the bottom after the PoC tests, I've added the following 3 lines to the library function, for the test:
```solidity
           bool is_facetParamEqualTo_oldFacetAddress = oldFacet.facetAddress == _facet;
           emit CheckFacetChangeResult(oldFacet.facetAddress, _facet, selector, is_facetParamEqualTo_oldFacetAddress);
           require(oldFacet.facetAddress != _facet, "old facet and new/replacement facet is same address");
```

Simple PoC test to prove the function allows for `_facet` parameter address value to be equal to the old facet address.

Test command used:
`forge test --contracts test/foundry/unit/concrete/DiamondCut/UpgradeLogic.t.sol --mt test_ExecuteDiamondCut -vvvv`

# Test 1: without the require check

The following test result proves/demonstrates it's possible to pass old facet's address when supposed to be new/replacement facet's address for `_replaceFunctions()`:
```solidity
$ forge test --contracts test/foundry/unit/concrete/DiamondCut/UpgradeLogic.t.sol --mt test_ExecuteDiamondCut -vvvv
[⠢] Compiling...
No files changed, compilation skipped

Ran 1 test for test/foundry/unit/concrete/DiamondCut/UpgradeLogic.t.sol:UpgradeLogicTest
[PASS] test_ExecuteDiamondCut() (gas: 638139)
Traces:
  [638139] UpgradeLogicTest::test_ExecuteDiamondCut()
    ├─ [6999] Utils::getGettersSelectors() [delegatecall]
.
.
.
    │   ├─ [531409] AdminFacet::executeUpgrade(DiamondCutData({ facetCuts: [FacetCut({ facet: 0x0F8458E544c9D4C7C25A881240727209caae20B8, action: 1, is
.
.
.
    │   │   ├─ emit CheckFacetChangeResult(oldFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], newOrReplacementFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], selector: 0x46657fe900000000000000000000000000000000000000000000000000000000, isOldFacetEqualToNewFacetAddress: true)
    │   │   ├─ emit CheckFacetChangeResult(oldFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], newOrReplacementFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], selector: 0x6e9960c300000000000000000000000000000000000000000000000000000000, isOldFacetEqualToNewFacetAddress: true)
    │   │   ├─ emit CheckFacetChangeResult(oldFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], newOrReplacementFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], selector: 0xd046815600000000000000000000000000000000000000000000000000000000, isOldFacetEqualToNewFacetAddress: true)
.
.
.
    │   │   ├─ emit CheckFacetChangeResult(oldFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], newOrReplacementFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], selector: 0x7b30c8da00000000000000000000000000000000000000000000000000000000, isOldFacetEqualToNewFacetAddress: true)
    │   │   ├─ emit DiamondCut(facetCuts: [FacetCut({ facet: 0x0F8458E544c9D4C7C25A881240727209caae20B8, action: 1, isFreezable: true, selectors: [0x46
.
.
.
    ├─ [1655] DiamondProxy::isFunctionFreezable(0x7b30c8da00000000000000000000000000000000000000000000000000000000) [staticcall]
    │   ├─ [874] GettersFacet::isFunctionFreezable(0x7b30c8da00000000000000000000000000000000000000000000000000000000) [delegatecall]
    │   │   └─ ← true
    │   └─ ← true
    └─ ← ()

Suite result: ok. 1 passed; 0 failed; 0 skipped; finished in 6.85ms (3.09ms CPU time)
```
- You want to check my emitted events in above test result: `emit CheckFacetChangeResult`

# Test 2: with the require check added:
```solidity
    │   │   ├─ emit CheckFacetChangeResult(oldFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], newOrReplacementFacetAddress: GettersFacet: [0x0F8458E544c9D4C7C25A881240727209caae20B8], selector: 0x46657fe900000000000000000000000000000000000000000000000000000000, isOldFacetEqualToNewFacetAddress: true)
    │   │   └─ ← revert: old facet and new/replacement facet is same address
    │   └─ ← revert: old facet and new/replacement facet is same address
    └─ ← revert: old facet and new/replacement facet is same address

Suite result: FAILED. 0 passed; 1 failed; 0 skipped; finished in 4.30ms (344.58µs CPU time)

Ran 1 test suite in 2.12s (4.30ms CPU time): 0 tests passed, 1 failed, 0 skipped (1 total tests)

Failing tests:
Encountered 1 failing test in test/foundry/unit/concrete/DiamondCut/UpgradeLogic.t.sol:UpgradeLogicTest
[FAIL. Reason: revert: old facet and new/replacement facet is same address] test_ExecuteDiamondCut() (gas: 56075)

Encountered a total of 1 failing tests, 0 tests succeeded
```
- See the revert message above from the require check

# Recommendation:

Add a require check or at least emit an event to inform that the passed address for the `_facet` parameter is the same as the old facet address.

So for example, we can add a new event to the Diamond.sol library contract:
`event CheckFacetChangeResult(address oldFacetAddress, address newOrReplacementFacetAddress, bytes4 selector, bool isOldFacetEqualToNewFacetAddress);`

and then add the event and possibly a require check to the `_replaceFunctions()` function:
```diff
    function _replaceFunctions(address _facet, bytes4[] memory _selectors, bool _isFacetFreezable) private {
        DiamondStorage storage ds = getDiamondStorage();

        // Facet with no code cannot be added.
        // This check also verifies that the facet does not have zero address, since it is the
        // address with which 0x00000000 selector is associated.
        require(_facet.code.length > 0, "K");

        uint256 selectorsLength = _selectors.length;
        for (uint256 i = 0; i < selectorsLength; i = i.uncheckedInc()) {
            bytes4 selector = _selectors[i];
            SelectorToFacet memory oldFacet = ds.selectorToFacet[selector];
            require(oldFacet.facetAddress != address(0), "L"); // it is impossible to replace the facet with zero address

+           bool is_facetParamEqualTo_oldFacetAddress = oldFacet.facetAddress == _facet;
+           emit CheckFacetChangeResult(oldFacet.facetAddress, _facet, selector, is_facetParamEqualTo_oldFacetAddress);
+           require(oldFacet.facetAddress != _facet, "old facet and new/replacement facet is same address");
            
            _removeOneFunction(oldFacet.facetAddress, selector);
            // Add facet to the list of facets if the facet address is a new one
            _saveFacetIfNew(_facet);
            _addOneFunction(_facet, selector, _isFacetFreezable);
        }
    }
```
=======
=======
