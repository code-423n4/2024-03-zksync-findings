### Report 1:
#### Denial of Service
The code below shows the implementation of transferFundsFromLegacy(...) function in the L1SharedBridge contract, as noted from the comment description this function is suppose to be a part of the migration process, the function is assuming token must be transferred during the migration process but this is wrong as there might be circumstances where there is no token to be transferred and the migration must proceed, this would not work due to the validation that requires balance after to be greater than balance before, thereby causing Denial of Service when there is no token to be transferred. Protocol should reconsider the code Design.
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L115
```solidity
>>>    /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
        if (_token == ETH_TOKEN_ADDRESS) {
            uint256 balanceBefore = address(this).balance;
            IMailbox(_target).transferEthToSharedBridge();
            uint256 balanceAfter = address(this).balance;
>>>            require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
                balanceAfter -
                balanceBefore;
        } else {
            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
>>>            require(amount > 0, "ShB: 0 amount to transfer");
            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
        }
    }
```
###  Report 2:
