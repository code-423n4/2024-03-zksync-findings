## [G-01] Refactoring requestL2TransactionDirect and requestL2TransactionTwoBridges in Bridgehub

**`requestL2TransactionDirect` and `requestL2TransactionTwoBridges`:**

These functions share common logic for interacting with the shared bridge and state transition manager. Consider refactoring them to extract the shared logic into a separate internal function to avoid code duplication and reduce gas costs.

Here's how you can refactor the `requestL2TransactionDirect` and `requestL2TransactionTwoBridges` functions in the `Bridgehub` contract to extract shared logic and reduce gas costs:

**1 - Create a new internal function:**

function _requestL2Transaction(
    uint256 _chainId,
    address _sender,
    address _l2Contract,
    uint256 _mintValue,
    uint256 _l2Value,
    bytes calldata _l2Calldata,
    uint256 _l2GasLimit,
    uint256 _l2GasPerPubdataByteLimit,
    bytes[] calldata _factoryDeps,
    address _refundRecipient
) internal returns (bytes32 canonicalTxHash) {
    address stateTransition = getStateTransition(_chainId);
    address refundRecipient = _actualRefundRecipient(_refundRecipient);

    canonicalTxHash = IZkSyncStateTransition(stateTransition).bridgehubRequestL2Transaction(
        BridgehubL2TransactionRequest({
            sender: _sender,
            contractL2: _l2Contract,
            mintValue: _mintValue,
            l2Value: _l2Value,
            l2Calldata: _l2Calldata,
            l2GasLimit: _l2GasLimit,
            l2GasPerPubdataByteLimit: _l2GasPerPubdataByteLimit,
            factoryDeps: _factoryDeps,
            refundRecipient: refundRecipient
        })
    );
}

This internal function encapsulates the common logic of interacting with the shared bridge and state transition manager. It takes all the necessary parameters and returns the canonical transaction hash.

**2 - Update `requestL2TransactionDirect`:**

function requestL2TransactionDirect(
    L2TransactionRequestDirect calldata _request
) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
    {
        address token = baseToken[_request.chainId];
        if (token == ETH_TOKEN_ADDRESS) {
            require(msg.value == _request.mintValue, "Bridgehub: msg.value mismatch 1");
        } else {
            require(msg.value == 0, "Bridgehub: non-eth bridge with msg.value");
        }

        sharedBridge.bridgehubDepositBaseToken{value: msg.value}(
            _request.chainId,
            msg.sender,
            token,
            _request.mintValue
        );
    }

    canonicalTxHash = _requestL2Transaction(
        _request.chainId,
        msg.sender,
        _request.l2Contract,
        _request.mintValue,
        _request.l2Value,
        _request.l2Calldata,
        _request.l2GasLimit,
        _request.l2GasPerPubdataByteLimit,
        _request.factoryDeps,
        _request.refundRecipient
    );
}

The `requestL2TransactionDirect` function now only handles the specific logic related to depositing base tokens and then calls the `_requestL2Transaction` internal function with the appropriate parameters.

**3 - Update requestL2TransactionTwoBridges:**

function requestL2TransactionTwoBridges(
    L2TransactionRequestTwoBridgesOuter calldata _request
) external payable override nonReentrant returns (bytes32 canonicalTxHash) {
    {
        address token = baseToken[_request.chainId];
        uint256 baseTokenMsgValue;
        if (token == ETH_TOKEN_ADDRESS) {
            require(
                msg.value == _request.mintValue + _request.secondBridgeValue,
                "Bridgehub: msg.value mismatch 2"
            );
            baseTokenMsgValue = _request.mintValue;
        } else {
            require(msg.value == _request.secondBridgeValue, "Bridgehub: msg.value mismatch 3");
            baseTokenMsgValue = 0;
        }
        sharedBridge.bridgehubDepositBaseToken{value: baseTokenMsgValue}(
            _request.chainId,
            msg.sender,
            token,
            _request.mintValue
        );
    }

    L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)
        .bridgehubDeposit{value: _request.secondBridgeValue}(
        _request.chainId,
        msg.sender,
        _request.l2Value,
        _request.secondBridgeCalldata
    );

    require(outputRequest.magicValue == TWO_BRIDGES_MAGIC_VALUE, "Bridgehub: magic value mismatch");

    require(
        _request.secondBridgeAddress > BRIDGEHUB_MIN_SECOND_BRIDGE_ADDRESS,
        "Bridgehub: second bridge address too low"
    ); // to avoid calls to precompiles

    canonicalTxHash = _requestL2Transaction(
        _request.chainId,
        _request.secondBridgeAddress,
        outputRequest.l2Contract,
        _request.mintValue,
        _request.l2Value,
        outputRequest.l2Calldata,
        _request.l2GasLimit,
        _request.l2GasPerPubdataByteLimit,
        outputRequest.factoryDeps,
        _request.refundRecipient
    );

    IL1SharedBridge(_request.secondBridgeAddress).bridgehubConfirmL2Transaction(
        _request.chainId,
        outputRequest.txDataHash,
        canonicalTxHash
    );
}

Similarly, the `requestL2TransactionTwoBridges` function now handles the specific logic related to the second bridge interaction and then calls the `_requestL2Transaction` internal function with the appropriate parameters.

By extracting the shared logic into `_requestL2Transaction`, you avoid code duplication and reduce gas costs associated with redundant checks and function calls. This can improve the overall efficiency and maintainability of the `Bridgehub` contract.

## [G-02] Inlining _checkPredecessorDone in Governance Contract

**`_checkPredecessorDone`:**

This function is called within `execute` and `executeInstant`. Consider moving the check directly into those functions to avoid the overhead of an additional internal function call.

Here's how you can inline the `_checkPredecessorDone` function within the `execute` and `executeInstant` functions in the `Governance` contract to avoid the overhead of an additional internal function call:

**1 - Update execute function:**

function execute(Operation calldata _operation) external payable onlyOwnerOrSecurityCouncil {
    bytes32 id = hashOperation(_operation);

    require(_operation.predecessor == bytes32(0) || isOperationDone(_operation.predecessor), "Predecessor operation not completed");

    require(isOperationReady(id), "Operation must be ready before execution");

    _execute(_operation.calls);

    require(isOperationReady(id), "Operation must be ready after execution");

    timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
    emit OperationExecuted(id);
}

**2 - Update executeInstant function:**

function executeInstant(Operation calldata _operation) external payable onlySecurityCouncil {
    bytes32 id = hashOperation(_operation);

    require(_operation.predecessor == bytes32(0) || isOperationDone(_operation.predecessor), "Predecessor operation not completed");

    require(isOperationPending(id), "Operation must be pending before execution");

    _execute(_operation.calls);

    require(isOperationPending(id), "Operation must be pending after execution");

    timestamps[id] = EXECUTED_PROPOSAL_TIMESTAMP;
    emit OperationExecuted(id);
}

By directly incorporating the predecessor check within these functions, you eliminate the need for a separate function call, which can save gas, especially if these functions are called frequently.

## [G-03] Inlining getCommittedBatchTimestamp in ValidatorTimelock Contract

**`getCommittedBatchTimestamp`:**

This function is called within loops in `executeBatches` and `executeBatchesSharedBridge`. Consider directly accessing the `committedBatchTimestamp` mapping within those loops instead of calling this function repeatedly. This can save gas by avoiding function call overhead.

Here's how you can directly access the `committedBatchTimestamp` mapping within the `executeBatches` and `executeBatchesSharedBridge` functions to avoid the overhead of calling `getCommittedBatchTimestamp` repeatedly:

**1 - Update executeBatches function:**

function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
    uint256 delay = executionDelay; // uint32
    unchecked {
        for (uint256 i = 0; i < _newBatchesData.length; ++i) {
            // Directly access committedBatchTimestamp instead of calling getCommittedBatchTimestamp
            uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(_newBatchesData[i].batchNumber);

            // Note: if the `commitBatchTimestamp` is zero, that means either:
            // * The batch was committed, but not through this contract.
            // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
            // We allow executing such batches.

            require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
        }
    }
    _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
}

**2 - Update executeBatchesSharedBridge function:**

function executeBatchesSharedBridge(
    uint256 _chainId,
    StoredBatchInfo[] calldata _newBatchesData
) external onlyValidator(_chainId) {
    uint256 delay = executionDelay; // uint32
    unchecked {
        for (uint256 i = 0; i < _newBatchesData.length; ++i) {
            // Directly access committedBatchTimestamp instead of calling getCommittedBatchTimestamp
            uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);

            // Note: if the `commitBatchTimestamp` is zero, that means either:
            // * The batch was committed, but not through this contract.
            // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
            // We allow executing such batches.

            require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
        }
    }
    _propagateToZkSyncStateTransition(_chainId);
}

By directly accessing the mapping within the loop, you avoid the overhead of calling the `getCommittedBatchTimestamp` function repeatedly, which can save gas, especially when processing multiple batches.

## [G-04] Refactoring commitBatches and commitBatchesSharedBridge in ValidatorTimelock

**`commitBatches` and `commitBatchesSharedBridge`:**

These functions share common logic for recording timestamps and calling `_propagateToZkSyncStateTransition`. Consider refactoring them to extract the shared logic into a separate internal function to avoid code duplication and reduce gas costs.

Here's how you can refactor the `commitBatches` and `commitBatchesSharedBridge` functions in the `ValidatorTimelock` contract to extract shared logic and reduce gas costs:

**1 - Create a new internal function:**

function _commitBatchesInternal(
    uint256 _chainId,
    StoredBatchInfo calldata _lastCommittedBatchData,
    CommitBatchInfo[] calldata _newBatchesData
) internal {
    unchecked {
        // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
        // It is safe to cast.
        uint32 timestamp = uint32(block.timestamp);
        for (uint256 i = 0; i < _newBatchesData.length; ++i) {
            committedBatchTimestamp[_chainId].set(_newBatchesData[i].batchNumber, timestamp);
        }
    }

    _propagateToZkSyncStateTransition(_chainId);
}

This internal function encapsulates the common logic of recording timestamps for committed batches and calling `_propagateToZkSyncStateTransition`. It takes the `chain ID`, last committed batch data, and new batches data as parameters.

**2 - Update commitBatches function:**

function commitBatches(
    StoredBatchInfo calldata _lastCommittedBatchData,
    CommitBatchInfo[] calldata _newBatchesData
) external onlyValidator(ERA_CHAIN_ID) {
    // Call the internal function with the chain ID and other parameters
    _commitBatchesInternal(ERA_CHAIN_ID, _lastCommittedBatchData, _newBatchesData);
}

## [G-05] Optimizing _encodeBlobAuxilaryOutput in ExecutorFacet

**_encodeBlobAuxilaryOutput:**

The function initializes an array of 32 `bytes32` values, but only uses the first two elements. Consider initializing a smaller array to avoid unnecessary memory allocation.
































