## Inconvient input, contract balance is always gonna get transferred
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L62-L69)
```solidity

    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
        require(msg.sender == address(sharedBridge), "Not shared bridge");
        uint256 amount = IERC20(_token).balanceOf(address(this));
        //@audit inconvenient, if it is always going to transfer the contract balance, why take input from the user
        require(amount == _amount, "Incorrect amount");
        IERC20(_token).safeTransfer(address(sharedBridge), amount);
    }
```


## Require target address does not equal this contract address

### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116-L116)
```solidity
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId)

```

## Function should emit an event
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L116-L116)
```solidity
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId)

```    

## Require `from` does not equal address(this)
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L178-L178)
```solidity
        _token.safeTransferFrom(_from, address(this), _amount);

```

## Require `amount` to be equal `msg.value`
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L185-L185)
```solidity
    function bridgehubDeposit(

```

## Check if token is not blacklisted
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L463-L463)
```solidity
    function _checkWithdrawal(

```
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L560-L560)
```solidity
    function depositLegacyErc20Bridge(

```

## Require token is not black listed and not weth
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L103-L103)
```solidity
    function addToken(address _token) external onlyOwner 

```
## set isOperationPending to false
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L154-L159)
```solidity

```

## Change operation state
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L168-L183)
```solidity
    function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
        bytes32 id = hashOperation(_operation);
        // Check if the predecessor operation is completed.
        _checkPredecessorDone(_operation.predecessor);
        // Ensure that the operation is ready to proceed.
        require(isOperationReady(id), "Operation must be ready before execution");
        // Execute operation.
        _execute(_operation.calls);
        // Reconfirming that the operation is still ready after execution.
        // This is needed to avoid unexpected reentrancy attacks of re-executing the same operation.
        require(isOperationReady(id), "Operation must be ready after execution");
        // Set operation to be done
        timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
        //@audit change operation state
        emit OperationExecuted(id);
    }
```
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L188-L203)
```solidity
    function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
        bytes32 id = hashOperation(_operation);
        // Check if the predecessor operation is completed.
        _checkPredecessorDone(_operation.predecessor);
        // Ensure that the operation is in a pending state before proceeding.
        require(isOperationPending(id), "Operation must be pending before execution");
        // Execute operation.
        _execute(_operation.calls);
        // Reconfirming that the operation is still pending before execution.
        // This is needed to avoid unexpected reentrancy attacks of re-executing the same operation.
        require(isOperationPending(id), "Operation must be pending after execution");
        // Set operation to be done
        timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
        //@audit change operation state
        emit OperationExecuted(id);
    }
```
## Avoid on-chain computations
### Instances
* [Link to code](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L52-L52)
```solidity
        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);

```
