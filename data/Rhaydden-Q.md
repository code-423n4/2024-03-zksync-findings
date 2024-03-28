
## Title
 Empty Payable Fallback Function in Governance Contract


## Description

```solidity
 receive() external payable {}
}
```
The `Governance.sol` contract contains an empty payable fallback function  that lacks explicit functionality and access control. This could lead to unintended behavior, such as accepting ETH without any mechanism to handle or store it, and inadvertently locked funds due to the lack of access control. Consider adding logic within the payable fallback function to handle incoming ETH appropriately and add access control mechanisms to ensure that only authorized addresses can send ETH to the contract.


There are 3 instances of this issue:

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L262

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/EmptyContract.sol#L10-L14

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L227


