## \[G-01\]. Optimize Gas usage by removing duplicate Require Statements.

[https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L55-L58](//l2sharedBridge.sol)

```solidity
function initialize(
        address _l1Bridge,
        address _l1LegecyBridge,
        bytes32 _l2TokenProxyBytecodeHash,
        address _aliasedOwner
    ) external reinitializer(2) {
        require(_l1Bridge != address(0), "bf");
        require(_l2TokenProxyBytecodeHash != bytes32(0), "df");   
        require(_aliasedOwner != address(0), "sf");
        require(_l2TokenProxyBytecodeHash != bytes32(0), "df"); 

        l1Bridge = _l1Bridge;
        l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;

        if (block.chainid != ERA_CHAIN_ID) {
            address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
            l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
            l2TokenBeacon.transferOwnership(_aliasedOwner);
        } else {
            require(_l1LegecyBridge != address(0), "bf2");
            // l2StandardToken and l2TokenBeacon are already deployed on ERA, and stored in the proxy
        }
    }
```

**Description:-** In the \`initialize\` function, there are two identical \`require\` statements checking the \`_l2TokenProxyBytecodeHash\` parameter for non-zero values. These duplicate checks can lead to unnecessary gas consumption, as the same condition is verified twice within the function.

**Mitigation Step:-** Remove Redundant Require statement \`_l2TokenProxyBytecodeHash\` to enhance gas efficiency without compromising the function's integrity.

```solidity
function initialize(
        address _l1Bridge,
        address _l1LegecyBridge,
        bytes32 _l2TokenProxyBytecodeHash,
        address _aliasedOwner
    ) external reinitializer(2) {
        require(_l1Bridge != address(0), "bf");
        require(_l2TokenProxyBytecodeHash != bytes32(0), "df");   
        require(_aliasedOwner != address(0), "sf");
       -- require(_l2TokenProxyBytecodeHash != bytes32(0), "df"); 

        l1Bridge = _l1Bridge;
        l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;
```

## \[G-02\] Unnecessary variable in `systemContractCaller.sol`

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractsCaller.sol#L76-L114

**Description:-** Variable `callAddr` ,    `msgValueSimulator`  ,`forwardMask`  are local variable which access state constant variable and some of them are used only once which means it doesn’t need to be declared at all. The code snippet below can be changed from:

**From:**

```solidity
function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {
        //this variable need to be delete and instead constant variable directly use
        address callAddr = SYSTEM_CALL_CALL_ADDRESS;
        
        uint32 dataStart;
        assembly {
            dataStart := add(data, 0x20)
        }
        uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

        uint256 farCallAbi = getFarCallABI(
            0,
            0,
            dataStart,
            dataLength,
            gasLimit,
            // Only rollup is supported for now
            0,
            CalldataForwardingMode.UseHeap,
            false,
            true
        );

        if (value == 0) {
            // Doing the system call directly
            assembly {
                success := call(to, callAddr, 0, 0, farCallAbi, 0, 0)
            }
        } else {
        //this variable need to be delete and instead constant variable directly use
            address msgValueSimulator = MSG_VALUE_SYSTEM_CONTRACT;
            // We need to supply the mask to the MsgValueSimulator to denote
            // that the call should be a system one.
            //this variable need to be delete and instead constant variable directly use
            uint256 forwardMask = MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT;

            assembly {
                success := call(msgValueSimulator, callAddr, value, to, farCallAbi, forwardMask, 0)
            }
        }
```

**To:**

```solidity
function systemCall(uint32 gasLimit, address to, uint256 value, bytes memory data) internal returns (bool success) {

        uint32 dataStart;
        assembly {
            dataStart := add(data, 0x20)
        }
        uint32 dataLength = uint32(Utils.safeCastToU32(data.length));

        uint256 farCallAbi = getFarCallABI(
            0,
            0,
            dataStart,
            dataLength,
            gasLimit,
            // Only rollup is supported for now
            0,
            CalldataForwardingMode.UseHeap,
            false,
            true
        );

        if (value == 0) {
            // Doing the system call directly
            assembly {
                success := call(to, SYSTEM_CALL_CALL_ADDRESS, 0, 0, farCallAbi, 0, 0)
            }
        } else {
            assembly {
                success := call(MSG_VALUE_SYSTEM_CONTRACT, SYSTEM_CALL_CALL_ADDRESS, value, to, farCallAbi, 
                MSG_VALUE_SIMULATOR_IS_SYSTEM_BIT, 0)
            }
        }
    }
```

## \[G-03\] Caching the length of calldata increases gas cost instead of reducing it.

## `ContractDeployer.sol`

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L244

**From:**

```solidity
function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
        require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        );

        uint256 deploymentsLength = _deployments.length;
        // We need to ensure that the `value` provided by the call is enough to provide `value`
        // for all of the deployments
        uint256 sumOfValues = 0;
        for (uint256 i = 0; i < deploymentsLength; ++i) {
            sumOfValues += _deployments[i].value;
        }
        require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

        for (uint256 i = 0; i < deploymentsLength; ++i) {
            this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
        }
    }
```

**To:**

```solidity
function forceDeployOnAddresses(ForceDeployment[] calldata _deployments) external payable {
        require(
            msg.sender == FORCE_DEPLOYER || msg.sender == address(COMPLEX_UPGRADER_CONTRACT),
            "Can only be called by FORCE_DEPLOYER or COMPLEX_UPGRADER_CONTRACT"
        );

      --uint256 deploymentsLength = _deployments.length;
        // We need to ensure that the `value` provided by the call is enough to provide `value`
        // for all of the deployments
        uint256 sumOfValues = 0;
     --for (uint256 i = 0; i < deploymentsLength; ++i) {
     ++for (uint256 i = 0; i < _deployments.length; ++i) {
        
            sumOfValues += _deployments[i].value;
        }
        require(msg.value == sumOfValues, "`value` provided is not equal to the combined `value`s of deployments");

      --for (uint256 i = 0; i < deploymentsLength; ++i) {
      ++for (uint256 i = 0; i < _deployments.length; ++i) {
            this.forceDeployOnAddress{value: _deployments[i].value}(_deployments[i], msg.sender);
        }
}
```

## Contract :- `ImmutableSimmulator.sol`

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ImmutableSimulator.sol#L37

**from:-**

```solidity
function setImmutables(address _dest, ImmutableData[] calldata _immutables) external override {
        require(msg.sender == address(DEPLOYER_SYSTEM_CONTRACT), "Callable only by the deployer system contract");
        unchecked {
            uint256 immutablesLength = _immutables.length;
            for (uint256 i = 0; i < immutablesLength; ++i) {
                uint256 index = _immutables[i].index;
                bytes32 value = _immutables[i].value;
                immutableDataStorage[uint256(uint160(_dest))][index] = value;
            }
        }
    }
```

**To:-**

```solidity
//--uint256 immutablesLength = _immutables.length;
        //--for (uint256 i = 0; i < immutablesLength; ++i) {
          ++for (uint256 i = 0; i < _immutables.length; ++i) {
                uint256 index = _immutables[i].index;
                bytes32 value = _immutables[i].value;
                immutableDataStorage[uint256(uint160(_dest))][index] = value;
            }
```

## Contract :- `KnownCodesStorage.sol`

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/KnownCodesStorage.sol#L29

**From:-**

```solidity
function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {
        unchecked {
            uint256 hashesLen = _hashes.length;
            for (uint256 i = 0; i < hashesLen; ++i) {
                _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);
            }
        }
    }
```

**To:-**

```solidity
function markFactoryDeps(bool _shouldSendToL1, bytes32[] calldata _hashes) external onlyCallFromBootloader {
        unchecked {
            //--uint256 hashesLen = _hashes.length;
            //--for (uint256 i = 0; i < hashesLen; ++i) {
           ++ for (uint256 i = 0; i < _hashes.length; ++i) {
                _markBytecodeAsPublished(_hashes[i], _shouldSendToL1);
            }
        }
    }
```

## \[G-04\] Unnecessary variables in `ContractDeployer.sol`

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L302

Variable `version` is used only once, which means, it doesn’t need to be declared at all. The code snippet below can be changed from:

```solidity
function _ensureBytecodeIsKnown(bytes32 _bytecodeHash) internal view {
        uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);
        require(knownCodeMarker > 0, "The code hash is not known");
    }
```

### To:

```solidity
function _ensureBytecodeIsKnown(bytes32 _bytecodeHash) internal view {
      //--uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);
        require(KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash) > 0, "The code hash is not known");
    }
```

**Function** `_storeConstructingByteCodeHashOnAddress`

**From:-**

```solidity
function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {
        // Set the "isConstructor" flag to the bytecode hash
        bytes32 constructingBytecodeHash = Utils.constructingBytecodeHash(_bytecodeHash);
        ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructingCodeHash(_newAddress, constructingBytecodeHash);
    }
```

**To:-**

```solidity
function _storeConstructingByteCodeHashOnAddress(address _newAddress, bytes32 _bytecodeHash) internal {
        // Set the "isConstructor" flag to the bytecode hash
        // --  bytes32 constructingBytecodeHash = Utils.constructingBytecodeHash(_bytecodeHash);
        ACCOUNT_CODE_STORAGE_SYSTEM_CONTRACT.storeAccountConstructingCodeHash(_newAddress, Utils.constructingBytecodeHash(_bytecodeHash));
    }
```

**Function:- `getNewAddressCreate2`**

**From:-**

```solidity
function getNewAddressCreate2(
        address _sender,
        bytes32 _bytecodeHash,
        bytes32 _salt,
        bytes calldata _input
    ) public view override returns (address newAddress) {
        // No collision is possible with the Ethereum's CREATE2, since
        // the prefix begins with 0x20....
        bytes32 constructorInputHash = EfficientCall.keccak(_input);

        bytes32 hash = keccak256(
            bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
        );

        newAddress = address(uint160(uint256(hash)));
    }
```

**To:-**

```solidity
// -- bytes32 constructorInputHash = EfficientCall.keccak(_input);

        bytes32 hash = keccak256(
     //      -- bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, constructorInputHash)
           ++ bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, EfficientCall.keccak(_input))
        );

        newAddress = address(uint160(uint256(hash)));
    }
```

## \[G-05\] Unnecessary variables in `DefaultAccount.sol`

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L99-L100

Variable `totalRequiredBalance` is used only once, which means, it doesn’t need to be declared at all. The code snippet below can be changed from:

### **from:-**

```solidity
uint256 totalRequiredBalance = _transaction.totalRequiredBalance();
        require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
```

**To:-**

```solidity
require(_transaction.totalRequiredBalance() <= address(this).balance, "Not enough balance for fee + value");
```

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L201-L202

**from:-**

```solidity
bool success = _transaction.payToTheBootloader();

 require(success,  "Failed to pay the fee to the operator");
```

**To:-**

```solidity
// -- bool success = _transaction.payToTheBootloader();

 require(_transaction.payToTheBootloader(),  "Failed to pay the fee to the operator");
```

## \[G-06\] Refactor the function to save gas.

**Description:- Avoid from assigning the old value into new variable and directly emit the events with old value and then update the variables.**

**https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L126-L138**

**From:-**

```solidity
function _setVerifier(IVerifier _newVerifier) private {
        // An upgrade to the verifier must be done carefully to ensure there aren't batches in the committed state
        // during the transition. If verifier is upgraded, it will immediately be used to prove all committed batches.
        // Batches committed expecting the old verifier will fail. Ensure all commited batches are finalized before the
        // verifier is upgraded.
        if (_newVerifier == IVerifier(address(0))) {
            return;
        }

        IVerifier oldVerifier = s.verifier;
        s.verifier = _newVerifier;
        emit NewVerifier(address(oldVerifier), address(_newVerifier));
    }
```

**To:-**

```solidity
function _setVerifier(IVerifier _newVerifier) private {
        if (_newVerifier == IVerifier(address(0))) {
            return;
        }
        ++ emit NewVerifier(address(oldVerifier), address(_newVerifier));
        // -- IVerifier oldVerifier = s.verifier;
        s.verifier = _newVerifier;
        // -- emit NewVerifier(address(oldVerifier), address(_newVerifier));
    }
```

### https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L155-L157

**From:-**

```solidity
VerifierParams memory oldVerifierParams = s.verifierParams;
    s.verifierParams = _newVerifierParams;
    emit NewVerifierParams(oldVerifierParams, _newVerifierParams);
```

**To:-**

```solidity
// -- VerifierParams memory oldVerifierParams = s.verifierParams;
    ++ emit NewVerifierParams(oldVerifierParams, _newVerifierParams);
    s.verifierParams = _newVerifierParams;
    // -- emit NewVerifierParams(oldVerifierParams, _newVerifierParams);
```

### \[G-07\] Move lesser gas costing require checks to the top.

**Description:- Require() statements that check input arguments or cost lesser gas should be at the top of the function. Check that involve constants should come before checks that involve stat variables, function calls and calculations**

https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L83-L85

**From:-**

```solidity
function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
        IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);

        require(_value != 0, "Nonce value cannot be set to 0");
        // If an account has sequential nonce ordering, we enforce that the previous
        // nonce has already been used.
        if (accountInfo.nonceOrdering == IContractDeployer.AccountNonceOrdering.Sequential && _key != 0) {
            require(isNonceUsed(msg.sender, _key - 1), "Previous nonce has not been used");
        }

        uint256 addressAsKey = uint256(uint160(msg.sender));

        nonceValues[addressAsKey][_key] = _value;

        emit ValueSetUnderNonce(msg.sender, _key, _value);
    }
```

**To:-**

```solidity
function setValueUnderNonce(uint256 _key, uint256 _value) public onlySystemCall {
        ++ require(_value != 0, "Nonce value cannot be set to 0");
        
        IContractDeployer.AccountInfo memory accountInfo = DEPLOYER_SYSTEM_CONTRACT.getAccountInfo(msg.sender);

        // -- require(_value != 0, "Nonce value cannot be set to 0");
        // If an account has sequential nonce ordering, we enforce that the previous
        // nonce has already been used.
```