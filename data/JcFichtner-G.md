## [G-01] Optimizing the L1ERC20Bridge Contract

While the provided contract seems well-structured, there are still some potential areas for gas optimization:

###### General Optimizations

**1 - Cache Storage Variables:**

- In functions like `deposit` and `claimFailedDeposit`, the `depositAmount` mapping is accessed multiple times. Cache the value in a local variable to reduce storage reads.

**2 - Use Unchecked Math:**

- In functions like `_depositFundsToSharedBridge`, where overflows are unlikely due to prior checks or context, consider using unchecked blocks for arithmetic operations.

**3 - Use Custom Errors:**

- Replace `require` statements with custom errors for specific error conditions. This can save gas by reducing the amount of data stored and returned in the revert message.

###### Specific Optimizations

**1 - `deposit` function:**

Instead of calling `_depositFundsToSharedBridge` and then checking if the `amount` is equal to `_amount`, consider modifying `_depositFundsToSharedBridge` to return a boolean indicating success and using a require statement based on the returned value. This can save gas by avoiding an additional comparison.

**2 - `finalizeWithdrawal` function:**

The `isWithdrawalFinalized` mapping is checked and then never used again. Consider removing this check and relying solely on the shared bridge's check to save gas.

###### Additional Considerations

**1 - Use of `safeTransfer` and `safeTransferFrom`:**

While these functions provide additional safety checks, they consume more gas than the standard `transfer` and `transferFrom` functions. If the token contract is known to be reliable and the amounts are guaranteed to be valid, consider using the standard transfer functions instead.

**2 - Alternatives to OpenZeppelin:**

Libraries like `Solmate` and `Solady` offer gas-efficient implementations of common functions. Consider exploring these alternatives for further optimization.

## [G-02] Optimizing the L1SharedBridge Contract

The L1SharedBridge contract facilitates the bridging of assets between Layer 1 (L1) and various hyperchains, supporting both ETH and ERC20 tokens. It's designed to work with a proxy for upgradability, and it interacts with a Bridgehub contract for cross-chain operations, a legacy bridge for backward compatibility, and maintains a mapping of L2 bridges for different chains. The contract includes mechanisms for depositing, withdrawing, and handling failed transactions, with provisions for non-reentrancy and initializable patterns for security and upgradeability.

Here are some gas optimizations for this contract:

###### General Optimizations

**1 - Cache Storage Variables:**

***(A) - `depositHappened` mapping:***

In the `claimFailedDeposit` function, the `depositHappened` mapping is accessed twice:

- First, to check if the deposit happened: `require(depositHappened[_chainId][_l2TxHash] != 0x00, "ShB tx hap");`

- Second, to delete the record after successful claim: `delete depositHappened[_chainId][_l2TxHash];`

***Optimization:*** Cache the value of `depositHappened[_chainId][_l2TxHash]` in a local variable at the beginning of the function and use the local variable for both checks and deletion. This saves one storage read.

***(B) - `chainBalance` mapping:***

In both `claimFailedDeposit` and `_finalizeWithdrawal` functions, the `chainBalance` mapping is accessed twice:

- First, to check if the chain has sufficient balance: `require(chainBalance[_chainId][l1Token] >= amount, ...);`

- Second, to update the balance after withdrawal: `chainBalance[_chainId][l1Token] -= amount;`

***Optimization:*** In both functions, cache the value of `chainBalance[_chainId][l1Token]` in a local variable before the checks and updates. This saves one storage read per function.

**2 - Use Unchecked Math:**

- In the `_depositFunds` function, the subtraction operation `balanceAfter - balanceBefore` is unlikely to underflow due to the prior transfer of tokens. You can wrap this operation in an unchecked block

**3 - Use Custom Errors:**

- Replace `require` statements with custom errors for specific error conditions to save gas on revert messages.

## [G-03] Optimizing the Bridgehub Contract

This contract serves as a central hub for bridging operations, so optimizing it for gas efficiency is crucial. Here are some potential areas for improvement:

###### General Optimizations

1 - Cache Storage Variables:

- In the `requestL2TransactionDirect` function, `the baseToken[_request.chainId]` mapping is accessed twice. Instead, you can cache the value in a local variable

2 - Use Unchecked Math:

- In the createNewChain function, the _chainId is checked to be within the valid range of uint48. Therefore, the subsequent operation _chainId <= type(uint48).max is guaranteed to be true and will not overflow. You can wrap this operation in an unchecked

3 - Use Custom Errors:

- Replace require statements with custom errors for specific error conditions to save gas on revert messages.
Specific Optimizations:

###### Specific Optimizations

Both `requestL2TransactionDirect` and `requestL2TransactionTwoBridges` handle deposits for both `ETH` and `non-ETH` tokens. However, they currently have separate code blocks for each case, leading to redundancy. Here's how we can refactor them to share common code:

**1 - Extract Common Logic:**

Create a new internal function, let's call it `_handleDeposit`, that takes the following arguments:

- `uint256 _chainId`: The chain ID for the transaction.
- `address _sender`: The sender of the transaction.
- `address _token`: The token being deposited (ETH or ERC20).
- `uint256 _amount`: The amount being deposited.

This function will handle the common logic for both `ETH` and `non-ETH` deposits:

function _handleDeposit(
    uint256 _chainId,
    address _sender,
    address _token,
    uint256 _amount
) internal {
    if (_token == ETH_TOKEN_ADDRESS) {
        require(msg.value == _amount, "Bridgehub: msg.value mismatch");
    } else {
        require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
        uint256 withdrawAmount = _depositFunds(_sender, IERC20(_token), _amount);
        require(withdrawAmount == _amount, "Bridgehub: deposit amount mismatch");
    }

    if (!hyperbridgingEnabled[_chainId]) {
        chainBalance[_chainId][_token] += _amount;
    }
}

1 - Update Existing Functions:

Now, update `requestL2TransactionDirect` and `requestL2TransactionTwoBridges` to call `_handleDeposit` instead of having separate logic for `ETH` and `non-ETH` tokens. 

Here's how the updated functions would look:

- requestL2TransactionDirect:

function requestL2TransactionDirect(
    L2TransactionRequestDirect calldata _request
) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
    address token = baseToken[_request.chainId];
    _handleDeposit(_request.chainId, msg.sender, token, _request.mintValue);

    // ... rest of the function logic ...
}

- requestL2TransactionTwoBridges:

function requestL2TransactionTwoBridges(
    L2TransactionRequestTwoBridgesOuter calldata _request
) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
    address token = baseToken[_request.chainId];
    uint256 baseTokenMsgValue = (token == ETH_TOKEN_ADDRESS) ? _request.mintValue : 0;

    _handleDeposit(_request.chainId, msg.sender, token, _request.mintValue);

    // ... rest of the function logic ...
}

By extracting the common logic into `_handleDeposit`, we reduce code redundancy and improve the contract's maintainability. This can also lead to gas savings due to reduced code size and fewer conditional checks.

## [G-04] Optimizing the Governance Contract

This contract manages governance operations, so optimizing it for gas efficiency is important to ensure smooth and cost-effective governance processes. Here are some potential areas for improvement:

###### General Optimizations

**1 - Cache Storage Variables:**

 - Functions like `isOperationReady` and execute access the `timestamps` mapping multiple times. Cache the relevant timestamp in a local variable to reduce storage reads.

**2 - Use Unchecked Math:**

- In functions like `_schedule`, where overflows are unlikely due to prior checks or context, consider using unchecked blocks for arithmetic operations.

**3 - Use Custom Errors:**

- Replace `require` statements with custom errors for specific error conditions to save gas on revert messages.
































