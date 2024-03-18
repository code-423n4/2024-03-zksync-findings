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
#### No Correlation between Old Protocol Version and New Protocol Version
The implementation to set new Version for Protocol Upgrade shows that there is no correlation or validation between Old and New Version used, the implication of this is that there can be overlap of old and new version since the correct data usage is only determined by parameter and no validation in the code
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L147
```solidity
   function setNewVersionUpgrade(
        Diamond.DiamondCutData calldata _cutData,
        uint256 _oldProtocolVersion,
        uint256 _newProtocolVersion
    ) external onlyOwner {
>>>        upgradeCutHash[_oldProtocolVersion] = keccak256(abi.encode(_cutData));
>>>        protocolVersion = _newProtocolVersion;
    }
```
###  Report 3:
#### Zero Expiry Period
As noted in the Config.sol contract Priority Expiration is not given any value at all, instead it is empty which means expiration period is no period at all.
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Config.sol#L37
```solidity
/// @dev The amount of time in seconds the validator has to process the priority transaction
/// NOTE: The constant is set to zero for the Alpha release period
uint256 constant PRIORITY_EXPIRATION = 0 days;
```
###  Report 4:
#### Non Registration of check
As noted in the createNewChain(...) function provided below, check was not registered, the necessary registration should be done to avoid contract error.
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L251
```solidity
function createNewChain(
        uint256 _chainId,
        address _baseToken,
        address _sharedBridge,
        address _admin,
        bytes calldata _diamondCut
    ) external onlyBridgehub {
        if (stateTransition[_chainId] != address(0)) {
            // StateTransition chain already registered
            return;
        }

>>>        // check not registered
        Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));

        // check input
        bytes32 cutHashInput = keccak256(_diamondCut);
        require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");
```
###  Report 5:
#### Incomplete Implementation
The code provided below from the Mailbox contract shows how _writePriorityOp(...) function is implemented, as noted from the pointer - "Restore after fee modeling will be stable. (SMA-1230)", this was not implemented in the code and should be corrected.
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L338
```solidity
function _writePriorityOp(
        WritePriorityOpParams memory _priorityOpParams,
        bytes memory _calldata,
        bytes[] memory _factoryDeps
    ) internal returns (bytes32 canonicalTxHash) {
        L2CanonicalTransaction memory transaction = _serializeL2Transaction(_priorityOpParams, _calldata, _factoryDeps);

        bytes memory transactionEncoding = abi.encode(transaction);

        TransactionValidator.validateL1ToL2Transaction(
            transaction,
            transactionEncoding,
            s.priorityTxMaxGasLimit,
            s.feeParams.priorityTxMaxPubdata
        );

        canonicalTxHash = keccak256(transactionEncoding);

        s.priorityQueue.pushBack(
            PriorityOperation({
                canonicalTxHash: canonicalTxHash,
                expirationTimestamp: _priorityOpParams.expirationTimestamp,
>>>                layer2Tip: uint192(0) // TODO: Restore after fee modeling will be stable. (SMA-1230)
            })
        );
```
###  Report 6:
#### Code does not Revert When Operation is not Done
The code in the Governance contract below is suppose to revert if Operation is not done, but there is an exception when _predecessorId is bytes32 0, an empty _predecessorId  is enough reason to revert the code instead the code goes through without reversion 
https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L240
```solidity
function _checkPredecessorDone(bytes32 _predecessorId) internal view {
        require(_predecessorId == bytes32(0) || isOperationDone(_predecessorId), "Predecessor operation not completed");
    }
```