# Improve Logic in Setter Functions in the `Bridgehub` contract

## Impact
Eliminate unnecessary caching: If the old value solely serves immediate actions (e.g., event emission), access it directly within the setter. This streamlines code, potentially reduces memory overhead, and enhances readability.

## Proof of Concept
[Bridgehub::setPendingAdmin](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L56C1-L56C65)
```solidity
    function setPendingAdmin(
        address _newPendingAdmin
) external onlyOwnerOrAdmin {

+       emit NewPendingAdmin(pendingAdmin, _newPendingAdmin);
+       pendingAdmin = _newPendingAdmin;

-        // Save previous value into the stack to put it into the event later
-       address oldPendingAdmin = pendingAdmin;
-       // Change pending admin
-        pendingAdmin = _newPendingAdmin;
-       emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
}
```


## Tools Used

Manual Review

## Recommendations
When the old value is only required for immediate actions within the function, directly access it instead of caching, which streamlines code, potentially reduces memory overhead, and improves code readability.
