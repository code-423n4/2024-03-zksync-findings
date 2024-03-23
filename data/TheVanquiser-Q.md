a useless payable function and check of msg.value on ``finalizeDeposit``
```
function finalizeDeposit(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        bytes calldata _data
    ) external payable override {
        // Only the L1 bridge counterpart can initiate and finalize the deposit.
        require(
            AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
                AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
            "mq"
        );
        require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```
this function called for ERC20 bridge, ``L1SharedBridge._getDepositL2Calldata`` called ``L2SharedBridge.finalizeDeposit`` without ether value.
so the payable function and check of msg.value on ``finalizeDeposit`` function is useless

Recommendation:
remove payable and check of msg.value on ``finalizeDeposit`` function