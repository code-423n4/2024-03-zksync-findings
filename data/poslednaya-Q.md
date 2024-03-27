# Event in `acceptAdmin()` emits `newAdmin` as zero-address

# Lines of code

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L69

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L119

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L32

# Summary

Basing on emits-info current admin of contract always be `address(0)`. Just because we delete `pendingAdmin` variable and than emitted it in `NewPendingAdmin()`. This logic exist in all `acceptAdmin()` functions through protocol. 

```solidity
    event NewAdmin(address indexed oldAdmin, address indexed newAdmin);

    function acceptAdmin() external {
        address currentPendingAdmin = pendingAdmin;
        require(msg.sender == currentPendingAdmin, "n42"); // Only proposed by current admin address can claim the admin rights

        address previousAdmin = admin;
        admin = currentPendingAdmin;
        delete pendingAdmin;

        emit NewPendingAdmin(currentPendingAdmin, address(0));
        emit NewAdmin(previousAdmin, pendingAdmin);
    }
```

# Recommendation

Consider change ->

```solidity
emit NewAdmin(previousAdmin, currentPendingAdmin)
```

