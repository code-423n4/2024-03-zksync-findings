# QA Report

## 

## [L-1] Mismatch Between ``tranferTokenToSharedBridge`` and documented functionality

The function name ``tranferTokenToSharedBridge`` is missing an ``s``, making it an incorrect spelling of the intended action, which is ``transfer``.

Smart contracts where precision is crucial, every character matters. A typo can lead to misunderstandings or, in worse cases, the malfunction of contract execution if the function name is called or referenced elsewhere with the correct spelling.

```diff
FILE: https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

62: /// @dev transfer token to shared bridge as part of upgrade
- 63:    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
+ 63:    function transferTokenToSharedBridge(address _token, uint256 _amount) external {

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L63

## 

## [L-2] Mismatch between comment and the actual implementation

- ``Comment Description`` : The comment ``/// @dev transfer token to shared bridge as part of upgrade`` suggests that the function is designed to transfer a specified amount of tokens to the shared bridge, presumably as part of a smart contract upgrade process. The comment implies flexibility in the amount of tokens to be transferred.

- ``Actual Implementation``: The actual code, however, does not align with this flexibility. Instead of transferring the amount specified by the caller ``(_amount)``, the function transfers the entire balance of tokens held by the contract ``(amount = IERC20(_token).balanceOf(address(this)))``. Furthermore, the function enforces that this total balance must match the ``_amount`` specified by the caller, which effectively restricts the transfer to only the total balance rather than allowing a specific, potentially partial, amount.

```solidity
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1ERC20Bridge.sol

/// @dev transfer token to shared bridge as part of upgrade
    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
        require(msg.sender == address(sharedBridge), "Not shared bridge");
        uint256 amount = IERC20(_token).balanceOf(address(this));
        require(amount == _amount, "Incorrect amount");
        IERC20(_token).safeTransfer(address(sharedBridge), amount);
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L62-L68

### Recommended Mitigation

- Align the Comment to the Actual Code (Only Full Balance Transfers)

```solidity

/// @dev Transfers the entire token balance to the shared bridge as part of an upgrade, ensuring no partial token transfers.
function transferTokenToSharedBridge(address _token, uint256 _amount) external {
    require(msg.sender == address(sharedBridge), "Not shared bridge");
    uint256 amount = IERC20(_token).balanceOf(address(this));
    require(amount == _amount, "Incorrect amount");
    IERC20(_token).safeTransfer(address(sharedBridge), amount);
}

```

##

## [L-1] Typo Error

The comment /// @dev tranfer tokens... contains a spelling mistake: tranfer should be transfer.

```diff
FILE: 2024-03-zksync/code/contracts/ethereum/contracts/bridge
/L1SharedBridge.sol

- 115: /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
+ 115: /// @dev transfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process

```
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L115


