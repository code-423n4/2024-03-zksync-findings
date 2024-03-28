# Lack of access control on initialize function [INFORMATIONAL]
The initialize function can be called multiple times, potentially allowing an attacker to change the owner of the contract.

POC:

Deploy the contract with an initial owner.
Call initialize again with a new address as the owner.

Impact:

```
    common/ReentrancyGuard.sol#L41C1-L44C6
    modifier reentrancyGuardInitializer() {
        _initializeReentrancyGuard();
        _;
    }
```

``` solidity
l1\Bridgehub.sol
37:     /// @notice to avoid parity hack
38:     constructor() reentrancyGuardInitializer {}
39: 
40:     /// @notice used to initialize the contract
41:     function initialize(address _owner) external reentrancyGuardInitializer {
42:         _transferOwnership(_owner);
43:     }
44: 
45:     modifier onlyOwnerOrAdmin() {
46:         require(msg.sender == admin || msg.sender == owner(), "Bridgehub: not owner or admin");
47:         _;
48:     }
49: 
```

Recommendation:

Implement a modifier to restrict the initialize function to be called only once.

Example:
``` solidity
modifier onlyInitializing {
    require(!initialized, "Contract is already initialized");
    _;
    initialized = true;
}

constructor() reentrancyGuardInitializer {
    __gap[0] = _gapStoragePos;
    initialized = false;
}

function initialize(address _owner) external onlyInitializing {
    _transferOwnership(_owner);
}
```


#  Lack of __gap Variable L1ERC20Bridge and L2StandardERC20 [INFORMATIONAL]

The L1ERC20Bridge and L2StandardERC20 contracts are intended to be used as logic contracts with a proxy, but they currently do not include a __gap variable. This could lead to storage collisions in future versions that inherit from one of these contracts. If a subsequent version has its own storage variable and additional storage variables are added to the inherited contract, a storage collision will occur.

To prevent this, we recommend adding a __gap storage variable as the last variable in these upgradable contracts, so that the total number of storage slots is fixed (for example, at [amount]gap). This will ensure that any changes to the storage layout of the base contract in the future do not affect the upgradable contracts. However, the __gap storage variable will need to be adjusted as new storage variables are added to future versions, in order to maintain the fixed number of storage slots (for example, [amount]gap). By following this practice, we can ensure that upgradable contracts remain functional and free from storage collisions, even as the underlying base contracts evolve.


# transferEthToSharedBridge has no check against maximum limits [INFORMATIONAL]

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L38

consider acceptable value, and no attempt at an acceptable amount of ETH.

Recommendation: Add a maximum acceptable value limit and add a mechanism for the acceptable amount of ETH.


# bridgehubRequestL2Transaction dan requestL2Transactiontidak checks the validity of _contractL2, so that an invalid contract can be accepted if Bridgehub or an external user sends a transaction request with an invalid contract. [INFORMATIONAL]

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L47
https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L197

Recommendation: Add _contractL2 validity check before committing the transaction dan checking the validity of contracts before executing transactions, invalid contracts can be prevented from being executed.


# _requestL2Transactiondan _writePriorityOpmenerima reference to _params, which can cause problems if _params is a reference to mutable data.[INFORMATIONAL]

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258

``` solidity
    // Copy _params to prevent modifications after sending to _writePriorityOp
    WritePriorityOpParams memory paramsCopy = _params;
```

Recommendation: Convert _params to a new immutable data type, so that the data cannot be changed once it is sent.

# lack of _proveL2LogInclusion do not perform checks on received parameters.  [INFORMATIONAL]
 
 https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L54C1-L71C6

 ``` audit
    function _proveL2LogInclusion(
        uint256 _batchNumber,
        uint256 _index,
        L2Log memory _log,
        bytes32[] calldata _proof
    ) internal view returns (bool) {
        require(_batchNumber <= s.totalBatchesExecuted, "xx");


        bytes32 hashedLog = keccak256(
            abi.encodePacked(_log.l2ShardId, _log.isService, _log.txNumberInBatch, _log.sender, _log.key, _log.value)
        );
        // Check that hashed log is not the default one,
        // otherwise it means that the value is out of range of sent L2 -> L1 logs
        require(hashedLog != L2_L1_LOGS_TREE_DEFAULT_LEAF_HASH, "tw");

@>      require(_proof.length > 0, "Proof cannot be empty");

        // It is ok to not check length of `_proof` array, as length
        // of leaf preimage (which is `L2_TO_L1_LOG_SERIALIZE_SIZE`) is not
        // equal to the length of other nodes preimages (which are `2 * 32`)


        bytes32 calculatedRootHash = Merkle.calculateRoot(_proof, _index, hashedLog);
        bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];
@>      require(actualRootHash == calculatedRootHash, "Invalid proof");  

        return actualRootHash == calculatedRootHash;
    }
```

recommendation : consider additional validation logs, non-empty proofs, and correct Merkle proofs according to the given root hash


# Missing input validation checks _pointEvaluationPrecompile

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L605

no check for the length of `_openingValueCommitmentProof` This could potentially lead to out-of-bounds array access and other related issues.

Recommendation:
require(_openingValueCommitmentProof.length == EXPECTED_LENGTH, "Invalid length of openingValueCommitmentProof");