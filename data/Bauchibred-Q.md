# QA Report



<details>
  <summary>DISCLAIMER</summary>

---

While we've tried our best to maintain readability for brevity and focus, we have selectively truncated the code snippets to spotlight relevant sections. Certain excerpts may be abbreviated, and some references are provided via search commands due to the extensive nature of the project and time constraints

---

As a request to the judge: In order to not spam the judging repo, we've attached some findings here that are subjective in their nature of being borderline medium/low findings, we've hinted these instances in the reports, so if the judge sees it fit we'd be especting upgrades of these findings.

---

Finally, it's important to mention that a previous audit conducted [a few months back by Code4rena](https://github.com/code-423n4/2023-10-zksync) on an [older commit](https://github.com/code-423n4/2024-03-zksync/compare/2023-10-zksync...main) of the contracts in scope, this contest had a bot race and as such yielded a [bot report](https://raw.githubusercontent.com/code-423n4/2023-10-zksync/main/bot-report.md) with multiple QA suggestions, the report had over `4000` instances of QA report (both `L's` & `NC's`). Our quick review on some of these findings from the bot, revealed that only few of thosse suggestions have been acted upon. We recommend that, alongside this report, the team also revisits the [bot report](https://raw.githubusercontent.com/code-423n4/2023-10-zksync/main/bot-report.md) to explore further QA suggestions to improve code structure, this is cause we've deliberately tried our best in not duplicating points from that previous analysis in this report.

---

</details>


## Table of Contents

| Issue ID | Description |
| -------- | ----------- |
| [QA-01](#qa-01-a-chain-that-gets-frozen-by-the-state-transition-manager-can-never-be-removed-from-the-frozen-state-in-statetransitionmanager.sol) | A chain that gets frozen by the state transition manager can never be removed from the frozen state in `StateTransitionManager.sol` |
| [QA-02](#qa-02-genesis-upgrades-currently-do-not-fully-work-as-intended) | Genesis upgrades, currently do not fully work as intended |
| [QA-03](#qa-03-bootloader-wrongly-identifies-the-right_padded_get_account_version_selector-as-not-attached-with-the-contract-deployer-deployment-execution) | Bootloader wrongly identifies the `RIGHT_PADDED_GET_ACCOUNT_VERSION_SELECTOR` as not attached with the `Contract Deployer` deployment execution |
| [QA-04](#qa-04-the-new-require(dictionary.length-/-8-<=-encodeddata.length-/-2)-check-allows-malicious-operators-to-always-pass-in-malformed-data-to-the-bootloader-to-ensure-that-all-users-gas-gets-burnt-without-executing-the-tx.) | The new `require(dictionary.length / 8 <= encodedData.length / 2)` check allows malicious operators to always pass in malformed data to the bootloader to ensure that all users gas gets burnt without executing the tx. |
| [QA-05](#qa-05-users-tokens-could-get-lost-indefinitely) | Users tokens could get lost indefinitely |
| [QA-06](#qa-06-a-large-amount-withdrawal-could-break-the-minting-logic-of-l2basetoken-effectively-causing-attempts-of-consequent-mints-to-fail) | A large amount withdrawal could break the minting logic of `L2BaseToken` effectively causing attempts of consequent mints to fail |
| [QA-07](#qa-07-fix-typos-&-documentations-_(multiple-instances)_) | Fix typos & documentations _(Multiple instances)_ |
| [QA-08](#qa-08-there-are-currently-no-assurances-that-funds-specified-for-operation-are-rightly-matched) | There are currently no assurances that funds specified for operation are rightly matched |
| [QA-09](#qa-09-protocol-is-susceptible-to-synchronizing-issues-cause-reverted-system-contract-upgrade-batches-must-stiill-be-commited-between-l1-and-l2-upgrades-due-to-wrongly-asuming-just-reverting-in-the-bootloader-is-enough) | Protocol is susceptible to synchronizing issues cause reverted system contract upgrade batches must stiill be commited between L1 and L2 upgrades due to wrongly asuming just reverting in the bootloader is enough |
| [QA-](#qa--10-shadow-upgrades-would-currently-have-their-executional-data-leaked-if-they-fail) | 10 Shadow upgrades would currently have their executional data leaked if they fail |
| [QA-11](#qa-11-fix-bugs-present-in-the-precomcompiles-or-clearly-document-the-bugs-for-users/developers) | Fix bugs present in the precomcompiles or clearly document the bugs for users/developers |
| [QA-12](#qa-12-consider-renaming-current_max_precompile_address-to-max_possible_precompile_address) | Consider renaming `CURRENT_MAX_PRECOMPILE_ADDRESS` to `MAX_POSSIBLE_PRECOMPILE_ADDRESS` |
| [QA-13](#qa-13-users-funds-could-still-be-stuck-due-to-lack-of-access-to-eth-on-the-l2-through-l1->l2-transactions-so-this-should-be-clearly-documented) | Users funds could still be stuck due to lack of access to `ETH` on the `L2` through `L1->L2 `transactions so this should be clearly documented |
| [QA-14](#qa-14-if-the-pending-admin-becomes-malicious-there-is-no-specific-way-to-stop-them-from-accepting-the-admin) | If the pending admin becomes malicious there is no specific way to stop them from accepting the admin |
| [QA-15](#qa-15-protocol-does-not-consider-eip-4844-and-still-assumes-more-than-one-batch-can-be-commited) | Protocol does not consider EIP-4844 and still assumes more than one batch can be commited |
| [QA-16](#qa-16-missing-getter-functions-for-key-internal-zksyncstatetransitionstorage-variables-should-be-introduced) | Missing getter functions for key internal `ZkSyncStateTransitionStorage` variables should be introduced |
| [QA-17](#qa-17-upgrades-are-automatically-immediately-possible-instead-of-being-able-to-have-a-kick-in-time-in-the-future) | upgrades are automatically immediately possible instead of being able to have a kick in time in the future |
| [QA-18](#qa-18-the-placeholder-_postupgrade()-has-no-implementation-and-is-not-meant-to-be-used-but-is-being-queried-twice-via-both-the-genesis-and-normal-upgrade-pattern) | The placeholder `_postUpgrade()` has no implementation and is not meant to be used but is being queried twice via both the genesis and normal upgrade pattern |
| [QA-19](#qa-19-new-instances-of-missing-natspec-comments) | New instances of missing natspec comments |
| [QA-20](#qa-20-setters-do-not-have-equality/zero-checkers) | Setters do not have `equality/zero` checkers |
| [QA-21](#qa-21-multiple-instances-of-where-messages-within-require-are-not-descriptive) | Multiple instances of where messages within `require` are not descriptive |
| [QA-22](#qa-22-deviation-from-solidity-best-styling-practices-in-scoped-contracts) | Deviation from Solidity best styling practices in scoped contracts |
| [QA-23](#qa-23-remove-unnecessary-code-irrelevant-to-final-production) | Remove unnecessary code irrelevant to final production |
| [QA-24](#qa-24-alpha-period-code-is-still-in-production-despite-the-period-ending-in-april-2023) | Alpha period code is still in production despite the period ending in April 2023 |
| [QA-25](#qa-25-redeployment-considerations-for-l2contracthelper/config.sol-in-case-of-updates) | Redeployment considerations for `L2ContractHelper/Config.sol` in case of updates |
| [QA-26](#qa-26-l1sharedbridge.solmight-encounter-accounting-errors) | `L1SharedBridge.sol`might encounter accounting errors |
| [QA-27](#qa-27-the-ecrecover-gas-cost-been-massively-increased-without-significant-increases-in-executional-cost) | The `Ecrecover` gas cost been massively increased without significant increases in executional cost |
| [QA-28](#qa-28-zkevms-codeoracle-precompile-somewhat-deviates-from-evms-extcodecopy-behavior) | zkEVM's `CodeOracle` Precompile somewhat deviates from EVM's `extcodecopy` behavior |
| [QA-29](#qa-29-protocol-currently-does-not-consider-all-windows-in-regards-to-mindelay) | Protocol currently does not consider all windows in regards to `minDelay` |
| [QA-30](#qa-30-basezksyncupgradegenesis_setnewprotocolversion()-should-not-allow-the-protocol-version-difference-to-be-up-to-max_allowed_protocol_version_delta) | `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion()` should not allow the protocol version difference to be up to `MAX_ALLOWED_PROTOCOL_VERSION_DELTA` |
| [QA-31](#qa-31-users-failed-tx-could-be-unclaimable-from-the-shared-bridge) | Users failed tx could be unclaimable from the shared bridge |
| [QA-32](#qa-32-apply-fixes-to-commented-out-bug-cases) | Apply fixes to commented out bug cases |
| [QA-33](#qa-33-unnecessary-duplication-of-checks) | Unnecessary duplication of checks |
| [QA-34](#qa-34-non-existent-facets-would-be-assumed-to-be-unfreezable-due-to-the-wrong-conditional-keyword-in-isfacetfreezable()) | Non-existent facets would be assumed to be unfreezable due to the wrong conditional keyword in `isFacetFreezable()` |
| [QA-35](#qa-35-remove-the-trailing-comma-after-queries-to-isnotenoughgasforpubdata-in-the-bootloader-to-enforce-no-error-in-the-yul-syntax) | Remove the trailing comma after queries to `isNotEnoughGasForPubdata` in the bootloader to enforce no error in the Yul Syntax |
| [QA-36](#qa-36-consider-rightly-passing-the-elements-of-the-bridgehubl2transactionrequest-in-_requestl2transaction()) | Consider rightly passing the elements of the `BridgehubL2TransactionRequest` in `_requestL2Transaction()` |
| [QA-37](#qa-37-resolve-newly-introduced-todos) | Resolve newly introduced TODOs |
| [##](###-qa-38--operationstate.waiting-should-be-considered-the-case-even-when-timestamp-==-block.timestamp) | QA-38  `OperationState.Waiting` should be considered the case even when `timestamp == block.timestamp` |
| [QA-39](#qa-39-redundant-return-of-the-nonce-deployed) | Redundant return of the nonce deployed |
| [QA-40](#qa-40-chunking-the-pubdata-should-be-made-more-efficient) | Chunking the pubdata should be made more efficient |
| [QA-41](#qa-41-owner-can-still-access-renounceownership()) | Owner can still access `renounceOwnership()` |
| [QA-42](#qa-42-there-exist-a-light-deviation-between-the-ethereum-vm-and-zks-in-regards-to-eth-deposits) | There exist a light deviation between the Ethereum VM and zK's in regards to eth deposits |
| [QA-43](#qa-43-0.8.20-is-vulnerable-to-some-bugs-and-compiler-version-should-be-updated-to-be-on-the-safe-side) | `0.8.20` is vulnerable to some bugs and compiler version should be updated to be on the safe side |
| [QA-44](#qa-44-execute()-&-executeinstant()-could-use-msg.value-in-a-better-manner) | `execute()` & `executeInstant()` could use `msg.value` in a better manner |
| [QA-45](#qa-45-statetransitionmanager.solcreatenewchain()-has-some-nuances-with-its-initdata) | `StateTransitionManager.sol::createNewChain()` has some nuances with it's `initData` |
| [QA-46](#qa-46-double-addressed-tokens-can-be-stolen-from-the-bridge) | Double addressed tokens can be stolen from the bridge |
| [QA-47](#qa-47-fix-bootloaders-documentation-in-regards-to-unread-memory-points) | Fix bootloader's documentation in regards to unread memory points |
| [QA-48](#qa-48-protocol-should-consider-supporting-deposits-of-pure-erc20s) | Protocol should consider supporting deposits of pure erc20s |
| [QA-49](#qa-49-remove-instances-of-unnecessary-casting) | Remove instances of unnecessary casting |
| [QA-50](#qa-50-always-update-comments-in-code-if-its-already-the-deadline) | Always update comments in code if it's already the deadline |
| [QA-51](#qa-51-fix-documentation-in-regards-to-timing-requirements-so-code-doesnt-deviate-from-docs) | Fix documentation in regards to timing requirements so code doesn't deviate from docs |
| [QA-52](#qa-52-airdrops-are-automatically-lost-for-the-l1erc20bridge) | Airdrops are automatically lost for the L1ERC20Bridge |
| [QA-53](#qa-53-transactionhelperisethtoken()-is-not-used-anywhere-so-it-should-be-removed) | `TransactionHelper::isEthToken()` is not used anywhere, so it should be removed |
| [QA-54](#qa-54-the-storedbatchhash()-fails-to-distinguish-between-reverted-and-unreverted-batches) | The` storedBatchHash()` fails to distinguish between reverted and unreverted batches |
| [QA-55](#qa-55-users-would-assume-proof-verification-is-performed-twice-in-provebatches()-due-to-a-wrongly-commenting-out-the-else-keyword-and-lack-of-documentation) | Users would assume proof verification is performed twice in `proveBatches()` due to a wrongly commenting out the `else` keyword and lack of documentation |
| [QA-56](#qa-56-wrong-error-message-in-basezksyncupgradegenesis_setnewprotocolversion) | Wrong error message in `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion` |

## QA-01 A chain that gets frozen by the state transition manager can never be removed from the frozen state in `StateTransitionManager.sol`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L159-L163

```solidity
    function freezeChain(uint256 _chainId) external onlyOwner {
        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
    }

```

This is a special function used by the admin to freeze a specific chain Id, this would come in handy in different context and is placed as a safe measure to help ensure the chain could be frozen to be safe.

Now protocol, logic also includes an unfreezing functionality, but this has been wrongly implemented, see https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L164-L168

```solidity
    function unfreezeChain(uint256 _chainId) external onlyOwner {
        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
    }

```

It's evident that where as this function is meant to be used for "unfreezing" the specified chain, it insteads attempt to call `freezeDiamond()`, now this means that an attempt to call on `unfreezeChain()` by the owner of the `StateTransitionManager.sol` contract would always revert since while `freezeDiamond()` is being executed it checks if the chain Id is frozen already and if yes it reverts (`require(!diamondStorage.isFrozen, "a9");`), see https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L133-L150

```solidity
    function freezeDiamond() external onlyAdminOrStateTransitionManager {
        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();

        require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already
        diamondStorage.isFrozen = true;

        emit Freeze();
    }

    /// @inheritdoc IAdmin
    function unfreezeDiamond() external onlyAdminOrStateTransitionManager {
        Diamond.DiamondStorage storage diamondStorage = Diamond.getDiamondStorage();

        require(diamondStorage.isFrozen, "a7"); // diamond proxy is not frozen
        diamondStorage.isFrozen = false;

        emit Unfreeze();
    }
```

Evidently, this bug is probably due to a copy paste error (i.e copying the implementation of `freezeChain()` for `unfreezeChain()` ), as we can see that the dev comment is the same in both instances of _freezing the chain_.

### Impact

Whereas the owner/admin can currently freeze a specified chain, the logic of unfreezing these chains is flawed and as such any chain that gets frozen can't get unfrozen by the state transition Manager.

> This was submitted as a QA, cause even though this is a break in important functinoality, if we navigate to [these instances](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L133-L150) in `Admin.sol` we can see that having the `onlyAdminOrStateTransitionManager` on the `unfreeze()` function means that whenver the chain id gets frozen and the state transition manager can't unfreeze it, [the admin](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L130) can just directly call `Admin::freezeDiamond()` since the modifier allows it

### Recommended Mitigation Steps

Consider applying these changes to https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L164-L168

```diff
-    /// @dev freezes the specified chain
+    /// @dev unfreezes the specified chain
    function unfreezeChain(uint256 _chainId) external onlyOwner {
-        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
+        IZkSyncStateTransition(stateTransition[_chainId]).unfreezeDiamond();
    }

```

## QA-02 Genesis upgrades, currently do not fully work as intended

### Proof of Concept

Based on documentations on how genesis upgrades should work, the transaction is to return the hash of the L2 system contract upgrade transaction after it's execution.

Now, take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L46-L68

```solidity

    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
        // Note that due to commitment delay, the timestamp of the L2 upgrade batch may be earlier than the timestamp
        // of the L1 block at which the upgrade occurred. This means that using timestamp as a signifier of "upgraded"
        // on the L2 side would be inaccurate. The effects of this "back-dating" of L2 upgrade batches will be reduced
        // as the permitted delay window is reduced in the future.
        require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

        _setNewProtocolVersion(_proposedUpgrade.newProtocolVersion);
        _upgradeL1Contract(_proposedUpgrade.l1ContractsUpgradeCalldata);
        _upgradeVerifier(_proposedUpgrade.verifier, _proposedUpgrade.verifierParams);
        _setBaseSystemContracts(_proposedUpgrade.bootloaderHash, _proposedUpgrade.defaultAccountHash);

        bytes32 txHash = _setL2SystemContractUpgrade(
            _proposedUpgrade.l2ProtocolUpgradeTx,
            _proposedUpgrade.factoryDeps,
            _proposedUpgrade.newProtocolVersion
        );

        _postUpgrade(_proposedUpgrade.postUpgradeCalldata);

        emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
    }
```

This function is an overriden one of the inherited `BaseZkSyncUpgrade.upgrade()`, case here is that unlike the inheritted version where the bytes data to be returned [has been explicitly mentioned as `txHash`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L67), this function does not explicitly name the variable to be returned, leading to all attempts of calling this function to return `0`.

#### Minimalistic POC

Deploying this contract on remix proves this bug case

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;

contract BaseContract {
    function upgrade(bytes memory _proposedUpgrade) public virtual pure returns (bytes32 txHash) {
txHash = bytes32(abi.encodePacked(_proposedUpgrade));
 }
}

contract BaseContractGenesis is BaseContract {


    function upgrade(bytes memory _proposedUpgrade) public override pure returns (bytes32) {

        bytes32 txHash = bytes32(abi.encodePacked(_proposedUpgrade));

    }
}

```

Passing the value: `0x212226`

We can see that:

- `BaseContract.upgrade()` returns `0: bytes32: txHash 0x2122260000000000000000000000000000000000000000000000000000000000`, &
- `BaseContractGenesis.upgrade()` returns `0: bytes32: txHash 0x0000000000000000000000000000000000000000000000000000000000000000`

And this happens despite both functions having the same implementation.

### Impact

Borderline low/medium, cause whereas genesis upgrades do not work as expected, we can't seem to find a direct instance where the expected hash being returned is implemented in protocol.

### Recommended Mitigation Steps

Name the variable to be returned as is done in [BaseZkSyncUpgrade.upgrade()`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L67) or attach the `return` at the end of the function's execution, i.e apply these changes to: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L46-L68

```diff

-    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32) {
+    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual override returns (bytes32 txHash) {
        // Note that due to commitment delay, the timestamp of the L2 upgrade batch may be earlier than the timestamp
        // of the L1 block at which the upgrade occurred. This means that using timestamp as a signifier of "upgraded"
        // on the L2 side would be inaccurate. The effects of this "back-dating" of L2 upgrade batches will be reduced
        // as the permitted delay window is reduced in the future.
        require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

        _setNewProtocolVersion(_proposedUpgrade.newProtocolVersion);
        _upgradeL1Contract(_proposedUpgrade.l1ContractsUpgradeCalldata);
        _upgradeVerifier(_proposedUpgrade.verifier, _proposedUpgrade.verifierParams);
        _setBaseSystemContracts(_proposedUpgrade.bootloaderHash, _proposedUpgrade.defaultAccountHash);

        bytes32 txHash = _setL2SystemContractUpgrade(
            _proposedUpgrade.l2ProtocolUpgradeTx,
            _proposedUpgrade.factoryDeps,
            _proposedUpgrade.newProtocolVersion
        );

        _postUpgrade(_proposedUpgrade.postUpgradeCalldata);

        emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
    }
```

#### Additional Note

> Depending on the judge's stance of either looking at this as "breaking core functionality" or "ignorable miss in `code/docs`" determines the final valididty as we assume the former puts this report on the grounds of a `medium`.

## QA-03 Bootloader wrongly identifies the `RIGHT_PADDED_GET_ACCOUNT_VERSION_SELECTOR` as not attached with the `Contract Deployer` deployment execution

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1937-L1961

```yul
            function shouldMsgValueMimicCallBeSystem(to, dataPtr) -> ret {
                let dataLen := mload(dataPtr)
                // Note, that this point it is not fully known whether it is indeed the selector
                // of the calldata (it might not be the case if the `dataLen` < 4), but it will be checked later on
                let selector := shr(224, mload(add(dataPtr, 32)))

                let isSelectorCreate := or(
                    eq(selector, {{CREATE_SELECTOR}}),
                    eq(selector, {{CREATE_ACCOUNT_SELECTOR}})
                )
                let isSelectorCreate2 := or(
                    eq(selector, {{CREATE2_SELECTOR}}),
                    eq(selector, {{CREATE2_ACCOUNT_SELECTOR}})
                )

                // Firstly, ensure that the selector is a valid deployment function
                ret := or(
                    isSelectorCreate,
                    isSelectorCreate2
                )
                // Secondly, ensure that the callee is ContractDeployer
                ret := and(ret, eq(to, CONTRACT_DEPLOYER_ADDR()))
                // Thirdly, ensure that the calldata is long enough to contain the selector
                ret := and(ret, gt(dataLen, 3))
            }
```

This function returns whether the mimicCall should use the `isSystem` flag, note that his flag should only be used for contract deployments and nothing else, now navigating to the bootloaders preprocess script here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/scripts/preprocess-bootloader.ts, we can see that, not all contract deployments selectors would be tagged with the flag, note that this is the intended behaviour since calls to the deployer system contract are the only ones allowed to be system calls

```json
...
  RIGHT_PADDED_GET_ACCOUNT_VERSION_SELECTOR: getPaddedSelector("ContractDeployer", "extendedAccountVersion"),
...
  CREATE_SELECTOR: getSelector("ContractDeployer", "create"),
  CREATE2_SELECTOR: getSelector("ContractDeployer", "create2"),
  CREATE_ACCOUNT_SELECTOR: getSelector("ContractDeployer", "createAccount"),
  CREATE2_ACCOUNT_SELECTOR: getSelector("ContractDeployer", "create2Account"),
...

```

Evidently there are 5 contract deployment functionalities attached with the bootloader's preprocessor, but only 4 of those would be tagged with the `isSystem` flag in the bootloader, since the "extendedAccountVersion" has not been attached

### Impact

The current implementation of the `bootloader::shouldMsgValueMimicCallBeSystem` would wrongly assume that the contract deployment of the "extendedAccountVersion" is not a system call, i.e [this instance of using the `isSystem` flag in the bootloader](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1972) wrongly assumes that this is not a system call, making the ABI returned by `getFarCallABI()` for low-level innvocations of calls and mimicCalls wrong.

The route for this logic is : `executeL1Tx-> msgValueSimulatorMimicCall -> shouldMsgValueMimicCallBeSystem /mimicCallOnlyResult -> getFarCallABI `

> Submitting this as QA, leaving to the judge to upgrade if they see fit

### Recommended Mitigation Steps

Include the `RIGHT_PADDED_GET_ACCOUNT_VERSION_SELECTOR` in `bootloader::shouldMsgValueMimicCallBeSystem` as an `isSystem` call.

## QA-04 The new `require(dictionary.length / 8 <= encodedData.length / 2)` check allows malicious operators to always pass in malformed data to the bootloader to ensure that all users gas gets burnt without executing the tx.

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L44-L70

```solidity
    function publishCompressedBytecode(
        bytes calldata _bytecode,
        bytes calldata _rawCompressedData
    ) external payable onlyCallFromBootloader returns (bytes32 bytecodeHash) {
        unchecked {
            (bytes calldata dictionary, bytes calldata encodedData) = _decodeRawBytecode(_rawCompressedData);


            require(
                encodedData.length * 4 == _bytecode.length,
                "Encoded data length should be 4 times shorter than the original bytecode"
            );


            require(
                dictionary.length / 8 <= encodedData.length / 2,
                "Dictionary should have at most the same number of entries as the encoded data"
            );


            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
                uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
                require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");


                uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
                uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);


                require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
            }
        }
```

The `publishCompressedBytecode()` function has been updated, and here is the new implementation https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L44-L70, in comparison to the previous implementation, it no longer enforces multiple checks, i.e the `dictionary.length % 8 = 0` and the check where the dictionary's length `< 2** 16` this is done so that protocol can correctly enforce more that the reason why a call to this function fails would be due to gas from the bootloader, but there is a new check that faults this logic , i.e `require(dictionary.length / 8 <= encodedData.length / 2)`, issue with this is that this check does not allow the bootloader to correctly enforce that calls to this functiion would mostly fail due to the gas provided not being enough and might still cause the attempt to forcefully revert https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1740-L1745 i.e an operator passing in a data that does not always fall as "correct" within the checks, for example say the new check of`dictionary.length / 8 <= encodedData.length / 2` is false, would lead to the `sendCompressedBytecode()` in the bootloader near calling and burning all the gas.

### Impact

Having it in mind that the `sendCompressedBytecode()` function is called by the bootloader whenever there is a need for the L2 transaction to use packed bytecode as seen here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1506 , this then gives the operator the opportunity of burning all of the user's provided gas of any L2 transaction that needs packed/published bytecodes... potentially doing it constantly if the operator is malicious since all they need to do is tamper with the data they pass to the bootloader to ensure the compression always ends up malformed by ignoring the new `dictionary.length/8` check and then all users attempt just burn their gas.

### Recommended Mitigation Steps

Since this enforcement `dictionary.length / 8 <= encodedData.length / 2` still needs to be placed so as not to allow operator pass in an excessive length, then the near calling should be scrapped from the bootloader when an attempt to `sendCompressedBytecode()` is made, i.e if the compression is malformed the attempt should instead revert with reason rather than burning all the gas.

#### Additiional Notes

> NB: This wasn't intended to be a QA submission, but these lines exist in the readMe: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/README.md#L31-L34

```markdown
### Validator can provide inefficient bytecode compression

In the current implementation, the mechanism for bytecode compression is not strictly unambiguous. That means the validator has the flexibility to choose a less efficient compression for the bytecode to increase the deployment cost for the end user. Besides that, there is another non-fixed [issue](https://github.com/code-423n4/2023-10-zksync-findings/issues/805), that gives a way for the operator to forces the user to pay more for the bytecode compression or even burn all the transaction gas during bytecode compression verification.
```

Now we assume the above snippet makes this issue somewhat subjective as we could argue it makes it stand on the lines of being OOS, If all parties think otherwise then this should be upgraded.

## QA-05 Users tokens could get lost indefinitely

### Proof of Concept

This is a "bug case" that's present in two different identified instances by us

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L554-L603

```solidity
    function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");


        // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
        if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
            chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
        }


        bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);


        {
            //@audit
            // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
            // Otherwise, the refund will be sent to the specified address.
            // If the recipient is a contract on L1, the address alias will be applied.
            address refundRecipient = _refundRecipient;
            if (_refundRecipient == address(0)) {
                refundRecipient = _prevMsgSender != tx.origin
                    ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
                    : _prevMsgSender;
            }


            L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
                chainId: ERA_CHAIN_ID,
                l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
                mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
                l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
                l2Calldata: l2TxCalldata,
                l2GasLimit: _l2TxGasLimit,
                l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
                factoryDeps: new bytes[](0),
                refundRecipient: refundRecipient
            });
            l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
        }


        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
        // Save the deposited amount to claim funds on L1 if the deposit failed on L2
        depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;


        emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
    }
```

This function initiates a deposit by locking funds on the contract and then sending the request, issue here arises whenever the refund is not specified, protocol then goes ahead to assume the refund recipient to be the aliased address of the sender if they are a contract.

Now, key to note that while this function is being called from the L1ERC20Bridge [`msg.sender` is being passed as `prevMsgSender`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L144-L147), main case here is with the aliasing logic and the fact that there is a high chance that the user has no control over the contract/ the private key for the `AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender) L2 address` and therefore this would lead to their funds being stuck funds in many cases.

- Now consider https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L287

```solidity
    function _requestL2Transaction(
        uint256 _mintValue,
        WritePriorityOpParams memory _params,
        bytes memory _calldata,
        bytes[] memory _factoryDeps
    ) internal returns (bytes32 canonicalTxHash) {
        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");
        _params.txId = s.priorityQueue.getTotalPriorityTxs();

        // Checking that the user provided enough ether to pay for the transaction.
        // Using a new scope to prevent "stack too deep" error

        _params.l2GasPrice = _deriveL2GasPrice(tx.gasprice, _params.l2GasPricePerPubdata);
        uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
        require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost

        // If the `_refundRecipient` is not provided, we use the `_sender` as the recipient.
        //@audit
        address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
        // If the `_refundRecipient` is a smart contract, we apply the L1 to L2 alias to prevent foot guns.
        if (refundRecipient.code.length > 0) {
            refundRecipient = AddressAliasHelper.applyL1ToL2Alias(refundRecipient);
        }
        _params.refundRecipient = refundRecipient;

        // populate missing fields
        _params.expirationTimestamp = uint64(block.timestamp + PRIORITY_EXPIRATION); // Safe to cast
        _params.valueToMint = _mintValue;

        canonicalTxHash = _writePriorityOp(_params, _calldata, _factoryDeps);
    }
```

We can see that a similar logic could be applied here, cause the contract during it's execution includes a refund recipient, now if it's set to `address(0)` _(assuming this to be the default behavior)_. The transaction on L2 fails, and a refund should be issued. However, because the refund recipient is msg.sender (the L2 contract), the refund goes to the L2 contract's address. The original sender from L1 does not receive the refund, resulting in a potential loss of funds in this case too.

### Impact

Users funds would be inacessible/stuck since they are not in control of the aliased address.

### Recommended Mitigation Steps

This is a pretty old bug case, where protocols assume that the msg.sender is in control of their addresses or aliased ones on another chain, whcich led to the famous [20M OP wintermute hack](https://rekt.news/wintermute-rekt/) from 2022, bestw ay imo to fix this would be that while depositing via `deposit(...)` if `_prevMsg.sender` is a contract and no explicit `refundRecipient` is specified, just revert the call.

#### Additional Note

- [Article from Rekt](https://rekt.news/wintermute-rekt/) &
- [Code4rena's bug report based on a similar ground](https://github.com/code-423n4/2023-09-maia-findings/issues?q=is%3Aissue+is%3Aopen+if+the+Virtual+Account%27s+owner+is+a+Contract+Account+%28multisig+wallet%29%2C+attackers+can+gain+control+of+the+Virtual+Accounts+by+gaining+control+of+the+same+owner%27s+address+in+a+different+chain)

## QA-06 A large amount withdrawal could break the minting logic of `L2BaseToken` effectively causing attempts of consequent mints to fail

### Proof of Concept

First take a look at both ways to intiate the withdrawals https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L72-L93

```solidity
    function withdraw(address _l1Receiver) external payable override {
        uint256 amount = _burnMsgValue();

        // Send the L2 log, a user could use it as proof of the withdrawal
        bytes memory message = _getL1WithdrawMessage(_l1Receiver, amount);
        L1_MESSENGER_CONTRACT.sendToL1(message);

        emit Withdrawal(msg.sender, _l1Receiver, amount);
    }

    function withdrawWithMessage(address _l1Receiver, bytes memory _additionalData) external payable override {
        uint256 amount = _burnMsgValue();

        // Send the L2 log, a user could use it as proof of the withdrawal
        bytes memory message = _getExtendedWithdrawMessage(_l1Receiver, amount, msg.sender, _additionalData);
        L1_MESSENGER_CONTRACT.sendToL1(message);

        emit WithdrawalWithMessage(msg.sender, _l1Receiver, amount, _additionalData);
    }
```

Evident that both functions are for initiating the withdrawals to be claimed on L1, and the only difference is that the former purely withdraws whereas the latter attaches a message, now they both make a call to [`_burnMsgValue()`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L73) while calculating the amount to be withdrawn, whose implementation is defined here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L99-L109

```solidity
    function _burnMsgValue() internal returns (uint256 amount) {
        amount = msg.value;

        // Silent burning of the ether
        unchecked {
            // This is safe, since this contract holds the ether balances, and if user
            // send a `msg.value` it will be added to the contract (`this`) balance.
            balance[address(this)] -= amount;
            totalSupply -= amount;
        }
    }
```

Case here is that, protocol wrongly assumes that having the subtractions in the unchecked block is "completely" safe, but that's wrong, this is cause the only safe part of this `balance[address(this)] -= amount` this is cause no matter the value of `amount` passed it's equal to the `msg.value` and as such has already been transferred to the contract, i.e `address(this)`, but the same argument can't be made for `totalSupply -= amount` this is cause, no addition of `msg.value` to `totalSupply` is enforced before this subtraction, going through this contract we can see that, the only instance where the totatalSupply gets increased is when `mint()` is called from the bootloader https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L64-L68

```solidity
    function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
        totalSupply += _amount;
        balance[_account] += _amount;
        emit Mint(_account, _amount);
    }
```

Meaning that whenever `totalSupply < msg.value` evaluates to true, while executing `_burnMsgValue()` the totalSupply value is crazily updated to very close to uint(256).max since the subtraction is done in an unchecked block.

### Impact

Say multiple black swan events occur on zkSync and now users have lost their interest in the rollup and are taking their funds off to L1 enmasse, this would lead to the higher chance that since all withdrawals are akready depleting the `totalSupply` a large supply would come and cause to this to underflow.

The above case is not the only route where this even checks in, the simple fact that if the total minted supply is not too large then multiple attempts to withdraw or even one attempt to withdraw could break the accounting logic of the `totalSupply`.

Now asides breaking burning, this would go ahead to break the minting logic cause now we have a very massive value for `totalSupply` and any little addition would cause it to overflow,[case is that while minting there are no unchecked blocks](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L63-L68), so the default solidity 0.8.x overflow/underflow protection would cause this to revert.

> NB: This causes a very High impact, but has a very low probability of happening, so its borderline QA/Medium

### Recommended Mitigation Steps

Consider explicitly checking that the total supply is more than the requested amount to be burnt, i.e apply these changes to https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/L2BaseToken.sol#L99-L109

```diff
    function _burnMsgValue() internal returns (uint256 amount) {
        amount = msg.value;
+     require(totalSupply >= amount, "Transfer amount exceeds total minted supply");
        // Silent burning of the ether
        unchecked {
            // This is safe, since this contract holds the ether balances, and if user
            // send a `msg.value` it will be added to the contract (`this`) balance.
            balance[address(this)] -= amount;
            totalSupply -= amount;
        }
    }
```

## QA-07 Fix typos & documentations _(Multiple instances)_

### Proof of Concept

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L331-L338

```solidity
            {
                // Deposits that happened before the upgrade cannot be checked here, they have to be claimed and checked in the legacyBridge
                bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);
                //@audit
                // Double claims are not possible, as we this check except for legacy bridge withdrawals
                // Funds claimed before the update will still be recorded in the legacy bridge
                // Note we double check NEW deposits if they are called from the legacy bridge
                notCheckedInLegacyBridgeOrWeCanCheckDeposit = (!_checkedInLegacyBridge) || weCanCheckDepositHere;
            }
```

Evidently the statement "Double claims are not possible, as we this except for legacy bridge withdrawals" is wrong and should be fixed.

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L115-L136

```solidity
    /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
        if (_token == ETH_TOKEN_ADDRESS) {
            uint256 balanceBefore = address(this).balance;
            IMailbox(_target).transferEthToSharedBridge();
            uint256 balanceAfter = address(this).balance;
            require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
                balanceAfter -
                balanceBefore;
        } else {
            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
            require(amount > 0, "ShB: 0 amount to transfer");
            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
        }
    }

```

This: " /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process"

Should be changed to: " /// @dev transfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process"

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L188-L195

```solidity
        // We only require 9 logs to be checked, the 10th is if we are expecting a protocol upgrade
        // Without the protocol upgrade we expect 9 logs: 2^9 - 1 = 511
        // With the protocol upgrade we expect 8 logs: 2^10 - 1 = 1023
        if (_expectedSystemContractUpgradeTxHash == bytes32(0)) {
            require(processedLogs == 511, "b7");
        } else {
            require(processedLogs == 1023, "b8");
        }
```

This line: `// With the protocol upgrade we expect 8 logs: 2^10 - 1 = 1023`, obviously should be `// With the protocol upgrade we expect **10** logs: 2^10 - 1 = 1023`

- Another instance here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1498-L1501

```yul
                        // Here we are making sure that the bytecode is indeed not yet know and needs to be published,
                        // preveting users from being overcharged by the operator.
                        let marker := getCodeMarker(bytecodeHash)

```

It should instead be "Here we are making sure that the bytecode is indeed not yet **known** and needs to be published"

- One more instance can be seen here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L43-L47

```solidity
/// @dev The maximal possible address of an L1-like precompie. These precompiles maintain the following properties:
/// - Their extcodehash is EMPTY_STRING_KECCAK
/// - Their extcodesize is 0 despite having a bytecode formally deployed there.
uint256 constant CURRENT_MAX_PRECOMPILE_ADDRESS = 0xff;

```

Evidently the comment means to say "/// @dev The maximal possible address of an L1-like **precompile**. These precompiles maintain the following properties:"... and not `precompie`.

- Another instance can be seen here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/precompiles/CodeOracle.yul#L68-L71

```yul
            function decommit(versionedHash, lenInWords) {
                // The operation below are never expected to overflow since the `lenInWords` is a most 2 bytes long.
                let gasCost := mul(decommmitCostPerWord(), lenInWords)
            //..snip
           }

```

This line : `The operation below are never expected to overflow since the `lenInWords` is a most 2 bytes long.` should be "The operation below are never expected to overflow since the `lenInWords` is **at** most 2 bytes long."

- Another instance is here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/precompiles/P256Verify.yul#L4

```yul
 * @notice The contract that emulates RIP-7212's P256VERIFY precompile.
```

`RIP` should instead be `EIP`

- Another instance is here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L38

```solidity
 * methods won't work for non-system contracts and also breaking changes at short notice are possilbe.
```

`possilbe` should be `possible`


### Impact

Bad documentation code structure, making it hard for users/developers to understand code.

### Recommended Mitigation Steps

Fix the typos from these instances

## QA-08 There are currently no assurances that funds specified for operation are rightly matched

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L168-L202

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
        emit OperationExecuted(id);
    }

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
        emit OperationExecuted(id);
    }

```

These function at the long run call the below: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L225-L235

```solidity
    function _execute(Call[] calldata _calls) internal {
        for (uint256 i = 0; i < _calls.length; ++i) {
            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
            if (!success) {
                // Propagate an error if the call fails.
                assembly {
                    revert(add(returnData, 0x20), mload(returnData))
                }
            }
        }
    }
```

These functions are used to execute schedule operations either instantly or after their respective delays have passed, now issue is that the public function are marked as `payable` which suggests that while calling these functions, msg.value is going to be passed with them, but in the internal `_execute()` there is no validation that the msg.value provided is equal to the total value of `call[i].value` needed in the loop.

### Impact

Potential having excess funds in the Governance.sol, i.e when the msg.value is way greater than the total call.value needed for thetransaction, or not enough funds being available for the execution which then leads to eating up funds that have been sent to the contract for different operations

### Recommended Mitigation Steps

Check that msg.value == the total call value needed, if protocol plans on routing the logic via the balance too, then check if the `msg.value + contract's balance of eth` is enough for transaction.

## QA-09 Protocol is susceptible to synchronizing issues cause reverted system contract upgrade batches must stiill be commited between L1 and L2 upgrades due to wrongly asuming just reverting in the bootloader is enough

### Proof of Concept

Currently, either `upgrade()` function of [BaseZkSyncUpgrade](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L67C1-L88C6) and [BaseZkSyncUpgradeGenesis](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L47C3-L68C6) is called depending on the context of the current upgrade.

Considering `BaseZkSyncUpgrade` we can see that [`BaseZkSyncUpgrade::upgrade()` eventually calls `_setL2SystemContractUpgrade()`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L79) to pass on the data for the proposed upgrade

```solidity
        txHash = _setL2SystemContractUpgrade(
            _proposedUpgrade.l2ProtocolUpgradeTx,
            _proposedUpgrade.factoryDeps,
            _proposedUpgrade.newProtocolVersion
        );
```

Considering it's an upgrade transaction, this transaction should be executed on L2 with` _l2ProtocolUpgradeTx.txType = 254`. In the bootloader, i.e https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L594-L612

```yul
                    case 254 {
                        // This is an upgrade transaction.
                        // Protocol upgrade transactions are processed totally in the same manner as the normal L1->L2 transactions,
                        // the only difference are:
                        // - They must be the first one in the batch
                        // - They have a different type to prevent tx hash collisions and preserve the expectation that the
                        // L1->L2 transactions have priorityTxId inside them.
                        if transactionIndex {
                            assertionError("Protocol upgrade tx not first")
                        }

                        // This is to be called in the event that the L1 Transaction is a protocol upgrade txn.
                        // Since this is upgrade transactions, we are okay that the gasUsed by the transaction will
                        // not cover this additional hash computation
                        let canonicalL1TxHash := getCanonicalL1TxHash(txDataOffset)
                        sendToL1Native(true, protocolUpgradeTxHashKey(), canonicalL1TxHash)
                        //@audit
                        processL1Tx(txDataOffset, resultPtr, transactionIndex, userProvidedPubdataPrice, false)
                    }
```

Now during the current execution, [if for any reason this attempt fails, say the execution runs out of gas, the execution reverts](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1010-L1015), which is a direct fix to the **primary issue** from the previous audit contests, i.e https://github.com/code-423n4/2023-10-zksync-findings/issues/214#issuecomment-1795027489, but this is not enough fix to ensure that the synchronization is always in play.

Consider [these issues](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=label%3Aduplicate-214+is%3Aclosed) that were duplicated to the aforementioned due to having a similar logic, most especially [1](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+No+way+of+preventing+the+upgrade+from+happening+even+if+it+has+a+critical+vulnerability+is%3Aclosed) & [2](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+if+a+batch+committed+with+system+contract+upgrades+is+reverted+via+revertBatches%28%29+to+prevent+execution+of+that+batch%2C+new+batches+intended+to+be+committed+with+no+system+contract+upgrades+will+be+committed+as+batches+with+system+contract+upgrades.+is%3Aclosed).

In short, for [1](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+No+way+of+preventing+the+upgrade+from+happening+even+if+it+has+a+critical+vulnerability+is%3Aclosed) the bug report is about, whenever an upgrade has a criticial vulnerabilty, current implementation does not provide a possibility of preventing the upgrade to go on, cause the upgrade must be carried out and cannot be changed even if batches get reverted.

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L472-L497

```solidity
    function revertBatches(uint256 _newLastBatch) external nonReentrant onlyValidatorOrStateTransitionManager {
        _revertBatches(_newLastBatch);
    }


    /// @inheritdoc IExecutor
    function revertBatchesSharedBridge(uint256, uint256 _newLastBatch) external nonReentrant onlyValidator {
        _revertBatches(_newLastBatch);
    }


    function _revertBatches(uint256 _newLastBatch) internal {
        require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch
        require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted


        if (_newLastBatch < s.totalBatchesVerified) {
            s.totalBatchesVerified = _newLastBatch;
        }
        s.totalBatchesCommitted = _newLastBatch;


        // Reset the batch number of the executed system contracts upgrade transaction if the batch
        // where the system contracts upgrade was committed is among the reverted batches.
        if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
            delete s.l2SystemContractsUpgradeBatchNumber;
        }


        emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
    }
```

Evidently, one can see that the suggested fix from the report has not been implemented, i.e while reverting the upgrade tx the `s.l2SystemContractsUpgradeTxHash` is not provided again to prevent the error inorder to increase the robustness of the system, that's to say for cases like this, the team would then not have time to prevent the upgrade from happening, fix the error, and make an upgrade tx again rather than leaving the vulnerable upgrade in the wild and not being implemented.

Bug flow should be seen from the [attached report](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+No+way+of+preventing+the+upgrade+from+happening+even+if+it+has+a+critical+vulnerability+is%3Aclosed), now protocol's plan to solve this is by overriding `s.l2SystemContractsUpgradeTxHash` in order to cancel the buggy upgrade, but this wouldn't work, cause that upgrade [must be carried out in the next batch](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/docs/Smart%20contract%20Section/Handling%20L1%E2%86%92L2%20ops%20on%20zkSync.md?plain=1#L59-L65), so it gives zero time for protocol to code and then even deploy the new upgrader, now within this time frame, an attacker aware of the bugs in the implementation can exploit the system.

For case [2](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+if+a+batch+committed+with+system+contract+upgrades+is+reverted+via+revertBatches%28%29+to+prevent+execution+of+that+batch%2C+new+batches+intended+to+be+committed+with+no+system+contract+upgrades+will+be+committed+as+batches+with+system+contract+upgrades.+is%3Aclosed), the core of the issue is the same, i.e it lies in the protocol's failure to delete the transaction hash associated with a system contract upgrade when reverting a batch. This leads to a scenario where subsequent batches, even those not intended to include a system contract upgrade, are processed as if they do, due to the presence of the leftover upgrade transaction hash. This misprocessing causes unintended execution of system contract upgrades or reverts due to mismatched expectations about the batch's content.

Now, the protocol's design allows for the reverting of batches to undo changes not yet executed.However as previously highlighted, it inadequately addresses the cleanup of system contract upgrade markers, specifically the transaction hash (`s.l2SystemContractsUpgradeTxHash`). While it resets the batch number indicating an upgrade (`s.l2SystemContractsUpgradeBatchNumber`), it neglects the corresponding transaction hash. This leads to confusion in the `_commitBatches()` function, take a look at this https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L215-L248

```solidity
    function _commitBatches(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        // check that we have the right protocol version
        // three comments:
        // 1. A chain has to keep their protocol version up to date, as processing a block requires the latest or previous protocol version
        // to solve this we will need to add the feature to create batches with only the protocol upgrade tx, without any other txs.
        // 2. A chain might become out of sync if it launches while we are in the middle of a protocol upgrade. This would mean they cannot process their genesis upgrade
        // as thier protocolversion would be outdated, and they also cannot process the protocol upgrade tx as they have a pending upgrade.
        // 3. The protocol upgrade is increased in the BaseZkSyncUpgrade, in the executor only the systemContractsUpgradeTxHash is checked
        require(
            IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
            "Executor facet: wrong protocol version"
        );
        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
        require(_newBatchesData.length == 1, "e4");
        // Check that we commit batches after last committed batch
        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data


        bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
        // Upgrades are rarely done so we optimize a case with no active system contracts upgrade.
        //@audit
        if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
        } else {
            _commitBatchesWithSystemContractsUpgrade(
                _lastCommittedBatchData,
                _newBatchesData,
                systemContractsUpgradeTxHash
            );
        }


        s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
    }
```

Here we see that the new logic for EIP-4844, requirees only one batch to be committed at a time due to restriction of blobs per block, but this doesn't solve the root case, cause regardless, `if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0)` is `false`, which would be the case for our reverted batch, then the execution **always** routes the logic [to commiting with system contract upgrades](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239-L245).

TLDR: `revert()` will delete upgrade batch number but not the batch tx thus making reverts of batches with system upgrade **non functional** since the system tx hash may still be executed with new batches.

### Impact

Medium _(reason for submitting as QA attached in the  `#### Additiional Note` section )_, this is cause for the first case, we show how protocol have timelocked themself from being able to to stop the upgrade to a buggy implementation, that might even have critical bug implementations that an attacker could exploit while they code and attemot deploying a non buggy implementation, and for the second case, similar to the first we can see how if for whatever reason `l2SystemContractsUpgradeTxHash` is to be stopped from executing with a batch, it is not possible to do so, [due to `s.l2SystemContractsUpgradeTxHash` not being reverted in `revertBatches()`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L490-L494)

### Recommended Mitigation Steps

Modify the `revertBatches()` function to ensure comprehensive cleanup after a batch revert. This includes not only resetting the batch number associated with a system contract upgrade but also clearing the related transaction hash (`s.l2SystemContractsUpgradeTxHash`).
While reverting batches both `l2SystemContractsUpgradeBatchNumber` `s.l2SystemContractsUpgradeTxHash` should be provided and deleted.

#### Additiional Note

> NB: This wasn't intended to be a QA submission, but these lines exist in the readMe:https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/README.md#L35-L38

```markdown
### Aknowledged issues from the previous audits

All unfixed issues from the previous audits are considered out of scope.
- https://era.zksync.io/docs/reference/troubleshooting/audit-bug-bounty.html
```

Now, whereas navigating to the attached link from the `readMe` we can't see the audit where the idea of this bug has been coined attached, we still assume  that it is part of the _previous_ findings, now we just don't know if this was "acknowledged" or "confirmed" since we can see that the [team clearly "confirmed" the bug case](https://github.com/code-423n4/2023-10-zksync-findings/issues/214#issuecomment-1795027489) and applied a fix to it [in this commit](https://github.com/code-423n4/2024-03-zksync/compare/2023-10-zksync...main) provided for this contest, albeit an insufficient one... due to all these we've decided that rhis issue somewhat subjective and we'd leave it to the judge if they deem it fit to be be upgraded.

## QA- 10 Shadow upgrades would currently have their executional data leaked if they fail

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/IGovernance.sol#L21-L40

```solidity
struct Call {
    address target;
    uint256 value;
    bytes data;
}
struct Operation {
    Call[] calls;
    bytes32 predecessor;
    bytes32 salt;
}
```

The above represents both the struct used for calls made during an operation and how how an operation is being defined.

From [here](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L142-L145), we can see that protocol implements a logic for shadow upgrades.

Note that these trpes of upgrades are designed to keep upgrade details confidential until execution. However, if an upgrade attempt fails, the information within the `Operation calldata _operation` parameter, which is bundled with the call specifics via [execute()](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L168-L182), becomes public.

### Impact

A failed shadow upgrade unintentionally exposes critical upgrade details to the public, which can include sensitive call data and operational parameters. Malicious actors could exploit this information to discover system vulnerabilities and mount attacks before the deployment of a security patch, note that the current upgrade to the `Governance.sol` even marks these functions (i.e execute() & executeInstant() ) as payable, which suggests that now native token values could be attached to this window.

### Recommended Mitigation Steps

Enforce a protective mechanism that automatically puts the system in a freeze mode upon failure.

## QA-11 Fix bugs present in the precomcompiles or clearly document the bugs for users/developers

### Proof of Concept

Take a look at https://github.com/code-423n4/2023-10-zksync-findings/issues?q=175

Focus on the primary issue and it's duplicate, they all talk about how they are behavorial incosistencies in precompiles when they are delegate called into, with suggesting that the delegateCall() function of the EfficientCall() should be reimplemented to check if this precompiles are to be called and instead pass the call in as a staticcall, issue is that, as shown in the snippet belwo no change has been made to this function attached with the fact that no documentations attached to the natspec with this bug case, i.e https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L83-L95

```solidity
    /// @notice Perform a `delegateCall` without copying calldata to memory.
    /// @param _gas The gas to use for the call.
    /// @param _address The address to call.
    /// @param _data The calldata to use for the call.
    /// @return returnData The copied to memory return data.
    function delegateCall(
        uint256 _gas,
        address _address,
        bytes calldata _data
    ) internal returns (bytes memory returnData) {
        bool success = rawDelegateCall(_gas, _address, _data);
        returnData = _verifyCallResult(success);
    }
```

### Impact

Deviation from the EVM's precompile method

### Recommended Mitigation Steps

Consider clearly documenting ths bug case and inform users to not attempt calling it via delegate call or apply the suggested fixes of first checking if the contracts to be called are the precompiles and then `staticcall` them.

## QA-12 Consider renaming `CURRENT_MAX_PRECOMPILE_ADDRESS` to `MAX_POSSIBLE_PRECOMPILE_ADDRESS`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L43-L47

```solidity
/// @dev The maximal possible address of an L1-like precompie. These precompiles maintain the following properties:
/// - Their extcodehash is EMPTY_STRING_KECCAK
/// - Their extcodesize is 0 despite having a bytecode formally deployed there.
uint256 constant CURRENT_MAX_PRECOMPILE_ADDRESS = 0xff;

```

Note that this address is used in the`AccountCodeStorage.getCodeHash`function, i.e

```solidity
address account = address(uint160(_input));
if (uint160(account) <= CURRENT_MAX_PRECOMPILE_ADDRESS) {
    return EMPTY_STRING_KECCAK;
}
```

Case is that the current name suggests that there are 255 addresses already, where as is should mean that the maximal possible address of an L1-like precompile should be 255 as[ this comment ](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L43) hints.

### Impact

Confusing code, makes it harder to understand protocol

### Recommended Mitigation Steps

Consider changing `CURRENT_MAX_PRECOMPILE_ADDRESS` to `MAX_POSSIBLE_PRECOMPILE_ADDRESS`.

## QA-13 Users funds could still be stuck due to lack of access to `ETH` on the `L2` through `L1->L2 `transactions so this should be clearly documented

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L286

```solidity
    function _requestL2Transaction(
        uint256 _mintValue,
        WritePriorityOpParams memory _params,
        bytes memory _calldata,
        bytes[] memory _factoryDeps
    ) internal returns (bytes32 canonicalTxHash) {
        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");
        _params.txId = s.priorityQueue.getTotalPriorityTxs();

        // Checking that the user provided enough ether to pay for the transaction.
        // Using a new scope to prevent "stack too deep" error

        _params.l2GasPrice = _deriveL2GasPrice(tx.gasprice, _params.l2GasPricePerPubdata);
        uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
        //@audit
        require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost

        // If the `_refundRecipient` is not provided, we use the `_sender` as the recipient.
        address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
        // If the `_refundRecipient` is a smart contract, we apply the L1 to L2 alias to prevent foot guns.
        if (refundRecipient.code.length > 0) {
            refundRecipient = AddressAliasHelper.applyL1ToL2Alias(refundRecipient);
        }
        _params.refundRecipient = refundRecipient;

        // populate missing fields
        _params.expirationTimestamp = uint64(block.timestamp + PRIORITY_EXPIRATION); // Safe to cast
        _params.valueToMint = _mintValue;

        canonicalTxHash = _writePriorityOp(_params, _calldata, _factoryDeps);
    }
```

This function eventually gets called when requesting transactions from the L2, note that there is an enforcement that `mintVaue` is always larger than `baseCost + _params.l2Value`, note that from [here](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L283-L286) we can see that the msg.value of the L1->L2 transaction must only be part of ETH to be minted inside of transaction processing on the L2, the same thing can be [confirmed in the bootloader](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1818-L1822)

Now, the [DefaultAccount.sol mistakenly assumes that L1->L2 transactions initiated by external owned accounts (EOAs) provide all necessary functionality](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/DefaultAccount.sol#L118-L127), leading to its `executeTransactionFromOutside()` function being left unimplemented.

This oversight means users cannot access their ETH on L2 if a malicious operator selectively processes only L1->L2 transactions. This scenario not only restricts access to ETH on L2 but also breaches the security principle that guarantees users can initiate transactions from L1 to L2, enabling them to withdraw their assets in anticipation of a potentially harmful upgrade.

### Impact

- Users cannot access their L2 ETH if the operator acts maliciously.
- Compromises the security guarantee that allows fund withdrawals before executing a malicious upgrade.

> NB: Submitting as QA cause whereas sponsors "confirmed" this bug from the previous contest, they tagged it as a `disagree with severity`... but still of the opinion that this is a borderline medium severity bug and leaving at the discretion of the judge.

### Recommended Mitigation Steps

Enable the creation of L1->L2 transactions that can draw upon ETH in the L2 balance as part of the transaction value. Alternatively, implement functionality in the `DefaultAccount::executeTransactionFromOutside` function to ensure it operates as initially intended or this should be clearly documented

## QA-14 If the pending admin becomes malicious there is no specific way to stop them from accepting the admin

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L22-L42

```solidity
    /// @inheritdoc IAdmin
    function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
        // Save previous value into the stack to put it into the event later
        address oldPendingAdmin = s.pendingAdmin;
        // Change pending admin
        s.pendingAdmin = _newPendingAdmin;
        emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
    }

    /// @inheritdoc IAdmin
    function acceptAdmin() external {
        address pendingAdmin = s.pendingAdmin;
        require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights

        address previousAdmin = s.admin;
        s.admin = pendingAdmin;
        delete s.pendingAdmin;

        emit NewPendingAdmin(pendingAdmin, address(0));
        emit NewAdmin(previousAdmin, pendingAdmin);
    }
```

Both functions are all used in the logic to update the admins.

Now consider this scenario:

- Current admin sets a new pending admin
- After a few days, current admin found out that pending admin is malicious (or even maybe a wrong address, i.e current admin made a mistake to set a wrong address as pending admin)
- Current admin now attempts to update the pending admin with a new fresh pending admin
- Current pending admin sees the transaction and then front runs it by accepting the admin status

### Impact

Low, since this overall depends on the current admin setting an address that could become malicious as the pending admin (or a wrong address)

### Recommended Mitigation Steps

Consider implementing timelocks to the whole logic, i.e if pending admin does not accept their admin status in 1 day, it should be automatically revoked.

## QA-15 Protocol does not consider EIP-4844 and still assumes more than one batch can be commited

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L215-L306

```solidity
    function _commitBatches(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        //omitted for brevity
        //@audit
        // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
        require(_newBatchesData.length == 1, "e4");
        // Check that we commit batches after last committed batch
        require(s.storedBatchHashes[s.totalBatchesCommitted] == _hashStoredBatchInfo(_lastCommittedBatchData), "i"); // incorrect previous batch data

        bytes32 systemContractsUpgradeTxHash = s.l2SystemContractsUpgradeTxHash;
        // Upgrades are rarely done so we optimize a case with no active system contracts upgrade.
        if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0) {
            _commitBatchesWithoutSystemContractsUpgrade(_lastCommittedBatchData, _newBatchesData);
        } else {
            _commitBatchesWithSystemContractsUpgrade(
                _lastCommittedBatchData,
                _newBatchesData,
                systemContractsUpgradeTxHash
            );
        }

        s.totalBatchesCommitted = s.totalBatchesCommitted + _newBatchesData.length;
    }


    function _commitBatchesWithoutSystemContractsUpgrade(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData
    ) internal {
        //omitted for brevity
        //@audit
        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
            _lastCommittedBatchData = _commitOneBatch(_lastCommittedBatchData, _newBatchesData[i], bytes32(0));

            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
            emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            );
        }
    }


    function _commitBatchesWithSystemContractsUpgrade(
        StoredBatchInfo memory _lastCommittedBatchData,
        CommitBatchInfo[] calldata _newBatchesData,
        bytes32 _systemContractUpgradeTxHash
    ) internal {
        //omitted for brevity
        //@audit
        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
            // The upgrade transaction must only be included in the first batch.
            bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
            _lastCommittedBatchData = _commitOneBatch(
                _lastCommittedBatchData,
                _newBatchesData[i],
                expectedUpgradeTxHash
            );

            s.storedBatchHashes[_lastCommittedBatchData.batchNumber] = _hashStoredBatchInfo(_lastCommittedBatchData);
            emit BlockCommit(
                _lastCommittedBatchData.batchNumber,
                _lastCommittedBatchData.batchHash,
                _lastCommittedBatchData.commitment
            );
        }
    }

```

Now these functions are called whenever batches are to be committed, now post the EIP-4844 implementation, due to the restriction on number of blobs per block, protocol can only allow for a single batch to be committed at a time, which is clearly noted in `_commitBatches()` case here is that both `_commitBatchesWithoutSystemContractsUpgrade()` and `_commitBatchesWithSystemContractsUpgrade()` still attempt to loop through the `newBatchesData.length` which is already hardcoded and can only be one.

### Impact

Confusing code implementation, residue code from pre EIP-4844 implementation still present in code, post `EIP-4844` implementation.

### Recommended Mitigation Steps

Remove the for loops in both functions.

#### Additional Note

This bug is also present in this instance below: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L107-L142

```solidity

    function commitBatches(
        StoredBatchInfo calldata,
        CommitBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(ERA_CHAIN_ID) {
        unchecked {
            // This contract is only a temporary solution, that hopefully will be disabled until 2106 year, so...
            // It is safe to cast.
            uint32 timestamp = uint32(block.timestamp);
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                committedBatchTimestamp[ERA_CHAIN_ID].set(_newBatchesData[i].batchNumber, timestamp);
            }
        }

        _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
    }

    /// @dev Records the timestamp for all provided committed batches and make
    /// a call to the hyperchain diamond contract with the same calldata.
    function commitBatchesSharedBridge(
        uint256 _chainId,
        StoredBatchInfo calldata,
        CommitBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(_chainId) {
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

```

And https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L180-L222

```solidity
    /// @dev Check that batches were committed at least X time ago and
    /// make a call to the hyperchain diamond contract with the same calldata.
    function executeBatches(StoredBatchInfo[] calldata _newBatchesData) external onlyValidator(ERA_CHAIN_ID) {
        uint256 delay = executionDelay; // uint32
        unchecked {
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
                    _newBatchesData[i].batchNumber
                );

                // Note: if the `commitBatchTimestamp` is zero, that means either:
                // * The batch was committed, but not through this contract.
                // * The batch wasn't committed at all, so execution will fail in the zkSync contract.
                // We allow executing such batches.

                require(block.timestamp >= commitBatchTimestamp + delay, "5c"); // The delay is not passed
            }
        }
        _propagateToZkSyncStateTransition(ERA_CHAIN_ID);
    }

    /// @dev Check that batches were committed at least X time ago and
    /// make a call to the hyperchain diamond contract with the same calldata.
    function executeBatchesSharedBridge(
        uint256 _chainId,
        StoredBatchInfo[] calldata _newBatchesData
    ) external onlyValidator(_chainId) {
        uint256 delay = executionDelay; // uint32
        unchecked {
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
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

```

## QA-16 Missing getter functions for key internal `ZkSyncStateTransitionStorage` variables should be introduced

### Proof of Concept

Take a look at the getter facet here: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol

Now, consider the `ZkSyncStateTransitionStorage` struct here: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/ZkSyncStateTransitionStorage.sol#L66-L153

Going through both code snippets, one can see that where as there are multiple getter functions a few are missing, to list them:

1. `__DEPRECATED_diamondCutStorage`
2. `__DEPRECATED_governor`
3. `__DEPRECATED_pendingGovernor`
4. `__DEPRECATED_allowList`
5. `UpgradeStorage __DEPRECATED_upgrades`
6. `__DEPRECATED_lastWithdrawalLimitReset`
7. `__DEPRECATED_withdrawnAmountInWindow`
8. `mapping(address => uint256) __DEPRECATED_totalDepositedAmountPerUser`
9. `bool zkPorterIsAvailable`
10. `address blobVersionedHashRetriever`
11. `uint256 chainId`

Now where as one can say it's arguable not to attache getters for the deprecated variables, we can't say that for the non-deprecated ones.

### Impact

Users can't directly query important state data.

### Recommended Mitigation Steps

Consider adding corresponding getter functions in `Getters.sol` for the nondeprecated storage data.

## QA-17 upgrades are automatically immediately possible instead of being able to have a kick in time in the future

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L177-L228

```solidity
    function _setChainIdUpgrade(uint256 _chainId, address _chainContract) internal {
        bytes memory systemContextCalldata = abi.encodeCall(ISystemContext.setChainId, (_chainId));
        uint256[] memory uintEmptyArray;
        bytes[] memory bytesEmptyArray;

        L2CanonicalTransaction memory l2ProtocolUpgradeTx = L2CanonicalTransaction({
            txType: SYSTEM_UPGRADE_L2_TX_TYPE,
            from: uint256(uint160(L2_FORCE_DEPLOYER_ADDR)),
            to: uint256(uint160(L2_SYSTEM_CONTEXT_SYSTEM_CONTRACT_ADDR)),
            gasLimit: $(PRIORITY_TX_MAX_GAS_LIMIT),
            gasPerPubdataByteLimit: REQUIRED_L2_GAS_PRICE_PER_PUBDATA,
            maxFeePerGas: uint256(0),
            maxPriorityFeePerGas: uint256(0),
            paymaster: uint256(0),
            // Note, that the priority operation id is used as "nonce" for L1->L2 transactions
            nonce: protocolVersion,
            value: 0,
            reserved: [uint256(0), 0, 0, 0],
            data: systemContextCalldata,
            signature: new bytes(0),
            factoryDeps: uintEmptyArray,
            paymasterInput: new bytes(0),
            reservedDynamic: new bytes(0)
        });

        ProposedUpgrade memory proposedUpgrade = ProposedUpgrade({
            l2ProtocolUpgradeTx: l2ProtocolUpgradeTx,
            factoryDeps: bytesEmptyArray,
            bootloaderHash: bytes32(0),
            defaultAccountHash: bytes32(0),
            verifier: address(0),
            verifierParams: VerifierParams({
                recursionNodeLevelVkHash: bytes32(0),
                recursionLeafLevelVkHash: bytes32(0),
                recursionCircuitsSetVksHash: bytes32(0)
            }),
            l1ContractsUpgradeCalldata: new bytes(0),
            postUpgradeCalldata: new bytes(0),
            upgradeTimestamp: 0,
            newProtocolVersion: protocolVersion
        });

        Diamond.FacetCut[] memory emptyArray;
        Diamond.DiamondCutData memory cutData = Diamond.DiamondCutData({
            facetCuts: emptyArray,
            initAddress: genesisUpgrade,
            initCalldata: abi.encodeCall(IDefaultUpgrade.upgrade, (proposedUpgrade))
        });

        IAdmin(_chainContract).executeUpgrade(cutData);
        emit SetChainIdUpgrade(_chainContract, l2ProtocolUpgradeTx, protocolVersion);
    }
```

Considering this is the logic, for setting chain upgrades, what to note here is the setting applied to the `ProposedUpgrade` struct, navigating here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L14-L40, we can see all the necessities, attached to this struct, i.e most members of the struct are to kept as `0` in order not to be updated which is rightly, but the logic for `upgradeTimestamp` and `newProtocolVersion` is wrong.

For `upgradeTimestamp`, this value should be set as the timestamp after which the upgrade can be executed, i.e in the future or at least it shouldn't be hardcoded to `0`.

For `newProtocolVersion` the version needs to be greater than the previous protocol version, but execution instead just queries the current version which is wrong, since [the attempt to upgrade the version from BaseZkSyncUpgrade.sol would revert](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L238-L241) if the version is not greater than the current one.

Additionally note that this comment: "Note, that the priority operation id is used as "nonce" for L1->L2 transactions" in this case is invalid as the operation is not a `PRIORITY_OPERATION_L2_TX_TYPE` but rather a `SYSTEM_UPGRADE_L2_TX_TYPE`.

### Impact

The logic of having an upgrade be scheduled in the future is non-existent, due to the hardcodes, upgrading all upgrades are automatically immediately possible contrary to protocol's intention, this is also heavily dependent on the documentations around this, as generally for `GenesisUpgrade`, the upgradeTimestamp 0 is an ok value, as it can and should be executed immediately after chain genesis, but that's not the case for all instances

### Recommended Mitigation Steps

Consider allowing `upgradeTimestamp` to be set to a different value other than `0`, additionally consider allowing `protocolVersion` to be a passed in value.

## QA-18 The placeholder `_postUpgrade()` has no implementation and is not meant to be used but is being queried twice via both the genesis and normal upgrade pattern

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L265-L269

```solidity
    /// @notice placeholder function for custom logic for post-upgrade logic.
    /// Typically this function will never be used.
    /// @param _customCallDataForUpgrade Custom data for an upgrade, which may be interpreted differently for each
    /// upgrade.
    function _postUpgrade(bytes calldata _customCallDataForUpgrade) internal virtual {}
```

Evidently, we can see that this function is not to be used as it currently has no implementation and an empty block, but it's being queried twice via both the genesis and normal upgrade pattern consider these 2 instances, 1- https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L65-L66, & 2 - https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L85-L86

Now would be key to note that where as the `postUpgradeCalldata` would usually be empty it's not always the case and is actually the custom calldata for post upgrade hook which would be interpreted differently dependent on the upgrade

### Impact

Inability to implement any post upgrade calldata whenever `postUpgradeCalldata` is empty as the `_postUpgrade()` function lacks an implementation.

> Submitting as QA due to the "Typically this function will never be used" comment

### Recommended Mitigation Steps

Introduce a functionality to implement a post upgrade custom call data, as suggested by the docs, this should be via an implementation of `_postUpgrade()`.

## QA-19 New instances of missing natspec comments

### Proof of Concept

Multiple instances of this

- Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L527-L605

```solidity
    /*//////////////////////////////////////////////////////////////
                            ERA LEGACY FUNCTIONS
    //////////////////////////////////////////////////////////////*/

    /// @notice Initiates a deposit by locking funds on the contract and sending the request
    /// of processing an L2 transaction where tokens would be minted.
    /// @dev If the token is bridged for the first time, the L2 token contract will be deployed. Note however, that the
    /// newly-deployed token does not support any custom logic, i.e. rebase tokens' functionality is not supported.
    /// @param _l2Receiver The account address that should receive funds on L2
    /// @param _l1Token The L1 token address which is deposited
    /// @param _amount The total amount of tokens to be bridged
    /// @param _l2TxGasLimit The L2 gas limit to be used in the corresponding L2 transaction
    /// @param _l2TxGasPerPubdataByte The gasPerPubdataByteLimit to be used in the corresponding L2 transaction
    /// @param _refundRecipient The address on L2 that will receive the refund for the transaction.
    /// @dev If the L2 deposit finalization transaction fails, the `_refundRecipient` will receive the `_l2Value`.
    /// Please note, the contract may change the refund recipient's address to eliminate sending funds to addresses
    /// out of control.
    /// - If `_refundRecipient` is a contract on L1, the refund will be sent to the aliased `_refundRecipient`.
    /// - If `_refundRecipient` is set to `address(0)` and the sender has NO deployed bytecode on L1, the refund will
    /// be sent to the `msg.sender` address.
    /// - If `_refundRecipient` is set to `address(0)` and the sender has deployed bytecode on L1, the refund will be
    /// sent to the aliased `msg.sender` address.
    /// @dev The address aliasing of L1 contracts as refund recipient on L2 is necessary to guarantee that the funds
    /// are controllable through the Mailbox, since the Mailbox applies address aliasing to the from address for the
    /// L2 tx if the L1 msg.sender is a contract. Without address aliasing for L1 contracts as refund recipients they
    /// would not be able to make proper L2 tx requests through the Mailbox to use or withdraw the funds from L2, and
    /// the funds would be lost.
    /// @return l2TxHash The L2 transaction hash of deposit finalization.
    function depositLegacyErc20Bridge(
        address _prevMsgSender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount,
        uint256 _l2TxGasLimit,
        uint256 _l2TxGasPerPubdataByte,
        address _refundRecipient
    ) external payable override onlyLegacyBridge nonReentrant returns (bytes32 l2TxHash) {
        require(l2BridgeAddress[ERA_CHAIN_ID] != address(0), "ShB b. n dep");
        require(_l1Token != l1WethAddress, "ShB: WETH deposit not supported 2");

        // Note that funds have been transferred to this contract in the legacy ERC20 bridge.
        if (!hyperbridgingEnabled[ERA_CHAIN_ID]) {
            chainBalance[ERA_CHAIN_ID][_l1Token] += _amount;
        }

        bytes memory l2TxCalldata = _getDepositL2Calldata(_prevMsgSender, _l2Receiver, _l1Token, _amount);

        {
            // If the refund recipient is not specified, the refund will be sent to the sender of the transaction.
            // Otherwise, the refund will be sent to the specified address.
            // If the recipient is a contract on L1, the address alias will be applied.
            address refundRecipient = _refundRecipient;
            if (_refundRecipient == address(0)) {
                refundRecipient = _prevMsgSender != tx.origin
                    ? AddressAliasHelper.applyL1ToL2Alias(_prevMsgSender)
                    : _prevMsgSender;
            }

            L2TransactionRequestDirect memory request = L2TransactionRequestDirect({
                chainId: ERA_CHAIN_ID,
                l2Contract: l2BridgeAddress[ERA_CHAIN_ID],
                mintValue: msg.value, // l2 gas + l2 msg.Value the bridgehub will withdraw the mintValue from the base token bridge for gas
                l2Value: 0, // L2 msg.value, this contract doesn't support base token deposits or wrapping functionality, for direct deposits use bridgehub
                l2Calldata: l2TxCalldata,
                l2GasLimit: _l2TxGasLimit,
                l2GasPerPubdataByteLimit: _l2TxGasPerPubdataByte,
                factoryDeps: new bytes[](0),
                refundRecipient: refundRecipient
            });
            l2TxHash = bridgehub.requestL2TransactionDirect{value: msg.value}(request);
        }

        bytes32 txDataHash = keccak256(abi.encode(_prevMsgSender, _l1Token, _amount));
        // Save the deposited amount to claim funds on L1 if the deposit failed on L2
        depositHappened[ERA_CHAIN_ID][l2TxHash] = txDataHash;

        emit LegacyDepositInitiated(ERA_CHAIN_ID, l2TxHash, _prevMsgSender, _l2Receiver, _l1Token, _amount);
    }

```

Evidently we can see that for the @param `_prevMsgSender` nothing is being explained.

- Another instance to look at would be this https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L146-L170

```solidity
    /// @notice Allows bridgehub to acquire mintValue for L1->L2 transactions.
    /// @dev If the corresponding L2 transaction fails, refunds are issued to a refund recipient on L2.
    function bridgehubDepositBaseToken(
        uint256 _chainId,
        address _prevMsgSender,
        address _l1Token,
        uint256 _amount
    ) external payable virtual onlyBridgehubOrEra(_chainId) {
        if (_l1Token == ETH_TOKEN_ADDRESS) {
            require(msg.value == _amount, "L1SharedBridge: msg.value not equal to amount");
        } else {
            // The Bridgehub also checks this, but we want to be sure
            require(msg.value == 0, "ShB m.v > 0 b d.it");

            uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount); // note if _prevMsgSender is this contract, this will return 0. This does not happen.
            require(amount == _amount, "3T"); // The token has non-standard transfer logic
        }

        if (!hyperbridgingEnabled[_chainId]) {
            chainBalance[_chainId][_l1Token] += _amount;
        }
        // Note that we don't save the deposited amount, as this is for the base token, which gets sent to the refundRecipient if the tx fails
        emit BridgehubDepositBaseTokenInitiated(_chainId, _prevMsgSender, _l1Token, _amount);
    }

```

The `onlyBridgehubOrEra` modifier has been used and as such the documentation should entail that it "Allows bridgehub **or era** to acquire mintValue for L1->L2 "transactions.

- Another one to consider would be https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L488-L527

```solidity
    function _parseL2WithdrawalMessage(
        uint256 _chainId,
        bytes memory _l2ToL1message
    ) internal view returns (address l1Receiver, address l1Token, uint256 amount) {
        // We check that the message is long enough to read the data.
        // Please note that there are two versions of the message:
        // 1. The message that is sent by `withdraw(address _l1Receiver)`
        // It should be equal to the length of the bytes4 function signature + address l1Receiver + uint256 amount = 4 + 20 + 32 = 56 (bytes).
        // 2. The message that is sent by `withdrawWithMessage(address _l1Receiver, bytes calldata _additionalData)`
        // It should be equal to the length of the following:
        //@audit
        // bytes4 function signature + address l1Receiver + uint256 amount + address l2Sender + bytes _additionalData =
        // = 4 + 20 + 32 + 32 + _additionalData.length >= 68 (bytes).

        // So the data is expected to be at least 56 bytes long.
        require(_l2ToL1message.length >= 56, "ShB wrong msg len"); // wrong messsage length

        (uint32 functionSignature, uint256 offset) = UnsafeBytes.readUint32(_l2ToL1message, 0);
        if (bytes4(functionSignature) == IMailbox.finalizeEthWithdrawal.selector) {
            // this message is a base token withdrawal
            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
            l1Token = bridgehub.baseToken(_chainId);
        } else if (bytes4(functionSignature) == IL1ERC20Bridge.finalizeWithdrawal.selector) {
            // We use the IL1ERC20Bridge for backward compatibility with old withdrawals.

            // this message is a token withdrawal

            // Check that the message length is correct.
            // It should be equal to the length of the function signature + address + address + uint256 = 4 + 20 + 20 + 32 =
            // 76 (bytes).
            require(_l2ToL1message.length == 76, "ShB wrong msg len 2");
            (l1Receiver, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
            (l1Token, offset) = UnsafeBytes.readAddress(_l2ToL1message, offset);
            (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
        } else {
            revert("ShB Incorrect message function selector");
        }
    }
```

Evidently, in this case, we can see that the math around `// bytes4 function signature + address l1Receiver + uint256 amount + address l2Sender + bytes _additionalData =  // = 4 + 20 + 32 + 32 + _additionalData.length >= 68 (bytes).` is wrong and `68` in this case should be `88` instead.

### Impact

Incomplete code documentation, makes it harder to understand code

### Recommended Mitigation Steps

Apply all suffiecient natspec explanations where necessary.

## QA-20 Setters do not have `equality/zero` checkers

### Proof of Concept

There are multiple instances where protocol does not validate input data, to list a few, take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L248-L260

```solidity
    /// @dev Changes the minimum timelock duration for future operations.
    /// @param _newDelay The new minimum delay time (in seconds) for future operations.
    function updateDelay(uint256 _newDelay) external onlySelf {
        emit ChangeMinDelay(minDelay, _newDelay);
        minDelay = _newDelay;
    }

    /// @dev Updates the address of the security council.
    /// @param _newSecurityCouncil The address of the new security council.
    function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
        emit ChangeSecurityCouncil(securityCouncil, _newSecurityCouncil);
        securityCouncil = _newSecurityCouncil;
    }
```

Evidently, these functions are used for updating governance values, but no checks exist on making sure that the values being passed are not the same as the stored value for these variables.

- Another instance can be seen here: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/ContractDeployer.sol#L62-L70

```solidity
    /// @notice Update the used version of the account.
    /// @param _version The new version of the AA protocol to use.
    /// @dev Note that it allows changes from account to non-account and vice versa.
    function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {
        accountInfo[msg.sender].supportedAAVersion = _version;

        emit AccountVersionUpdated(msg.sender, _version);
    }

```

As we can see, there's no verification that`_version` is different from `accountInfo[msg.sender].supportedAAVersion` or not being `0`


### Impact

No input validation in this case leading to an unnecessary execution of code if the value is the same, or even if it's zero

### Recommended Mitigation Steps

Implement equality checkers in setter functions.

## QA-21 Multiple instances of where messages within `require` are not descriptive

### Proof of Concept

This is fairly rampant in code, taking the `Admin.sol` as the primary case to prove this bug
Take a look at these instances

```solidity
        require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights


        require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");


        require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");


        require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already


```

Other instances can be scoped out by using this search keyword: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+require%28+NOT+language%3ATypeScript+NOT+language%3AMarkdown&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+require%28+NOT+language%3ATypeScript+NOT+language%3AMarkdown&type=code)

### Impact

Where as some instances have the errored out cases commented out it still does not provide a descriptive case for the `require()` and as such this causes lack of understnading of protocol

### Recommended Mitigation Steps

Consider adding descriptive messages after each `require()`



## QA-22 Deviation from Solidity best styling practices in scoped contracts



### Proof of Concept

Multiple instances of going against the best styling practices one of such can be seen in Executor.sol

Take a look athttps://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L6

```solidity
import {COMMIT_TIMESTAMP_NOT_OLDER, COMMIT_TIMESTAMP_APPROXIMATION_DELTA, EMPTY_STRING_KECCAK, L2_TO_L1_LOG_SERIALIZE_SIZE, MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, PACKED_L2_BLOCK_TIMESTAMP_MASK, PUBLIC_INPUT_SHIFT, POINT_EVALUATION_PRECOMPILE_ADDR} from "../../../common/Config.sol";
```

Covers the whole screen which should instead include a line break for better readability
### Impact

Difficulties while reading through code
### Recommended Mitigation Steps

Follow best styling practices

## QA-23 Remove unnecessary code irrelevant to final production

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L51

```solidity
        // While this does not provide a protection in the production, it is needed for local testing
        // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
        assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32);
```

This check is used to ensure that the length of the L2Log encoding is not equal to the length of other L2Logs' tree nodes preimages, but according to the code comment, we know that the check is only in place for testing purposes, also from [here](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L8-L12) we can see that this is a constant value set as `88`.

### Impact

Bad code structure, unnecessary code irrelevant to the production is being left in protocol.

### Recommended Mitigation Steps

Remove this assertion from final realesed code.

## QA-24 Alpha period code is still in production despite the period ending in April 2023

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L35-L39

```solidity
/// @dev The amount of time in seconds the validator has to process the priority transaction
/// NOTE: The constant is set to zero for the Alpha release period
//@audit this is still 0?
uint256 constant PRIORITY_EXPIRATION = 0 days;

```

Evidently, the PRIORITY_EXPIRATION is set to zero, but this is meant for the Alpha release period which ended in April, now consider https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L258-L287

```solidity
    function _requestL2Transaction(
        uint256 _mintValue,
        WritePriorityOpParams memory _params,
        bytes memory _calldata,
        bytes[] memory _factoryDeps
    ) internal returns (bytes32 canonicalTxHash) {
        require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "uj");
        _params.txId = s.priorityQueue.getTotalPriorityTxs();


        // Checking that the user provided enough ether to pay for the transaction.
        // Using a new scope to prevent "stack too deep" error


        _params.l2GasPrice = _deriveL2GasPrice(tx.gasprice, _params.l2GasPricePerPubdata);
        uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
        require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost


        // If the `_refundRecipient` is not provided, we use the `_sender` as the recipient.
        address refundRecipient = _params.refundRecipient == address(0) ? _params.sender : _params.refundRecipient;
        // If the `_refundRecipient` is a smart contract, we apply the L1 to L2 alias to prevent foot guns.
        if (refundRecipient.code.length > 0) {
            refundRecipient = AddressAliasHelper.applyL1ToL2Alias(refundRecipient);
        }
        _params.refundRecipient = refundRecipient;


        // populate missing fields
        //@audit
        _params.expirationTimestamp = uint64(block.timestamp + PRIORITY_EXPIRATION); // Safe to cast
        _params.valueToMint = _mintValue;


        canonicalTxHash = _writePriorityOp(_params, _calldata, _factoryDeps);
    }
```

We can see that the deadline parameter uses this value "PRIORITY_EXPIRATION" to determine the deadline for the validators to process this transaction, but the value being 0 would mean that all transaction would use the timestamp the transaction was requested, which would be logically flawed.

### Impact

Outdated code still in production.

### Recommended Mitigation Steps

Since the Alpha release period has passed, the necessary value for `PRIORITY_EXPIRATION`should be passed and stored in `Config.sol`

## QA-25 Redeployment considerations for `L2ContractHelper/Config.sol` in case of updates

### Proof of Concept

Several functions and constants within `L2ContractHelper/Config.sol` are utilized by multiple Diamond facets across the smart contract system. Modifications to these shared elements necessitate Governor intervention to update all relevant facets. Non-compliance can lead to inconsistencies and potentially critical issues due to mismatched functionality across facets.

A search using the following query confirms this concern:[https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+L2ContractHelper.hashL2Bytecode&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+L2ContractHelper.hashL2Bytecode&type=code)

The search results demonstrate that the `hashL2Bytecode` function is employed within various facets, including `BaseZkSyncUpgrade.sol`, `Mailbox.sol`, `L1ERC20Bridge.sol`, and `L1EthBridge.sol`. Consequently, a change to `hashL2Bytecode` would necessitate redeploying all four of these facets.

### Impact

Low

### Recommended Mitigation Steps

To eliminate the need for widespread redeployments upon updates to `L2ContractHelper` and `Config.sol`, we propose integrating them as Diamond facets themselves. This approach enables other facets to access the functions and constants through cross-facet calls, while external contracts can interact with them via the Diamond. With this structure, modifications only require redeploying and replacing the specific facet containing the updated elements.

This mitigation strategy streamlines the update process for shared functionalities, minimizing the need for extensive redeployment across multiple facets.

## QA-26 `L1SharedBridge.sol`might encounter accounting errors

### Proof of Concept

Take a look at the new implementation of the Shared Bridge and how tokens are gotten from the legacy bridge, https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L115-L136

```solidity
    /// @dev tranfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process
    function transferFundsFromLegacy(address _token, address _target, uint256 _targetChainId) external onlyOwner {
        if (_token == ETH_TOKEN_ADDRESS) {
            uint256 balanceBefore = address(this).balance;
            IMailbox(_target).transferEthToSharedBridge();
            uint256 balanceAfter = address(this).balance;
            require(balanceAfter > balanceBefore, "ShB: 0 eth transferred");
            chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] =
                chainBalance[_targetChainId][ETH_TOKEN_ADDRESS] +
                balanceAfter -
                balanceBefore;
        } else {
            uint256 balanceBefore = IERC20(_token).balanceOf(address(this));
            uint256 amount = IERC20(_token).balanceOf(address(legacyBridge));
            require(amount > 0, "ShB: 0 amount to transfer");
            IL1ERC20Bridge(_target).tranferTokenToSharedBridge(_token, amount);
            uint256 balanceAfter = IERC20(_token).balanceOf(address(this));
            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
            chainBalance[_targetChainId][_token] = chainBalance[_targetChainId][_token] + amount;
        }
    }

```

Now this function calls https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L63-L69

```solidity
    function tranferTokenToSharedBridge(address _token, uint256 _amount) external {
        require(msg.sender == address(sharedBridge), "Not shared bridge");
        uint256 amount = IERC20(_token).balanceOf(address(this));
        require(amount == _amount, "Incorrect amount");
        IERC20(_token).safeTransfer(address(sharedBridge), amount);
    }

```

Case with this implementation is [the line](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L132)

```solidity
            require(balanceAfter - balanceBefore == amount, "ShB: wrong amount transferred");
```

This automatically means that all fee on transfer tokens sre not supported, cause now while transfering the funds, as far as the fee is charged the difference between the former balance and the new balance is not going to be the same, and as such this attempt to transfer the funds would always revert, note that protocol can't also specify a lower amount to be sent due to the check that ensures the whole balance is sent.

Now whereas protocol does not work cyrretly with `FOT` tokens, there are tokens that exist that could have their implementations be update to support fees, effectively breaking protocol if that were to happen.

### Impact

Funds are potentially stuck in the ERC20 bridge, also core functionality is broken, being that `transferFundsFromLegacy()` won't work for these tokens.

### Recommended Mitigation Steps

In as much as the aim of transfering these tokens from the ERC20 bridge is to clear the bridge of the tokens in it, then the finalization check could be changed from `balanceAfter - balanceBefore == amount` and instead implemented as a check that ensures that `IERC20(_token).balanceOf(address(legacyBridge)) == 0` after the transaction.

## QA-27 The `Ecrecover` gas cost been massively increased without significant increases in executional cost

### Proof of Concept

Take a look at the gas cost for ecrecover https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/precompiles/Ecrecover.yul#L22-L25

```yul
            /// @dev The gas cost of processing ecrecover circuit precompile.
            function ECRECOVER_GAS_COST() -> ret {
                ret := 7000
            }
```

It's been massively increased to more than `6x` it's former cost of `1112`, would be key to note that the execution of this contract is still the same without any execessive additional hashing/compiling that justifies this addition.

### Impact

Users are now charged `>6x` the charges to `ECRECOVER` where as there are no real stand out addition in executional costs.

### Recommended Mitigation Steps

Consider reducing this cost or always attach extensive documentation whenever an update happens to a variable, especially the ones attached to costs.

## QA-28 zkEVM's `CodeOracle` Precompile somewhat deviates from EVM's `extcodecopy` behavior

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/precompiles/CodeOracle.yul#L4

```yul
 * @notice The contract used to emulate EVM's `extcodecopy` behavior.

```

We can see that this function is to emulate EVM extcodecopy behaviour, but it contatns multiple deviation to the etheruem's native implementation, to list a few:

- **Memory Management:** `extcodecopy` allows specifying the destination memory location. `CodeOracle` relies on zkEVM's internal memory management, potentially reusing the same memory page for subsequent decommits, leading to caching issues.
- **Functionality:** Unlike `extcodecopy` which copies a specific size of code, `CodeOracle` decommits the entire code based on a versioned hash stored in a separate contract.
- **Error Handling:** `extcodecopy` handles out-of-gas situations during memory access. `CodeOracle` might not handle such cases, potentially leading to unexpected behavior.

### Impact

Borderline medium/low, since this is a deviation from Ethereum's specific implementation and would lead to confusion

### Recommended Mitigation Steps

Consider making it very similar to Ethereum's implementation or clearly document the deviation.

## QA-29 Protocol currently does not consider all windows in regards to `minDelay`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L250-L253

```solidity
    function updateDelay(uint256 _newDelay) external onlySelf {
        emit ChangeMinDelay(minDelay, _newDelay);
        minDelay = _newDelay;
    }
```

The `updateDelay` function within the Governance contract lacks a minimum threshold for the `_newDelay` parameter, which controls the `minDelay` value. If `_newDelay` gets set to say zero for instance, this effectively removes the security council's oversight.

This lack of synchronization between different time delays used in the upgrade scheduling process creates the possibility of conflicting scenarios. These delays are defined in separate contracts, i.e `minDelay` and `UPGRADE_NOTICE_PERIOD` in `Governance.sol` & `executionDelay` in `ValidatorTimelock.sol`

If `executionDelay` exceeds `minDelay` or `UPGRADE_NOTICE_PERIOD`, the upgrade might be executed on L1 before users can withdraw their funds. Even if `executionDelay` is shorter than `minDelay`, a malicious validator could intentionally delay the process, causing a similar issue.

### Impact

These loopholes in the zkSync governance contracts could be exploited to manipulate the upgrade process and potentially harm users.

One window allows the ownerto bypass the security council's oversight by setting the minimum approval delay for operations to zero. This timeframe, known as `minDelay`, is crucial because it gives the security council time to review and potentially cancel operations proposed by the admin. With `minDelay` at zero, the security council's approval becomes irrelevant, and the admin can execute operations unilaterally. This undermines the two-actor security model intended for governance.

> NB: It might as well not be `zero`, but a very short time frame, idea is still the same.

Another window stems from inconsistencies between different time delays used during upgrade scheduling. These delays include `minDelay` (time for security council review), `UPGRADE_NOTICE_PERIOD` (user notification window), and `executionDelay` (delay before upgrade execution on L1). If `minDelay` or `UPGRADE_NOTICE_PERIOD` are shorter than `executionDelay`, it can lead to unpredictable outcomes for users. Users' withdrawal requests might be stuck in limbo or executed before the upgrade, causing them to miss out on crucial information or protections.

For instance, the time delay inconsistencies could be problematic to the upgrade process in a way that impacts users attempting to withdraw ETH before an upgrade, say the `finalizeEthWithdrawal()` gets updgraded to function a bit different, users who had their transactions going on would be directly impacted

### Recommended Mitigation Steps

Enforce minimum `minDelay`, the `updateDelay` function should be modified to include a requirement that `_newDelay` be greater than `ValidatorTimelock.executionDelay()` with an additional buffer of at least 2 days to account for potential validator delays. This ensures the security council has sufficient time to review operations.

Also, consider establishing a dependency between `minDelay` (or `UPGRADE_NOTICE_PERIOD`) and `executionDelay`. This could involve enforcing `minDelay` to be always greater than `executionDelay` with a reasonable buffer.


 

## QA-30 `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion()` should not allow the protocol version difference to be up to `MAX_ALLOWED_PROTOCOL_VERSION_DELTA`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L42

```solidity
    function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
        uint256 previousProtocolVersion = s.protocolVersion;
        require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
        require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );

        // If the previous upgrade had an L2 system upgrade transaction, we require that it is finalized.
        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
        require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );

        s.protocolVersion = _newProtocolVersion;
        emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
    }

```

Considering the only change between this and the non-Genesis `BaseZkSyncUpgrade` is the fact that the protocol version is allowed to be set to the current one, i.e `//Genesis Upgrade difference: Note this is the only thing change > to >= _newProtocolVersion >= previousProtocolVersion, "New protocol version is not greater than the current one"`, i.e then to be in [alliance with Config.sol](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Config.sol#L30-L34) of allowing 100 as a delta, then the difference needs to be dropped by 1, since the lower end of the possible values has been reduced to accept `previousProtocolVersion`.

### Impact

Non-critical, just to be more in allignment with the `Config.sol`

### Recommended Mitigation Steps

Consider reimplementing the logic for the genesis upgrade.

## QA-31 Users failed tx could be unclaimable from the shared bridge

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L302-L369

```solidity
    /// @dev Processes claims of failed deposit, whether they originated from the legacy bridge or the current system.
    function _claimFailedDeposit(
        bool _checkedInLegacyBridge,
        uint256 _chainId,
        address _depositSender,
        address _l1Token,
        uint256 _amount,
        bytes32 _l2TxHash,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes32[] calldata _merkleProof
    ) internal nonReentrant {
        {
            bool proofValid = bridgehub.proveL1ToL2TransactionStatus(
                _chainId,
                _l2TxHash,
                _l2BatchNumber,
                _l2MessageIndex,
                _l2TxNumberInBatch,
                _merkleProof,
                TxStatus.Failure
            );
            require(proofValid, "yn");
        }
        require(_amount > 0, "y1");

        {
            bool notCheckedInLegacyBridgeOrWeCanCheckDeposit;
            {
                // Deposits that happened before the upgrade cannot be checked here, they have to be claimed and checked in the legacyBridge
                bool weCanCheckDepositHere = !_isEraLegacyWithdrawal(_chainId, _l2BatchNumber);
                // Double claims are not possible, as we this check except for legacy bridge withdrawals
                // Funds claimed before the update will still be recorded in the legacy bridge
                // Note we double check NEW deposits if they are called from the legacy bridge
                notCheckedInLegacyBridgeOrWeCanCheckDeposit = (!_checkedInLegacyBridge) || weCanCheckDepositHere;
            }
            if (notCheckedInLegacyBridgeOrWeCanCheckDeposit) {
                bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
                bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
                require(dataHash == txDataHash, "ShB: d.it not hap");
                delete depositHappened[_chainId][_l2TxHash];
            }
        }

        if (!hyperbridgingEnabled[_chainId]) {
            // check that the chain has sufficient balance
            require(chainBalance[_chainId][_l1Token] >= _amount, "ShB n funds");
            chainBalance[_chainId][_l1Token] -= _amount;
        }

        // Withdraw funds
        if (_l1Token == ETH_TOKEN_ADDRESS) {
            bool callSuccess;
            // Low-level assembly call, to avoid any memory copying (save gas)
            assembly {
                callSuccess := call(gas(), _depositSender, _amount, 0, 0, 0, 0)
            }
            require(callSuccess, "ShB: claimFailedDeposit failed");
        } else {
            IERC20(_l1Token).safeTransfer(_depositSender, _amount);
            // Note we don't allow weth deposits anymore, but there might be legacy weth deposits.
            // until we add Weth bridging capabilities, we don't wrap/unwrap weth to ether.
        }

        emit ClaimedFailedDepositSharedBridge(_chainId, _depositSender, _l1Token, _amount);
    }

```

Function is inevitably called when claiming the failed deposits,c ase here is that the logic for this hardcodes the receiver and expects it to be able to dela with the tokens, now different things could eb the cause of the address not being able to handle tokesn, for example say the `_depositSender` can't handle eth or has no receicve function, or for the case of a normal token, assume they get blacklisted or some other sort of issues, tokens are indefinitely locked in the bridge.

### Impact

Low, since this somewhat relies on user not using an address that can accept their failed deposits from the get go.

### Recommended Mitigation Steps

As a popular receommendation, it's advisable to implement a pull method for withdrawals, i.e users should be allowed to provide a fresh deposit address than forcing it into the one that made the deposit.

> NB: Whereas acknowledged findings have been said to be OOS, I'm considering a fresh case of the bug and submitting since this is a new contract and hasn't been reported before.

## QA-32 Apply fixes to commented out bug cases

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L67-L89

```solidity
    function upgrade(ProposedUpgrade calldata _proposedUpgrade) public virtual returns (bytes32 txHash) {
        // Note that due to commitment delay, the timestamp of the L2 upgrade batch may be earlier than the timestamp
        // of the L1 block at which the upgrade occurred. This means that using timestamp as a signifier of "upgraded"
        // on the L2 side would be inaccurate. The effects of this "back-dating" of L2 upgrade batches will be reduced
        // as the permitted delay window is reduced in the future.
        require(block.timestamp >= _proposedUpgrade.upgradeTimestamp, "Upgrade is not ready yet");

        _setNewProtocolVersion(_proposedUpgrade.newProtocolVersion);
        _upgradeL1Contract(_proposedUpgrade.l1ContractsUpgradeCalldata);
        _upgradeVerifier(_proposedUpgrade.verifier, _proposedUpgrade.verifierParams);
        _setBaseSystemContracts(_proposedUpgrade.bootloaderHash, _proposedUpgrade.defaultAccountHash);

        txHash = _setL2SystemContractUpgrade(
            _proposedUpgrade.l2ProtocolUpgradeTx,
            _proposedUpgrade.factoryDeps,
            _proposedUpgrade.newProtocolVersion
        );

        _postUpgrade(_proposedUpgrade.postUpgradeCalldata);

        emit UpgradeComplete(_proposedUpgrade.newProtocolVersion, txHash, _proposedUpgrade);
    }

```

We can see that while upgrading, the call gets routed to ` _upgradeVerifier() -> _setVerifier() -> _setVerifierParams()`, now issue here is that, as [commented](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L143-L147) an upgrade must be carefully done to ensure there aren't batches in the committed state during the transition, this is in order not to have the verifier be immediately used to prove all committed batches.

But this can easily be fixed by applying an equivalence check while upgrading, i.e `require(s.totalBatchesCommitted == s.totalBatchesVerified);`

### Impact

Admin error, but wrong verifier could be used to prove batches being committed in the transition state.

### Recommended Mitigation Steps

Introduce the check `require(s.totalBatchesCommitted == s.totalBatchesVerified);` to ensure this never happens.

## QA-33 Unnecessary duplication of checks

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L386-L456

```solidity
    function finalizeWithdrawal() external override {
        // To avoid rewithdrawing txs that have already happened on the legacy bridge.
        // Note: new withdraws are all recorded here, so double withdrawing them is not possible.
        //@audit
        if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
            require(!legacyBridge.isWithdrawalFinalized(_l2BatchNumber, _l2MessageIndex), "ShB: legacy withdrawal");
        }
        _finalizeWithdrawal(_chainId, _l2BatchNumber, _l2MessageIndex, _l2TxNumberInBatch, _message, _merkleProof);
    }

    /// @dev Internal function that handles the logic for finalizing withdrawals,
    /// serving both the current bridge system and the legacy ERC20 bridge.
    function _finalizeWithdrawal() internal nonReentrant returns (address l1Receiver, address l1Token, uint256 amount) {
        require(!isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex], "Withdrawal is already finalized");
        isWithdrawalFinalized[_chainId][_l2BatchNumber][_l2MessageIndex] = true;

        // Handling special case for withdrawal from zkSync Era initiated before Shared Bridge.
        //@audit
        if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
            // Checks that the withdrawal wasn't finalized already.
            bool alreadyFinalized = IGetters(ERA_DIAMOND_PROXY).isEthWithdrawalFinalized(
                _l2BatchNumber,
                _l2MessageIndex
            );
            require(!alreadyFinalized, "Withdrawal is already finalized 2");
        }
//ommited for brevity
    }
```

These functions are both used for finalizing the withdrawals, with multiple checks, issue here now is that the check if the transaction is from the era legacy is implemented twice which is unnecessary.

### Impact

NC - Overcomplication of code.

### Recommended Mitigation Steps

The check can be left just to the internal function while finalizing the withdrawal

## QA-34 Non-existent facets would be assumed to be unfreezable due to the wrong conditional keyword in `isFacetFreezable()`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L162-L174

```solidity
    /// @inheritdoc IGetters
    function isFacetFreezable(address _facet) external view returns (bool isFreezable) {
        Diamond.DiamondStorage storage ds = Diamond.getDiamondStorage();

        // There is no direct way to get whether the facet address is freezable,
        // so we get it from one of the selectors that are associated with the facet.
        uint256 selectorsArrayLen = ds.facetToSelectors[_facet].selectors.length;
        //@audit
        if (selectorsArrayLen != 0) {
            bytes4 selector0 = ds.facetToSelectors[_facet].selectors[0];
            isFreezable = ds.selectorToFacet[selector0].isFreezable;
        }
    }

```

This function is used to determine if a facet is freezable, issue here is that it wrongly uses `if()` instead of `require()` now since `if` is used, in the case where the facet is none existent `selectorsArrayLen == 0` would be true and as such the function would return `false` whereas it should revert since the facet is non-existent

### Impact

Users would be confused at this, since there is no difference between unfreezable facets and non-existent ones considering the current implementation of `isFacetFreezable()`

### Recommended Mitigation Steps

Consider changing the `if()` condition to `require()` that way only real unfreezable facets would return `false`.

## QA-35 Remove the trailing comma after queries to `isNotEnoughGasForPubdata` in the bootloader to enforce no error in the Yul Syntax

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L2315-L2320

```yul
                if isNotEnoughGasForPubdata(
                    basePubdataSpent,
                    gas(),
                    reservedGas,
                    gasPerPubdata,
                ) {
```

And https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1833-L1841

```yul
                if isNotEnoughGasForPubdata(
                    basePubdataSpent,
                    gas(),
                    // Note, that for L1->L2 transactions the reserved gas is used to protect the operator from
                    // transactions that might accidentally cause to publish too many pubdata.
                    // Thus, even if there is some accidental `reservedGas` left, it should not be used to publish pubdata.
                    0,
                    gasPerPubdata,
                ) {
```

We can see that tehre is a trailing comma in the function call but this is an invalid syntax according to Yul's formal specification: https://docs.soliditylang.org/en/latest/yul.html#specification-of-yul

Another instance not related to `isNotEnoughGasForPubdata` can be seen here: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L972-L977

### Impact

Borderline low... this is cause the `Bootloader.yul` code would not compile with the correct Yul compiler. Even if it compiles with the current zkEVM implementation, it potentially necessitates an update to the Bootloader.yul code and its hash on Layer 1. Such an update would require a system upgrade.

### Recommended Mitigation Steps

Consider removing the trailing comma in both cases.

## QA-36 Consider rightly passing the elements of the `BridgehubL2TransactionRequest` in `_requestL2Transaction()`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L197-L226

```solidity
    function requestL2Transaction(
        address _contractL2,
        uint256 _l2Value,
        bytes calldata _calldata,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit,
        bytes[] calldata _factoryDeps,
        address _refundRecipient
    ) external payable returns (bytes32 canonicalTxHash) {
        require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
        canonicalTxHash = _requestL2TransactionSender(
            BridgehubL2TransactionRequest({
                sender: msg.sender,
                contractL2: _contractL2,
                mintValue: msg.value,
                l2Value: _l2Value,
                //@audit l2Calldata should come before gas limit
                l2GasLimit: _l2GasLimit,
                l2Calldata: _calldata,
                l2GasPerPubdataByteLimit: _l2GasPerPubdataByteLimit,
                factoryDeps: _factoryDeps,
                refundRecipient: _refundRecipient
            })
        );
        IL1SharedBridge(s.baseTokenBridge).bridgehubDepositBaseToken{value: msg.value}(
            s.chainId,
            msg.sender,
            ETH_TOKEN_ADDRESS,
            msg.value
        );
    }
```

Now take a look at the implementation of the `BridgehubL2TransactionRequest` struct from https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/common/Messaging.sol#L127-L137

```solidity
struct BridgehubL2TransactionRequest {
    address sender;
    address contractL2;
    uint256 mintValue;
    uint256 l2Value;
    bytes l2Calldata;
    uint256 l2GasLimit;
    uint256 l2GasPerPubdataByteLimit;
    bytes[] factoryDeps;
    address refundRecipient;
}
```

One can see that, within the `requestL2Transaction()` exexcution the positions of `l2GasLimit` and the `calldata` bytes are swapped which would cause the ABI encoding/decoding of this struct be faulty or even cause an issue with the generation of the proof of this transaction

### Impact

Better code structure.

### Recommended Mitigation Steps

Consider passing in the struct in the right manner

## QA-37 Resolve newly introduced TODOs

### Proof of Concept

Using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20TODO&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20TODO&type=code) we can see that there are more than 22 code files that are left with multiple todos (a notable mention is that some contracts have only one nonetheless this should be fixed)

### Impact

Open Todos often hint that the codes are not ready for final production/deployment.

### Recommended Mitigation Steps

Fix open todos

 ## QA-38  `OperationState.Waiting` should be considered the case even when `timestamp == block.timestamp`



### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L105

```solidity
    function getOperationState(bytes32 _id) public view returns (OperationState) {
        uint256 timestamp = timestamps[_id];
        if (timestamp == 0) {
            return OperationState.Unset;
        } else if (timestamp == EXECUTED_PROPOSAL_TIMESTAMP) {
            return OperationState.Done;
        } else if (timestamp > block.timestamp) {
            return OperationState.Waiting;
        } else {
            return OperationState.Ready;
        }
    }


```

As seen this function is used to get the operation states of any operation, one thing to note is that the function is supposed to consider the operation pending only `after the timestamp has passed block.timestamp` but in the current implementation even when `timestamp == block.timestamp` the state would be `Ready` instead of `Waiting`
### Impact

Low, info on better code structure
### Recommended Mitigation Steps

Make the `OperationState.Waiting` check inclusive.

## QA-39 Redundant return of the nonce deployed

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/NonceHolder.sol#L122-L131

```solidity
    function getDeploymentNonce(address _address) external view returns (uint256 deploymentNonce) {
        uint256 addressAsKey = uint256(uint160(_address));
        (deploymentNonce, ) = _splitRawNonce(rawNonces[addressAsKey]);

        return deploymentNonce;
    }

```

Function is returning the deployment nonce for the accounts used with the CREATE opcode, case with this is that the variable to be returned is already named, but execution still passes a `return`

### Impact

Redundant code, bad structure

### Recommended Mitigation Steps

Always remove redundant code from production code.

## QA-40 Chunking the pubdata should be made more efficient

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/PubdataChunkPublisher.sol#L21-L57

```solidity
    function chunkAndPublishPubdata(bytes calldata _pubdata) external onlyCallFrom(address(L1_MESSENGER_CONTRACT)) {
        require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");

        bytes32[] memory blobHashes = new bytes32[](MAX_NUMBER_OF_BLOBS);

        // We allocate to the full size of MAX_NUMBER_OF_BLOBS * BLOB_SIZE_BYTES because we need to pad
        // the data on the right with 0s if it doesn't take up the full blob
        bytes memory totalBlobs = new bytes(BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS);

        assembly {
            // The pointer to the allocated memory above. We skip 32 bytes to avoid overwriting the length.
            let ptr := add(totalBlobs, 0x20)
            calldatacopy(ptr, _pubdata.offset, _pubdata.length)
        }

        for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
            uint256 start = BLOB_SIZE_BYTES * i;

            // We break if the pubdata isn't enough to cover 2 blobs. On L1 it is expected that the hash
            // will be bytes32(0) if a blob isn't going to be used.
            if (start >= _pubdata.length) {
                break;
            }

            bytes32 blobHash;
            assembly {
                // The pointer to the allocated memory above skipping the length.
                let ptr := add(totalBlobs, 0x20)
                blobHash := keccak256(add(ptr, start), BLOB_SIZE_BYTES)
            }

            blobHashes[i] = blobHash;
        }

        SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_ONE_HASH_KEY)), blobHashes[0]);
        SystemContractHelper.toL1(true, bytes32(uint256(SystemLogKey.BLOB_TWO_HASH_KEY)), blobHashes[1]);
    }
```

Function is used to chunk pubdata into pieces that can fit into blobs, case is that it queries to `constant variables` and then multiplies, when this value can just be hardcoded to the codebase, i.e this line `require(_pubdata.length <= BLOB_SIZE_BYTES * MAX_NUMBER_OF_BLOBS, "pubdata should fit in 2 blobs");`, both `BLOB_SIZE_BYTES` and `MAX_NUMBER_OF_BLOBS` have fixed numbers of `2` and `126976` respectively as gotten from https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol

This means that the check could be changed to `require(_pubdata.length <= 253_952 "pubdata should fit in 2 blobs");`

### Impact

Wastage of gas

### Recommended Mitigation Steps

Consider making the change in as much as the values are going to be constants

## QA-41 Owner can still access `renounceOwnership()`

### Proof of Concept

The `Governance.sol` contract, which plays a pivotal role in managing governance operations within the zkSync protocol, is designed to inherit both the `IGovernance` interface and the `Ownable2Step` contract. During the contract's deployment, the initial ownership is assigned to the `_admin` address through the `Governance.constructor`:

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L43-L45

```solidity
_transferOwnership(_admin);
```

This design ensures that critical functions, such as `scheduleTransparent` and `scheduleShadow`, are exclusively accessible by the `_admin` (owner) of the contract. However, the incorporation of the `Ownable2Step` contract, which extends the `Ownable` abstract contract, introduces a significant risk. The `Ownable` contract includes a `renounceOwnership` function allowing the current owner to relinquish ownership rights, effectively setting the owner to the zero address:

```solidity
function renounceOwnership() public virtual onlyOwner {
    _transferOwnership(address(0));
}
```

If the `_admin` executes the `renounceOwnership` function, it would render all owner-exclusive functionalities, including upgrade scheduling, inoperative, thereby crippling the entire zkSync protocol.

### Impact

By renouncing ownership, the `_admin` could unilaterally disable key governance functionalities. Such an action would not only undermine the protocol's integrity but also eliminate any possibility of future upgrades, posing a severe threat to the system's sustainability and security.

### Recommended Mitigation Steps

To safeguard the protocol against potential sabotage through ownership renunciation, it is advisable to override the `renounceOwnership` function within the `Governance.sol` contract. By explicitly reverting any attempts to renounce ownership, this modification ensures the continuity and inviolability of governance operations:

```solidity
function renounceOwnership() public override onlyOwner {
    revert("_admin cannot renounce ownership");
}
```

## QA-42 There exist a light deviation between the Ethereum VM and zK's in regards to eth deposits

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L197-L227

```solidity
    function requestL2Transaction(
        //@audit
        address _contractL2,
        uint256 _l2Value,
        bytes calldata _calldata,
        uint256 _l2GasLimit,
        uint256 _l2GasPerPubdataByteLimit,
        bytes[] calldata _factoryDeps,
        //@audit
        address _refundRecipient
    ) external payable returns (bytes32 canonicalTxHash) {
        require(s.chainId == ERA_CHAIN_ID, "legacy interface only available for era token");
        canonicalTxHash = _requestL2TransactionSender(
            BridgehubL2TransactionRequest({
                sender: msg.sender,
                contractL2: _contractL2,
                mintValue: msg.value,
                l2Value: _l2Value,
                l2GasLimit: _l2GasLimit,
                l2Calldata: _calldata,
                l2GasPerPubdataByteLimit: _l2GasPerPubdataByteLimit,
                factoryDeps: _factoryDeps,
                refundRecipient: _refundRecipient
            })
        );
        IL1SharedBridge(s.baseTokenBridge).bridgehubDepositBaseToken{value: msg.value}(
            s.chainId,
            msg.sender,
            ETH_TOKEN_ADDRESS,
            msg.value
        );
    }

```

This mechanism allows users to deposit ETH from L1 to L2 into two separate addresses within zkSync Era, which introduces a unique feature not found in the traditional Ethereum Virtual Machine (EVM) environment.

Users can deposit ETH to a contract address (`_contractL2`) and simultaneously direct a refund to a different recipient address, by specifying a different address from `_contractL2` . This dual-address deposit capability deviates from standard EVM practices, where transfers from an externally owned account (EOA) to two addresses simultaneously are not possible. This feature, specific to the zkSync Era, enables such transactions.

### Impact

Undocumented deviation from the Ethereum's VM

### Recommended Mitigation Steps

To mitigate any potential confusion and enhance security awareness, it's crucial to thoroughly document this dual-address deposit process.

## QA-43 `0.8.20` is vulnerable to some bugs and compiler version should be updated to be on the safe side

### Proof of Concept

See https://github.com/ethereum/solidity/blob/afda6984723fca99e82ebf34d0aec1804f1f3ce6/docs/bugs_by_version.json#L1865-L1871
we can see that this compiler version is vulnerable to:

- Use this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20.selector&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20.selector&type=code), we can see that protocol in multiple instances implement the `.selector()` query, would be key to note that, as explained in [this blog](https://soliditylang.org/blog/2023/07/19/missing-side-effects-on-selector-access-bug/) there are multiple side effects with accessing .selector() for the current compiler version, since it could cause potentially incorrect behavior of contracts compiled using the legacy pipeline.

-Considering the protocol's heavy use of `yul`, a different version of compiler should be used, cause this version is vulnerable to the full inliner non expression split argument evaluation order bug, explained [here](https://blog.soliditylang.org/2023/07/19/full-inliner-non-expression-split-argument-evaluation-order-bug/), do note that this could heavily cause reordering reverts in the bootloader or even it's return may lead to storage writes, memory writes, or event emissions not being performed. It may also lead to the contract not reverting (and therefore not rolling back some operations) when it should or vice-versa, and as such an updated version should be used.

- Lastly, would be key to note that `verbatim` is also used heavily protocol, for example even in the blob versioned hash receiver https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/utils/BlobVersionedHashRetriever.yul but this is also a tad affected by this compiler's verion of being vulnerable to the [verbatim invalid deduplication bug](https://soliditylang.org/blog/2023/11/08/verbatim-invalid-deduplication-bug/), note that the TLDR of this bug as understood is that wherein equivalent assembly blocks are identified and merged. `verbatim` assembly items surrounded by identical opcodes were incorrectly considered identical and unified, that's in the Block Deduplicator optimizer step, currently the `BlobVersionedHashRetriever.yul` only queries the verbatim, just once so no issue of the bug coming in place to unify similar blocks.

### Recommended Mitigation Steps

Consider updating the solididity compiler version

## QA-44 `execute()` & `executeInstant()` could use `msg.value` in a better manner

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L167-L202

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
        emit OperationExecuted(id);
    }

    /// @notice Executes the scheduled operation with the security council instantly.
    /// @dev Only the security council may execute an operation instantly.
    /// @param _operation The operation parameters will be executed with the upgrade.
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
        emit OperationExecuted(id);
    }

        function _execute(Call[] calldata _calls) internal {
        for (uint256 i = 0; i < _calls.length; ++i) {
            (bool success, bytes memory returnData) = _calls[i].target.call{value: _calls[i].value}(_calls[i].data);
            if (!success) {
                // Propagate an error if the call fails.
                assembly {
                    revert(add(returnData, 0x20), mload(returnData))
                }
            }
        }
    }
```

We can see that both functions are marked as payable and then call on the internal `_execute()`, but the codeflow does not assert that the provided `msg.value` is equal to the one that is been expended in `_execut()`.

### Impact

Misappropriation of funds for operations, as if the `msg.value` is less than `call.value`, then funds in the contract for different operations would be used for the current one.

### Recommended Mitigation Steps

Consider requiring that the `msg.value` provided is the `call.value` needed.

## QA-45 `StateTransitionManager.sol::createNewChain()` has some nuances with it's `initData`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L238-L288

```solidity
    /// @notice called by Bridgehub when a chain registers
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

        // check not registered
        Diamond.DiamondCutData memory diamondCut = abi.decode(_diamondCut, (Diamond.DiamondCutData));

        // check input
        bytes32 cutHashInput = keccak256(_diamondCut);
        require(cutHashInput == initialCutHash, "StateTransition: initial cutHash mismatch");

        // construct init data
        bytes memory initData;
        /// all together 4+9*32=292 bytes
        initData = bytes.concat(
            IDiamondInit.initialize.selector,
            bytes32(_chainId),
            bytes32(uint256(uint160(bridgehub))),
            bytes32(uint256(uint160(address(this)))),
            bytes32(uint256(protocolVersion)),
            bytes32(uint256(uint160(_admin))),
            bytes32(uint256(uint160(validatorTimelock))),
            bytes32(uint256(uint160(_baseToken))),
            bytes32(uint256(uint160(_sharedBridge))),
            bytes32(storedBatchZero),
            diamondCut.initCalldata
        );

        diamondCut.initCalldata = initData;
        // deploy stateTransitionContract
        DiamondProxy stateTransitionContract = new DiamondProxy{salt: bytes32(0)}(block.chainid, diamondCut);

        // save data
        address stateTransitionAddress = address(stateTransitionContract);

        stateTransition[_chainId] = stateTransitionAddress;

        // set chainId in VM
        _setChainIdUpgrade(_chainId, stateTransitionAddress);

        emit StateTransitionNewChain(_chainId, stateTransitionAddress);
    }
```

Evidently, the logic for `initData` seems to expect 292 bytes, hence this comment: " /// all together 4+9\*32=292 bytes" but going through the logic below, we can see that the function after passing in the `292` bytes, i.e the selector and all 9 `byte32` elements, it still passes the initData to be concated, which seems as a flawed logic as the whole concated value is later on set as the same `initData`.

### Impact

Bad code strycture, `initData` is expected to be `292` bytes but is accepted to be longer.

### Recommended Mitigation Steps

Consider clearly limiting this to `292` bytes or clearly document that this is to be extended in the future


## QA-46 Double addressed tokens can be stolen from the bridge

### Proof of Concept

While depositing the contract calls to see if the deposits have been cleared with token addresses, case here is that in most of the logic, it doesnt consider that a user can just specify the second address if the first one doesn't go through

### Recommended Mitigation Steps

Consider not supporting these types of tokens

## QA-47 Fix bootloader's documentation in regards to unread memory points

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1937-L1962

```yul
            function shouldMsgValueMimicCallBeSystem(to, dataPtr) -> ret {
                let dataLen := mload(dataPtr)
                // Note, that this point it is not fully known whether it is indeed the selector
                // of the calldata (it might not be the case if the `dataLen` < 4), but it will be checked later on
                let selector := shr(224, mload(add(dataPtr, 32)))

                let isSelectorCreate := or(
                    eq(selector, {{CREATE_SELECTOR}}),
                    eq(selector, {{CREATE_ACCOUNT_SELECTOR}})
                )
                let isSelectorCreate2 := or(
                    eq(selector, {{CREATE2_SELECTOR}}),
                    eq(selector, {{CREATE2_ACCOUNT_SELECTOR}})
                )

                // Firstly, ensure that the selector is a valid deployment function
                ret := or(
                    isSelectorCreate,
                    isSelectorCreate2
                )
                // Secondly, ensure that the callee is ContractDeployer
                ret := and(ret, eq(to, CONTRACT_DEPLOYER_ADDR()))
                // Thirdly, ensure that the calldata is long enough to contain the selector
                ret := and(ret, gt(dataLen, 3))
            }

```

This function returns whether the mimicCall should use the `isSystem` flag, issue here is that this statement ` // Note, that this point it is not fully known whether it is indeed the selector...` and should instead be `// Note that, at this point it is not fully known whether it is indeed the selector...`

### Impact

Bad code structure, harder to understand code since integrators would assume one is talking about the unread memory point at the end of `dataLen`

### Recommended Mitigation Steps

Apply the fix.

## QA-48 Protocol should consider supporting deposits of pure erc20s

### Proof of Concept

Here is how a token's deposit gets finalized: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L97

That is the contract creates the token address if the deposit for this token has never been made, But before that the user needs to deposit their tokens vua the L1 shared bridge.

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L243-L267

```solidity
    function _getDepositL2Calldata(
        address _l1Sender,
        address _l2Receiver,
        address _l1Token,
        uint256 _amount
    ) internal view returns (bytes memory) {
        bytes memory gettersData = _getERC20Getters(_l1Token);
        return abi.encodeCall(IL2Bridge.finalizeDeposit, (_l1Sender, _l2Receiver, _l1Token, _amount, gettersData));
    }

    /// @dev Receives and parses (name, symbol, decimals) from the token contract
    function _getERC20Getters(address _token) internal view returns (bytes memory) {
        if (_token == ETH_TOKEN_ADDRESS) {
            bytes memory name = bytes("Ether");
            bytes memory symbol = bytes("ETH");
            bytes memory decimals = abi.encode(uint8(18));
            return abi.encode(name, symbol, decimals); // when depositing eth to a non-eth based chain it is an ERC20
        }
        //@audit using staticcall for a call that is going to revert? Not all tokens support the name, symbol and decimal getters
        (, bytes memory data1) = _token.staticcall(abi.encodeCall(IERC20Metadata.name, ()));
        (, bytes memory data2) = _token.staticcall(abi.encodeCall(IERC20Metadata.symbol, ()));
        (, bytes memory data3) = _token.staticcall(abi.encodeCall(IERC20Metadata.decimals, ()));
        return abi.encode(data1, data2, data3);
    }

```

This function is inevitably called whenever executing `depositLegacyErc20Bridge()` & `bridgehubDeposit()`, used to generate a calldata for calling the deposit finalization, issue is that while the call is being routed to `_getERC20Getters()` and in the case where the token is not eth, protocol assumes the token implements the `name(), symbol(), & decimals()` function, but contrary to this assumption, these getter functions are not part of the original `EIP20` specification and as such not all tokens support this, causing an attempt get this deposit calldata revert for pure EIP20 tokens.

### Impact

Pure eip-20 tokens are not supported, since there is an inability to execute both `depositLegacyErc20Bridge()` & `bridgehubDeposit()` functions for these tokens

### Recommended Mitigation Steps

Reimplement a logic to allow for the support of pure eip20 tokens

## QA-49 Remove instances of unnecessary casting

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45

```solidity

    /// @return The total number of unprocessed priority operations in a priority queue
    function getSize(Queue storage _queue) internal view returns (uint256) {
        return uint256(_queue.tail - _queue.head);
    }

```

But from [here ](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45) we can see that both `_queue.tail ` & `_queue.head` are of `unit256` already so there's no need for this casting.

### Recommended Mitigation Steps

Remove the unnecessary casting

## QA-50 Always update comments in code if it's already the deadline

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L14

```solidity
/// @notice NOTE: The `getZkSyncMeta` that is used to obtain this struct will experience a breaking change in 2024.
struct ZkSyncMeta {
    uint32 pubdataPublished;
    uint32 heapSize;
    uint32 auxHeapSize;
    uint8 shardId;
    uint8 callerShardId;
    uint8 codeShardId;
}
```

The attached snippets suggests that there would be a breaking change to the struct in 2024, but we are in 2024 and the comment needs to updated to either another year or atleast a more specific time even if not months, could be anything like "Q3/Q4 2024"

### Impact

Confused code, appplications really hoping to build around this wouldn't know if to go on with their development/deployment since they don't know if the breaking change is going to affect their to be deployed logic, and also don't have a definitive on when this breaking change would occur.

### Recommended Mitigation Steps

Consider having a more specific time in regards to when the breaking change would occur

## QA-51 Fix documentation in regards to timing requirements so code doesn't deviate from docs

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/SystemContext.sol#L428-L434

```solidity
    function _ensureBatchConsistentWithL2Block(uint128 _newTimestamp) internal view {
        uint128 currentBlockTimestamp = currentL2BlockInfo.timestamp;
        require(
            _newTimestamp > currentBlockTimestamp,
            "The timestamp of the batch must be greater than the timestamp of the previous block"
        );
    }
```

Now look at this section of the docs https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/docs/Smart%20contract%20Section/Batches%20%26%20L2%20blocks%20on%20zkSync.md#timing-invariants

We can see that it's been wrongly stated that `For each L2 block its timestamp should be ≥ timestamp of the batch it belongs to` case is with the code implementation we can see that the check is instead strictly greater than.

### Impact

Bad code structure, making it harder to understand implementation.

### Recommended Mitigation Steps

Fix the docs, change https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/docs/Smart%20contract%20Section/Batches%20%26%20L2%20blocks%20on%20zkSync.md#timing-invariants to `For each L2 block its timestamp should be **>** timestamp of the batch it belongs to`

## QA-52 Airdrops are automatically lost for the L1ERC20Bridge

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

Contract is obviously a bridge that allows for the depositing of ERC20 tokens to hyperchains, this means that the contract at some point would hold a lot of tokens and could be eligible for some airdrops, since its most likely going to be based on the snapshot of the token balance, now clearly this contract does not entail any sweeping functions and as such all airdrops sent to this contract are effectively stuck

### Impact

Leak of value since there are no methods to get hold of the airdrops

### Recommended Mitigation Steps

Introduce a sweeper functionality for these cases.

## QA-53 `TransactionHelper::isEthToken()` is not used anywhere, so it should be removed

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L89-L97

```solidity

    function isEthToken(uint256 _addr) internal pure returns (bool) {
        return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;
    }

```

This function is used to know whether the `address` passed is th `Ether` address, and also returns true if the address passed is `0x0` (for conveniency) as stated [here](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L92), issue with this is tht using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+isEthToken&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+isEthToken&type=code) we can see that this function is not used anywhere.

### Impact

Remove redundant code as they most of the time hint flawed implementation

### Recommended Mitigation Steps

Remove the `isEthToken()` function since it's not being used anywhere

## QA-54 The` storedBatchHash()` fails to distinguish between reverted and unreverted batches

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L121-L125

```solidity
    /// @inheritdoc IGetters
    function storedBatchHash(uint256 _batchNumber) external view returns (bytes32) {
        return s.storedBatchHashes[_batchNumber];
    }

```

Now consider this previously confirmed issue: https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+is%3Aopen+Inaccurate+Batch+Stored+Hash+Retrieval+in+Getters+Contract

Case with the function's implementation is that, it returns zero for uncommitted batch numbers, but it lacks the capability to distinguish between a reverted and an unreverted batch. For example, if batch number 500 has been reverted, and a user queries storedBatchHash(500), it returns a non-zero value, which may create the impression that the batch is unreverted. However, it should ideally return zero in such scenarios.

Now evidently this is from a past report, but whereas protocol pronounced "acknowledged" findings to be OOS, this was `confirmed` and as such must have forgotten to be fixed.

### Impact

Users would be misled on the status for batches in zkSync

### Recommended Mitigation Steps

As previously recommended, revise the function as the below:

```solidity
function storedBatchHash(uint256 _batchNumber) external view returns (bytes32) {
        if(_batchNumber > s.totalBatchesCommitted){
            return bytes32(0);
        }
        return s.storedBatchHashes[_batchNumber];
    }
```

## QA-55 Users would assume proof verification is performed twice in `proveBatches()` due to a wrongly commenting out the `else` keyword and lack of documentation

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L386-L440

```solidity
    function _proveBatches(
        StoredBatchInfo calldata _prevBatch,
        StoredBatchInfo[] calldata _committedBatches,
        ProofInput calldata _proof
    ) internal {
//ommited for brevity
//@audit

        if (_proof.serializedProof.length > 0) {
            _verifyProof(proofPublicInput, _proof);
        }
        // #else
        _verifyProof(proofPublicInput, _proof);
        // #endif

        emit BlocksVerification(s.totalBatchesVerified, currentTotalBatchesVerified);
        s.totalBatchesVerified = currentTotalBatchesVerified;
    }

```

Thhis function eventually gets called when proving the batches, now as tagged by "@audit", evidently, if the proof is not empty, it gets verified, due to the `if` block.

Where as one might look at this and assume there to be a logical error, as naturally if we are having an `if/else` conditional arrangement, then the else block should entain a different execution, but here that's not the case cause the preprocessor is going to remove one of the ` _verifyProof(proofPublicInput, _proof);`

### Impact

Bad code structure, unclear documentation

### Recommended Mitigation Steps

Correctly apply the documentations attached to this

## QA-56 Wrong error message in `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L41

```solidity
    function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
        uint256 previousProtocolVersion = s.protocolVersion;
        require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than the current one"
        );
        require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );

        // If the previous upgrade had an L2 system upgrade transaction, we require that it is finalized.
        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
        require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );

        s.protocolVersion = _newProtocolVersion;
        emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
    }
```

This function is used to change the protocol version, only case atttached here is the fact that if `_newProtocolVersion >= previousProtocolVersion,` does not hold true, the execution errors out with "New protocol version is not greater than the current one" instead of "New protocol version is **not greater than or equal to** the current one".

### Impact

Inaccurate error messages, code confusion

### Recommended Mitigation Steps

Apply these changes to https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L20-L41

```diff
    function _setNewProtocolVersion(uint256 _newProtocolVersion) internal override {
        uint256 previousProtocolVersion = s.protocolVersion;
        require(
            // Genesis Upgrade difference: Note this is the only thing change > to >=
            _newProtocolVersion >= previousProtocolVersion,
            "New protocol version is not greater than or equal to the current one"
        );
        require(
            _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
            "Too big protocol version difference"
        );

        // If the previous upgrade had an L2 system upgrade transaction, we require that it is finalized.
        require(s.l2SystemContractsUpgradeTxHash == bytes32(0), "Previous upgrade has not been finalized");
        require(
            s.l2SystemContractsUpgradeBatchNumber == 0,
            "The batch number of the previous upgrade has not been cleaned"
        );

        s.protocolVersion = _newProtocolVersion;
        emit NewProtocolVersion(previousProtocolVersion, _newProtocolVersion);
    }
```


