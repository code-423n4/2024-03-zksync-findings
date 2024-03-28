
## Summary


## Low Risk Issues

### [L-1] safeApprove() is deprecated

Deprecated in favor of safeIncreaseAllowance() and safeDecreaseAllowance(). If only setting the initial allowance to the value that means infinite, safeIncreaseAllowance() can be used instead. The function may currently work, but if a bug is found in this version of OpenZeppelin, and the version that you're forced to upgrade to no longer has this function, you'll encounter unnecessary delays in porting and testing replacement contracts.

```solidity
file: TransactionHelper.sol

382                IERC20(token).safeApprove(paymaster, 0);
383                IERC20(token).safeApprove(paymaster, minAllowance);


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol


### [L-2] Empty receive()/fallback() function

If the intention is for Ether sent by a caller to be used for an actual purpose (i.e. the function is not just a WETH withdraw() handler), the function should call another function (e.g. call weth.deposit() and use the token on the caller's behalf) or at least emit an event to track that funds were sent directly to it.

```solidity
file: /system-contracts/contracts/EmptyContract.sol

11    fallback() external payable {}

13    receive() external payable {}

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/EmptyContract.sol


```solidity
file: /contracts/ethereum/contracts/governance/Governance.sol

262    receive() external payable {}


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol


```solidity
file: /system-contracts/contracts/DefaultAccount.sol

277    receive() external payable {
        // If the contract is called directly, behave like an EOA
    }

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol



### [L-3] `name()` is not a part of the ERC-20 standard

The `name()` function is not a part of the ERC-20 standard, and was added later as an optional extension. As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.

```solidity
file: /contracts/zksync/contracts/bridge/L2StandardERC20.sol

162        return super.name();


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


### [L-4] `symbol()` is not a part of the ERC-20 standard


The symbol() function is not a part of the ERC-20 standard, and was added later as an optional extension. As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.

```solidity
file: /contracts/zksync/contracts/bridge/L2StandardERC20.sol

165    function symbol() public view override returns (string memory) {
        // If method is not available, behave like a token that does not implement this method - revert on call.
        if (availableGetters.ignoreSymbol) revert();
        return super.symbol();
    }


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol




### [L-5] `decimals()` is not a part of the ERC-20 standard

The `decimals()` function is not a part of the ERC-20 standard, and was added later as an optional extension. As such, some valid ERC20 tokens do not support this interface, so it is unsafe to blindly cast all tokens to this interface, and then call this function.

```solidity
file: /contracts/zksync/contracts/bridge/L2StandardERC20.sol

171    function decimals() public view override returns (uint8) {
        // If method is not available, behave like a token that does not implement this method - revert on call.
        if (availableGetters.ignoreDecimals) revert();
        return decimals_;

```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol


## Non Critical Issues

no | Issue |Instances||
|-|:-|:-:|:-:|
| [N-01] | Import declarations should import specific identifiers, rather than the whole file | 8 | 
| [N-02] | Long functions should be refactored into multiple, smaller, functions | 1 | 



### [N-1] Import declarations should import specific identifiers, rather than the whole file
Using import declarations of the form import `{<identifier_name>} from "some/file.sol" `avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation (but does not save any gas)

```solidity
file: contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol

5  import "./IL1SharedBridge.sol";


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/interfaces/IL1ERC20Bridge.sol


```solidity
file: /contracts/ethereum/contracts/bridgehub/Bridgehub.sol

7   import "./IBridgehub.sol";
    import "../bridge/interfaces/IL1SharedBridge.sol";
    import "../state-transition/IStateTransitionManager.sol";
    import "../common/ReentrancyGuard.sol";
    import "../state-transition/chain-interfaces/IZkSyncStateTransition.sol";

14  import "../vendor/AddressAliasHelper.sol";


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol



### [N-2] Long functions should be refactored into multiple, smaller, functions

```solidity
file: /system-contracts/contracts/libraries/TransactionHelper.sol

///@audit 68 line

147    function _encodeHashLegacyTransaction(Transaction calldata _transaction) private view returns (bytes32) {


```
https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol

