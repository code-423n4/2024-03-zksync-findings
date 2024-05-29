---
sponsor: "zkSync"
slug: "2024-03-zksync"
date: "2024-05-29"
title: "zkSync Era"
findings: "https://github.com/code-423n4/2024-03-zksync-findings/issues"
contest: 347
---

# Overview

## About C4

Code4rena (C4) is an open organization consisting of security researchers, auditors, developers, and individuals with domain expertise in smart contracts.

A C4 audit is an event in which community participants, referred to as Wardens, review, audit, or analyze smart contract logic in exchange for a bounty provided by sponsoring projects.

During the audit outlined in this document, C4 conducted an analysis of the zkSync Era smart contract system written in Solidity. The audit took place between March 7—March 28 2024.

## Wardens

26 Wardens contributed reports to zkSync Era:

  1. [bin2chen](https://code4rena.com/@bin2chen)
  2. [oakcobalt](https://code4rena.com/@oakcobalt)
  3. [rvierdiiev](https://code4rena.com/@rvierdiiev)
  4. [Bauchibred](https://code4rena.com/@Bauchibred)
  5. [lsaudit](https://code4rena.com/@lsaudit)
  6. [hihen](https://code4rena.com/@hihen)
  7. [0x11singh99](https://code4rena.com/@0x11singh99)
  8. [ChaseTheLight](https://code4rena.com/@ChaseTheLight)
  9. [Dup1337](https://code4rena.com/@Dup1337) ([sorrynotsorry](https://code4rena.com/@sorrynotsorry) and [deliriusz](https://code4rena.com/@deliriusz))
  10. [slvDev](https://code4rena.com/@slvDev)
  11. [Pechenite](https://code4rena.com/@Pechenite) ([Bozho](https://code4rena.com/@Bozho) and [radev\_sw](https://code4rena.com/@radev_sw))
  12. [DadeKuma](https://code4rena.com/@DadeKuma)
  13. [oualidpro](https://code4rena.com/@oualidpro)
  14. [Sathish9098](https://code4rena.com/@Sathish9098)
  15. [erebus](https://code4rena.com/@erebus)
  16. [XDZIBECX](https://code4rena.com/@XDZIBECX)
  17. [yashar](https://code4rena.com/@yashar)
  18. [forgebyola](https://code4rena.com/@forgebyola)
  19. [Topmark](https://code4rena.com/@Topmark)
  20. [bctester](https://code4rena.com/@bctester)
  21. [zhanmingjing](https://code4rena.com/@zhanmingjing)
  22. [rjs](https://code4rena.com/@rjs)
  23. [aua\_oo7](https://code4rena.com/@aua_oo7)
  24. [K42](https://code4rena.com/@K42)

This audit was judged by [0xsomeone](https://code4rena.com/@0xsomeone).

Final report assembled by [liveactionllama](https://twitter.com/liveactionllama) and DecentralDisco.

# Summary

The C4 analysis yielded an aggregated total of 5 unique vulnerabilities. Of these vulnerabilities, 1 received a risk rating in the category of HIGH severity and 4 received a risk rating in the category of MEDIUM severity.

Additionally, C4 analysis included 7 reports detailing issues with a risk rating of LOW severity or non-critical. There were also 12 reports recommending gas optimizations.

All of the issues presented here are linked back to their original finding.

# Scope

The code under review can be found within the [C4 zkSync Era repository](https://github.com/code-423n4/2024-03-zksync), and is composed of 115 smart contracts written in the Solidity programming language and includes 10,785 lines of Solidity code.

# Severity Criteria

C4 assesses the severity of disclosed vulnerabilities based on three primary risk categories: high, medium, and low/non-critical.

High-level considerations for vulnerabilities span the following key areas when conducting assessments:

- Malicious Input Handling
- Escalation of privileges
- Arithmetic
- Gas use

For more information regarding the severity criteria referenced throughout the submission review process, please refer to the documentation provided on [the C4 website](https://code4rena.com), specifically our section on [Severity Categorization](https://docs.code4rena.com/awarding/judging-criteria/severity-categorization).

# High Risk Findings (1)
## [[H-01] `paymaster` will refund `spentOnPubdata` to user](https://github.com/code-423n4/2024-03-zksync-findings/issues/78)
*Submitted by [bin2chen](https://github.com/code-423n4/2024-03-zksync-findings/issues/78)*

A very important modification of this update is that the GAS spent by `pubdata` is collected at the final step of the transaction.

But if there is a `paymaster`, when executing `paymaster.postTransaction(_maxRefundedGas)`,
`_maxRefundedGas` does not subtract the `spentOnPubdata`.

`bootloader.yul` the code is as follow：

<details>

```yul
            function refundCurrentL2Transaction(
                txDataOffset,
                transactionIndex,
                success, 
                gasLeft,
                gasPrice,
                reservedGas,
                basePubdataSpent,
                gasPerPubdata
            ) -> finalRefund {
                setTxOrigin(BOOTLOADER_FORMAL_ADDR())

                finalRefund := 0

                let innerTxDataOffset := add(txDataOffset, 32)

                let paymaster := getPaymaster(innerTxDataOffset)
                let refundRecipient := 0
                switch paymaster
                case 0 {
                    // No paymaster means that the sender should receive the refund
                    refundRecipient := getFrom(innerTxDataOffset)
                }
                default {
                    refundRecipient := paymaster
                    
                    if gt(gasLeft, 0) {
                        checkEnoughGas(gasLeft)
                        let nearCallAbi := getNearCallABI(gasLeft)
                        let gasBeforePostOp := gas()
                        pop(ZKSYNC_NEAR_CALL_callPostOp(
                            // Maximum number of gas that the postOp could spend
                            nearCallAbi,
                            paymaster,
                            txDataOffset,
                            success,
                            // Since the paymaster will be refunded with reservedGas,
                            // it should know about it
@>                          safeAdd(gasLeft, reservedGas, "jkl"),
                            basePubdataSpent,
                            reservedGas,
                            gasPerPubdata
                        ))
                        let gasSpentByPostOp := sub(gasBeforePostOp, gas())

                        gasLeft := saturatingSub(gasLeft, gasSpentByPostOp)
                    } 
                }

                // It was expected that before this point various `isNotEnoughGasForPubdata` methods would ensure that the user 
                // has enough funds for pubdata. Now, we just subtract the leftovers from the user.
@>              let spentOnPubdata := getErgsSpentForPubdata(
                    basePubdataSpent,
                    gasPerPubdata
                )

                let totalRefund := saturatingSub(add(reservedGas, gasLeft), spentOnPubdata)

                askOperatorForRefund(
                    totalRefund,
                    spentOnPubdata,
                    gasPerPubdata
                )

                let operatorProvidedRefund := getOperatorRefundForTx(transactionIndex)

                // If the operator provides the value that is lower than the one suggested for 
                // the bootloader, we will use the one calculated by the bootloader.
                let refundInGas := max(operatorProvidedRefund, totalRefund)

                // The operator cannot refund more than the gasLimit for the transaction
                if gt(refundInGas, getGasLimit(innerTxDataOffset)) {
                    assertionError("refundInGas > gasLimit")
                }

                if iszero(validateUint32(refundInGas)) {
                    assertionError("refundInGas is not uint32")
                }

                let ethToRefund := safeMul(
                    refundInGas, 
                    gasPrice, 
                    "fdf"
                ) 

                directETHTransfer(ethToRefund, refundRecipient)

                finalRefund := refundInGas
            }
```

</details>

`paymaster's` `_maxRefundedGas = gasLeft + reservedGas`, without subtracting `spentOnPubdata`.

This way `_maxRefundedGas` will be much larger than the correct value.

`paymaster` will refund the used `spentOnPubdata` to the user.

### Impact

`paymaster` will refund the `spentOnPubdata` already used by the user.

### Recommended Mitigation

<details>

```diff
            function refundCurrentL2Transaction(
                txDataOffset,
                transactionIndex,
                success, 
                gasLeft,
                gasPrice,
                reservedGas,
                basePubdataSpent,
                gasPerPubdata
            ) -> finalRefund {
                setTxOrigin(BOOTLOADER_FORMAL_ADDR())

                finalRefund := 0

                let innerTxDataOffset := add(txDataOffset, 32)

                let paymaster := getPaymaster(innerTxDataOffset)
                let refundRecipient := 0
                switch paymaster
                case 0 {
                    // No paymaster means that the sender should receive the refund
                    refundRecipient := getFrom(innerTxDataOffset)
                }
                default {
                    refundRecipient := paymaster
+                   let expectSpentOnPubdata := getErgsSpentForPubdata(
+                        basePubdataSpent,
+                        gasPerPubdata
+                    )                    
                    if gt(gasLeft, 0) {
                        checkEnoughGas(gasLeft)
                        let nearCallAbi := getNearCallABI(gasLeft)
                        let gasBeforePostOp := gas()
                        pop(ZKSYNC_NEAR_CALL_callPostOp(
                            // Maximum number of gas that the postOp could spend
                            nearCallAbi,
                            paymaster,
                            txDataOffset,
                            success,
                            // Since the paymaster will be refunded with reservedGas,
                            // it should know about it
-                           safeAdd(gasLeft, reservedGas, "jkl"),
+                           saturatingSub(add(reservedGas, gasLeft), expectSpentOnPubdata),
                            basePubdataSpent,
                            reservedGas,
                            gasPerPubdata
                        ))
                        let gasSpentByPostOp := sub(gasBeforePostOp, gas())

                        gasLeft := saturatingSub(gasLeft, gasSpentByPostOp)
                    } 
                }

                // It was expected that before this point various `isNotEnoughGasForPubdata` methods would ensure that the user 
                // has enough funds for pubdata. Now, we just subtract the leftovers from the user.
                let spentOnPubdata := getErgsSpentForPubdata(
                    basePubdataSpent,
                    gasPerPubdata
                )

                let totalRefund := saturatingSub(add(reservedGas, gasLeft), spentOnPubdata)

                askOperatorForRefund(
                    totalRefund,
                    spentOnPubdata,
                    gasPerPubdata
                )

                let operatorProvidedRefund := getOperatorRefundForTx(transactionIndex)

                // If the operator provides the value that is lower than the one suggested for 
                // the bootloader, we will use the one calculated by the bootloader.
                let refundInGas := max(operatorProvidedRefund, totalRefund)

                // The operator cannot refund more than the gasLimit for the transaction
                if gt(refundInGas, getGasLimit(innerTxDataOffset)) {
                    assertionError("refundInGas > gasLimit")
                }

                if iszero(validateUint32(refundInGas)) {
                    assertionError("refundInGas is not uint32")
                }

                let ethToRefund := safeMul(
                    refundInGas, 
                    gasPrice, 
                    "fdf"
                ) 

                directETHTransfer(ethToRefund, refundRecipient)

                finalRefund := refundInGas
            }
```

</details>

### Assessed type

Context

**[saxenism (zkSync) confirmed, but disagreed with severity and commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/78#issuecomment-2036982976):**
 > We confirm the finding. It is good.
> 
> We however believe that this is a medium severity issue since this is a rarely used functionality.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/78#issuecomment-2082867166):**
 > The Warden has identified a discrepancy in the way paymaster refunds are processed for L2 transactions, resulting in an over-compensation that overlaps with the gas spent on public data.
> 
> The exhibit is correct, and I am not in complete agreement with the Sponsor's assessment in relation to the submission's severity. The referenced code will trigger if a paymaster has been defined, and I do not believe there is any constraint that permits a malicious user from **always triggering the surplus refund** and thus **from slowly siphoning funds in the form of gas from the system**.
> 
> As the flaw **is always present** and its impact **is properly considered medium**, I consider the combination of those two factors to merit a **high severity rating**.



***

 
# Medium Risk Findings (4)
## [[M-01] Freezed Chain will never be unfreeze since `StateTransitionManager::unfreezeChain` is calling `freezeDiamond` instead of `unfreezeDiamond`](https://github.com/code-423n4/2024-03-zksync-findings/issues/97)
*Submitted by [0x11singh99](https://github.com/code-423n4/2024-03-zksync-findings/issues/97), also found by [oakcobalt](https://github.com/code-423n4/2024-03-zksync-findings/issues/136), [Bauchibred](https://github.com/code-423n4/2024-03-zksync-findings/issues/135), [erebus](https://github.com/code-423n4/2024-03-zksync-findings/issues/104), [XDZIBECX](https://github.com/code-423n4/2024-03-zksync-findings/issues/96), [Dup1337](https://github.com/code-423n4/2024-03-zksync-findings/issues/93), [yashar](https://github.com/code-423n4/2024-03-zksync-findings/issues/89), [bin2chen](https://github.com/code-423n4/2024-03-zksync-findings/issues/76), [forgebyola](https://github.com/code-423n4/2024-03-zksync-findings/issues/56), [Topmark](https://github.com/code-423n4/2024-03-zksync-findings/issues/20), [rvierdiiev](https://github.com/code-423n4/2024-03-zksync-findings/issues/48), [bctester](https://github.com/code-423n4/2024-03-zksync-findings/issues/24), and [zhanmingjing](https://github.com/code-423n4/2024-03-zksync-findings/issues/7)*

`StateTransitionManager::unfreezeChain` function is meant for unfreeze the freezed chain of passed `_chainId` param. While `freezeChain` function is meant for freeze the chain according to passed \_chainId. But `freezeChain` and `unfreezeChain` both functions are calling same function `freezeDiamond` by same line `IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond()` by mistake. So both these function will only freeze the chain.

Also there is no other function inside `StateTransitionManager.sol` contract which is calling `unfreezeDiamond`. `unfreezeDiamond` is function defined in `Admin.sol` where the call is going since `IZkSyncStateTransition` also inherits IAdmin which have freezeDiamond and unfreezeDiamond both functions. But `unfreezeDiamond` is not called from `unfreezeChain` function. So freezed chain will never be unfreeze.

`unfreezeChain` also have wrong comment instead of writing unfreezes it writes freezes.
It seems like dev just copy pasted without doing required changes.

### Vulnerable Code

[code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L165-L167](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L165C4-L167C6)

```solidity

159:    /// @dev freezes the specified chain
160:    function freezeChain(uint256 _chainId) external onlyOwner {
161:        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
     }

164:    /// @dev freezes the specified chain
165:    function unfreezeChain(uint256 _chainId) external onlyOwner {
166:        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();//@audit `freezeDiamond` called instead of `unfreezeDiamond`

    }

```

(<https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L15>)

[IZkSyncStateTransition is inheriting IAdmin](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IZkSyncStateTransition.sol#L15) and by IZkSyncStateTransition wrapping instance is prepared to call freezeDiamond.

```solidity
15: interface IZkSyncStateTransition is IAdmin, IExecutor, IGetters, IMailbox {
```

[IAdmin interfaces have both functions](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IAdmin.sol#L52C5-L58C41)

```solidity
13:  interface IAdmin is IZkSyncStateTransitionBase {

    ....

52:  /// @notice Instantly pause the functionality of all freezable facets & their selectors
     /// @dev Only the governance mechanism may freeze Diamond Proxy
54:    function freezeDiamond() external;

     /// @notice Unpause the functionality of all freezable facets & their selectors
     /// @dev Both the admin and the STM can unfreeze Diamond Proxy
58:    function unfreezeDiamond() external;

```

It shows that by mistake unfreezeChain is calling freezeDiamond instaed of unfreezeDiamond which should be used to unfreeze the chain.

### Impact

Freezed chain will never be unfreeze.
Since `freezeChain` and `unfreezeChain` both functions are calling same function `freezeDiamond` which is used to freeze the chain. And `unfreezeDiamond` no where called which should is made for unfreeze the freezed chain.

### Recommended Mitigation

In `StateTransitionManager::unfreezeChain` function call `unfreezeDiamond` instead of `freezeDiamond` on `IZkSyncStateTransition(stateTransition[_chainId])` instance.

```diff
File:  code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol
- 164:    /// @dev freezes the specified chain
+ 164:    /// @dev unfreezes the specified chain
165:    function unfreezeChain(uint256 _chainId) external onlyOwner {
- 166:        IZkSyncStateTransition(stateTransition[_chainId]).freezeDiamond();
+ 166:        IZkSyncStateTransition(stateTransition[_chainId]).unfreezeDiamond();
          }
```

**[0xsomeone (judge) increased severity to High](https://github.com/code-423n4/2024-03-zksync-findings/issues/97#issuecomment-2032589179)**

**[saxenism (zkSync) confirmed, but disagreed with severity and commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/97#issuecomment-2036801296):**
 > This is a good finding, but we consider this a `medium` severity issue because in the current codebase `admin` could also unfreeze (so no permanent freeze & so not high), but in the future we might wanna change this mechanism.

**[0xsomeone (judge) decreased severity to Medium and commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/97#issuecomment-2082815615):**
 > The submission and its relevant duplicates have identified a mistype in the codebase that causes certain functionality that is expected to be accessible to behave oppositely.
> 
> The exhibit represents an actual error in the code resulting in functionality missing, however, the functionality does contain an alternative access path per the Sponsor's statement and as such I consider this exhibit to be of medium risk.



***

## [[M-02] L2SharedBridge l1LegacyBridge is not set](https://github.com/code-423n4/2024-03-zksync-findings/issues/77)
*Submitted by [bin2chen](https://github.com/code-423n4/2024-03-zksync-findings/issues/77), also found by [rvierdiiev](https://github.com/code-423n4/2024-03-zksync-findings/issues/50)*

The migration steps for `L1ERC20Bridge/L2ERC20Bridge` are as follows:

<br><https://github.com/code-423n4/2024-03-zksync/blob/main/docs/Protocol%20Section/Migration%20process.md>

> II. Upgrade L1ERC20Bridge contract
>
> 1.  Upgrade L2 bridge
>
> The new L2ERC20Bridge will upgraded to become the L2SharedBridge, and it will be backwards compatible with all messages from the old L1ERC20Bridge, so we upgrade that first as L1->L2 messages are much faster, and in the meantime we can upgrade the L1ERC20Bridge. The new L2SharedBridge can receive deposits from both the old L1ERC20Bridge and the new L1SharedBridge.
>
> 2.  Upgrade L1ERC20Bridge
>
> We upgrade the L1ERC20Bridge, and move all ERC20 tokens to the L1SharedBridge.

Since `L2ERC20Bridge` will be updated first, and then `L1ERC20Bridge` will be updated, `L2SharedBridge` needs to be compatible with the old `L1ERC20Bridge` before `L1ERC20Bridge` is updated.

So in `L2SharedBridge.initialize()` we need to set `l1LegacyBridge = L1ERC20Bridge` and `finalizeDeposit()` to allow `l1LegacyBridge` to execute.

But the current implementation doesn't set `l1LegacyBridge`, it's always `address(0)`.

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
@>          // Missing set l1LegecyBridge？
            // l2StandardToken and l2TokenBeacon are already deployed on ERA, and stored in the proxy
        }
    }
```

The above method just checks `_l1LegecyBridge ! = address(0)`, and does not assign a value, `l1LegacyBridge` is always `adddress(0)`.

This way any messages sent by the user before update `L1ERC20Bridge` will fail because `finalizeDeposit()` will not pass the validation

### Impact

Until `L1ERC20Bridge` is updated, messages sent by the user will fail.

### Recommended Mitigation

```diff
    function initialize(
        address _l1Bridge,
        address _l1LegecyBridge,
        bytes32 _l2TokenProxyBytecodeHash,
        address _aliasedOwner
    ) external reinitializer(2) {
...
        if (block.chainid != ERA_CHAIN_ID) {
            address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
            l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
            l2TokenBeacon.transferOwnership(_aliasedOwner);
        } else {
            require(_l1LegecyBridge != address(0), "bf2");
+           l1LegacyBridge = _l1LegecyBridge
            // l2StandardToken and l2TokenBeacon are already deployed on ERA, and stored in the proxy
        }
    }
```

### Assessed type

Context

**[saxenism (zkSync) confirmed and commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/77#issuecomment-2036960006):**
 > We confirm this finding. Thank you :)
> 
> Just adding a little more context here:
> 
> The deposits will fail but user can call claimFailedDeposit to get funds back.
> We have failed to assign the l1LegacyBridge, but that does not pose a security risk since the l1Bridge should work as expected and therefore, the finalizeDeposit function still has a way to work. However, yes, this is an issue because this breaks our intended behaviour.

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/77#issuecomment-2082831324):**
 > The Warden has demonstrated how a missing assignment will result in legacy transactions failing to finalize. The impact is constrained to legacy transactions, and as it is possible for users to recover their failed deposits the impact is impermanent resulting in a severity of medium being appropriate.

***

## [[M-03] State transition manager is unable to force upgrade a deployed ST, which invalidates the designed safeguard for 'urgent high risk situation'](https://github.com/code-423n4/2024-03-zksync-findings/issues/53)
*Submitted by [oakcobalt](https://github.com/code-423n4/2024-03-zksync-findings/issues/53)*

### Impact

State transition manager (STM) will be unable to force upgrade a deployed ST against intended design for 'urgent high risk situation'.

This invalidates the designed safeguard mechanism of an STM force upgrade and ST.

### Proof of Concept

According to [doc](https://github.com/code-423n4/2024-03-zksync/blob/main/docs/Smart%20contract%20Section/L1%20ecosystem%20contracts.md#configurability-in-the-first-release), `in case of urgent high risk situation, STM might force upgrade the contract`(ST).

However, the above safeguard of force upgrading ST is not possible due to StateTransitionManger.sol's incomplete implementation.

(1) A deployed chain(ST) can choose to perform a mandatory upgrade at its own convenience. It's also possible for an ST to postpone an upgrade set by the state transition manager. An ST will perform an upgrade through `upgradeChainFromVersion()` on the Admin facet.

```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
    function upgradeChainFromVersion(
        uint256 _oldProtocolVersion,
        Diamond.DiamondCutData calldata _diamondCut
|>    ) external onlyAdminOrStateTransitionManager {
...
```

(<https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L103>)
Note that although `upgradeChainFromVersion()` is access-controlled by both chain admin and StateTransitionManager contract. StateTransitionManager will not be able to call it, because no methods or flows on StateTransitionManger.sol will invoke the call.

(2) Another method on Admin facet for upgrade is `executeUpgrade()` which is access-controlled by only StateTransitionManager contract. However, `executeUpgrade()` can only be invoked inside `_setChainIdUpgrade()`. And `_setChainIdUpgrade()` can only be invoked inside `createNewChain()`. This means, after a chain(ST)'s genesis, `executeUpgrade()` cannot be invoked by stateTransitionManger again to perform further upgrades.

```solidity
//code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol
    function executeUpgrade(
        Diamond.DiamondCutData calldata _diamondCut
|>    ) external onlyStateTransitionManager {
        Diamond.diamondCut(_diamondCut);
        emit ExecuteUpgrade(_diamondCut);
    }
```

(<https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L123>)

```solidity
    function _setChainIdUpgrade(
        uint256 _chainId,
        address _chainContract
    ) internal {
...
          //@audit executeUpgrade of an ST will only be called once at chain deployment, because _setChainIdUpgrade() is only invoked when creating a new chain.
|>        IAdmin(_chainContract).executeUpgrade(cutData);
...
```

(<https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L226>)

As a result of (1)&(2), StateChainManager cannot force upgrade an ST `in case of urgent high risk situation`. This invalidates the safeguard of force upgrade as stated by doc.

### Recommended Mitigation Steps

In StateTransitionManager.sol, add a method that can call `executeUpgrade()` or `upgradeChainFromVersion()` on a local chain.

**[saxenism (zkSync) confirmed and commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/53#issuecomment-2036919937):**
 > Agree with the finding. Thank you :)

**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/53#issuecomment-2082860557):**
 > The Warden has demonstrated how, in an urgent high-risk situation, a forced upgrade cannot be performed in contradiction with the project's documentation.
> 
> Based on the fact that the vulnerability is correct and would surface in a low-likelihood scenario, a medium-risk assessment is appropriate.
***

## [[M-04] User might be able to double withdraw during migration](https://github.com/code-423n4/2024-03-zksync-findings/issues/34)
*Submitted by [oakcobalt](https://github.com/code-423n4/2024-03-zksync-findings/issues/34)*

### Impact

A user might be able to double withdraw during migration in some edge conditions: (1) if their withdrawal tx is included in a batch number the same or after `eraFirstPostUpgradeBatch`; (2)And if the user `finalizeWithdrawal` on the old L1ERC20Bridge.sol before L1ERC20Bridge.sol is upgraded.

### Proof of Concept

The current migration process takes place in [steps](https://github.com/code-423n4/2024-03-zksync/blob/main/docs/Protocol%20Section/Migration%20process.md), which might allow edge conditions to occur. StepA: deploy new contracts(including L1SharedBridge); StepB:Era upgrade and L2 system contracts upgrade(at this point old L1ERC20Bridge still works); StepC: Upgrade L2 bridge and L1ERC20Brdige.sol. Then migrate funds to the new L1sharedBridge.

Since L1ERC20Bridge.sol is upgraded at the end. An edge condition can occur between StepA and StepB, where a user can still withdraw ERC20 tokens on the old L1ERC20Brdige.sol.

Scenario: If a user `finalizeWithdrawal` ERC20 tokens on the old L1ERC20Bridge.sol first, they can withdraw again on L1SharedBridge.sol as long as the `_l2batchNumber` of the withdraw tx equals or is greater than `eraFirstPostUpgradeBatch`. In other words, `_isEraLegacyWithdrawal` check can be invalidated.

1.  stepA: L1SharedBridge.sol will be deployed and initialized with a pre-determined value `eraFirstPostUpgradeBatch`;
2.  UserA can initiate an ERC20 withdrawal tx on L2 bridge(currently old version);
3.  stepB: Era upgrade is performed. UserA's withdrawal tx is included in the same `eraFirstPostUpgradeBatch` number;
4.  UserA `finializeWithdrawal` on the old L1ERC20Brdige.sol.UserA should receive funds because funds haven't been migrated yet;
5.  stepC: new L1ERC20Bridge.sol is upgraded and funds(ERC20) are migrated to L1SharedBridge.sol;
6.  UserA `finializeWithdrawal` on L1SharedBridge.sol. This time, `_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)` check will be bypassed,because user's `_l2BatchNumber` == `eraFirstPostUpgradeBatch`; UserA can receive the withdrawal funds a second time;

```solidity
//code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
    function finalizeWithdrawal(
        uint256 _chainId,
        uint256 _l2BatchNumber,
        uint256 _l2MessageIndex,
        uint16 _l2TxNumberInBatch,
        bytes calldata _message,
        bytes32[] calldata _merkleProof
    ) external override {
       //@audit-info when _l2BatchNumber>= eraFirstPostUpgradeBatch, `_isEraLegacyWithdrawal()` return false, checking on withdrawal status on legacyERC20bridge will be bypassed.
|>     if (_isEraLegacyWithdrawal(_chainId, _l2BatchNumber)) {
            require(
                !legacyBridge.isWithdrawalFinalized(
                    _l2BatchNumber,
                    _l2MessageIndex
                ),
                "ShB: legacy withdrawal"
            );
        }
        _finalizeWithdrawal(
            _chainId,
            _l2BatchNumber,
            _l2MessageIndex,
            _l2TxNumberInBatch,
            _message,
            _merkleProof
        );
}
```

(<https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L421-L427>)

```solidity
//code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol
    function _isEraLegacyWithdrawal(
        uint256 _chainId,
        uint256 _l2BatchNumber
    ) internal view returns (bool) {
        return
            (_chainId == ERA_CHAIN_ID) &&
|>          (_l2BatchNumber < eraFirstPostUpgradeBatch); //@audit-info note:when _l2BatchNumber>= eraFirstPostUpgradeBatch, `_isEraLegacyWithdrawal()` return false.
    }
```

(<https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L375>)

As seen, checking on legacyERC20bridge withdrawal status will only be performed when `_isEraLegacyWithdrawal` returns true. But due to `_l2BatchNumber` of a withdrawal tx during the upgrade can equal or be greater than a predefined `eraFirstPostUpgradeBatch`. `_isEraLegacyWithdrawal` check can be based on false assumptions on `_l2BatchNumber` and `eraFirstPostUpgradeBatch`, allowing double withdrawal on edge cases.

### Recommended Mitigation Steps

Consider adding a grace period during and following an upgrade, during which time legacyWithdrawal status will always be checked.

**[razzorsec (zkSync) confirmed, but disagreed with severity and commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/34#issuecomment-2064245734):**
 > Realistically invalid, since we will not finalize the upgrade batch. But an interesting thing to remember, so we would consider this as Low, as it is mostly about managing the server.


**[0xsomeone (judge) commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/34#issuecomment-2082849066):**
 > The Warden specifies that under certain circumstances, it is possible to perform a duplicate withdrawal when the system is in the midst of an upgrade.
> 
> The Sponsor specifies that this issue is realistically invalid, however, the Sponsor's statement relies on being aware of the flaw and acting actively against it (i.e. not finalizing the upgrade batch) which I do not consider adequate justification to lower the severity of this exhibit.
> 
> I believe a medium-risk grade is appropriate based on the fact that it illustrates a code flaw that will arise under operations permitted by the smart contracts which we cannot presume the Sponsor was aware of.

***

# Low Risk and Non-Critical Issues

For this audit, 7 reports were submitted by wardens detailing low risk and non-critical issues. The [report highlighted below](https://github.com/code-423n4/2024-03-zksync-findings/issues/122) by **Bauchibred** received the top score from the judge.

*The following wardens also submitted reports: [lsaudit](https://github.com/code-423n4/2024-03-zksync-findings/issues/65), [hihen](https://github.com/code-423n4/2024-03-zksync-findings/issues/33), [0x11singh99](https://github.com/code-423n4/2024-03-zksync-findings/issues/109), [Dup1337](https://github.com/code-423n4/2024-03-zksync-findings/issues/90), [ChaseTheLight](https://github.com/code-423n4/2024-03-zksync-findings/issues/73), and [oakcobalt](https://github.com/code-423n4/2024-03-zksync-findings/issues/60).*

**Note from the warden:**

While we've tried our best to maintain readability for brevity and focus, we have selectively truncated the code snippets to spotlight relevant sections. Certain excerpts may be abbreviated, and some references are provided via search commands due to the extensive nature of the project and time constraints

Also, it's important to mention that a previous audit conducted [a few months back by Code4rena](https://github.com/code-423n4/2023-10-zksync) on an [older commit](https://github.com/code-423n4/2024-03-zksync/compare/2023-10-zksync...main) of the contracts in scope, this audit had a bot race and as such yielded a [bot report](https://raw.githubusercontent.com/code-423n4/2023-10-zksync/main/bot-report.md) with multiple QA suggestions, the report had over `4000` instances of QA report (both `L's` & `NC's`). Our quick review on some of these findings from the bot, revealed that only few of those suggestions have been acted upon. We recommend that, alongside this report, the team also revisits the [bot report](https://raw.githubusercontent.com/code-423n4/2023-10-zksync/main/bot-report.md) to explore further QA suggestions to improve code structure, this is cause we've deliberately tried our best in not duplicating points from that previous analysis in this report.

## [01] Genesis upgrades, currently do not fully work as intended

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

This function is an overriden one of the inherited `BaseZkSyncUpgrade.upgrade()`, case here is that unlike the inherited version where the bytes data to be returned [has been explicitly mentioned as `txHash`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L67), this function does not explicitly name the variable to be returned, leading to all attempts of calling this function to return `0`.

### Minimalistic POC

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

Passing the value: `0x212226`.

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

**Additional Note**

> Depending on the judge's stance of either looking at this as "breaking core functionality" or "ignorable miss in `code/docs`" determines the final valididty as we assume the former puts this report on the grounds of a `medium`.

## [02] Bootloader wrongly identifies the `RIGHT_PADDED_GET_ACCOUNT_VERSION_SELECTOR` as not attached with the `Contract Deployer` deployment execution

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

This function returns whether the mimicCall should use the `isSystem` flag, note that his flag should only be used for contract deployments and nothing else, now navigating to the bootloaders preprocess script here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/scripts/preprocess-bootloader.ts, we can see that, not all contract deployments selectors would be tagged with the flag, note that this is the intended behaviour since calls to the deployer system contract are the only ones allowed to be system calls.

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

Evidently there are 5 contract deployment functionalities attached with the bootloader's preprocessor, but only 4 of those would be tagged with the `isSystem` flag in the bootloader, since the "extendedAccountVersion" has not been attached.

### Impact

The current implementation of the `bootloader::shouldMsgValueMimicCallBeSystem` would wrongly assume that the contract deployment of the "extendedAccountVersion" is not a system call, i.e [this instance of using the `isSystem` flag in the bootloader](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1972) wrongly assumes that this is not a system call, making the ABI returned by `getFarCallABI()` for low-level innvocations of calls and mimicCalls wrong.

The route for this logic is : `executeL1Tx-> msgValueSimulatorMimicCall -> shouldMsgValueMimicCallBeSystem /mimicCallOnlyResult -> getFarCallABI `

> Submitting this as QA, leaving to the judge to upgrade if they see fit

### Recommended Mitigation Steps

Include the `RIGHT_PADDED_GET_ACCOUNT_VERSION_SELECTOR` in `bootloader::shouldMsgValueMimicCallBeSystem` as an `isSystem` call.

## [03] The new `require(dictionary.length / 8 <= encodedData.length / 2)` check allows malicious operators to always pass in malformed data to the bootloader to ensure that all users gas gets burnt without executing the tx.

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

The `publishCompressedBytecode()` function has been updated, and here is the new implementation https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Compressor.sol#L44-L70, in comparison to the previous implementation, it no longer enforces multiple checks, i.e the `dictionary.length % 8 = 0` and the check where the dictionary's length `< 2** 16` this is done so that protocol can correctly enforce more that the reason why a call to this function fails would be due to gas from the bootloader, but there is a new check that faults this logic , i.e `require(dictionary.length / 8 <= encodedData.length / 2)`, issue with this is that this check does not allow the bootloader to correctly enforce that calls to this functiion would mostly fail due to the gas provided not being enough and might still cause the attempt to forcefully revert https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1740-L1745 i.e an operator passing in a data that does not always fall as "correct" within the checks, for example say the new check of `dictionary.length / 8 <= encodedData.length / 2` is false, would lead to the `sendCompressedBytecode()` in the bootloader near calling and burning all the gas.

### Impact

Having it in mind that the `sendCompressedBytecode()` function is called by the bootloader whenever there is a need for the L2 transaction to use packed bytecode as seen here https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1506 , this then gives the operator the opportunity of burning all of the user's provided gas of any L2 transaction that needs packed/published bytecodes... potentially doing it constantly if the operator is malicious since all they need to do is tamper with the data they pass to the bootloader to ensure the compression always ends up malformed by ignoring the new `dictionary.length/8` check and then all users attempt just burn their gas.

### Recommended Mitigation Steps

Since this enforcement `dictionary.length / 8 <= encodedData.length / 2` still needs to be placed so as not to allow operator pass in an excessive length, then the near calling should be scrapped from the bootloader when an attempt to `sendCompressedBytecode()` is made, i.e if the compression is malformed the attempt should instead revert with reason rather than burning all the gas.

**Additional Notes**

> NB: This wasn't intended to be a QA submission, but these lines exist in the readMe: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/README.md#L31-L34

```markdown
Validator can provide inefficient bytecode compression

In the current implementation, the mechanism for bytecode compression is not strictly unambiguous. That means the validator has the flexibility to choose a less efficient compression for the bytecode to increase the deployment cost for the end user. Besides that, there is another non-fixed [issue](https://github.com/code-423n4/2023-10-zksync-findings/issues/805), that gives a way for the operator to forces the user to pay more for the bytecode compression or even burn all the transaction gas during bytecode compression verification.
```

Now we assume the above snippet makes this issue somewhat subjective as we could argue it makes it stand on the lines of being OOS, If all parties think otherwise then this should be upgraded.

## [04] Users tokens could get lost indefinitely

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

This is a pretty old bug case, where protocols assume that the msg.sender is in control of their addresses or aliased ones on another chain, which led to the famous [20M OP wintermute hack](https://rekt.news/wintermute-rekt/) from 2022, best way imo to fix this would be that while depositing via `deposit(...)` if `_prevMsg.sender` is a contract and no explicit `refundRecipient` is specified, just revert the call.

### Additional Note

- [Article from Rekt](https://rekt.news/wintermute-rekt/) &
- [Code4rena's bug report based on a similar ground](https://github.com/code-423n4/2023-09-maia-findings/issues?q=is%3Aissue+is%3Aopen+if+the+Virtual+Account%27s+owner+is+a+Contract+Account+%28multisig+wallet%29%2C+attackers+can+gain+control+of+the+Virtual+Accounts+by+gaining+control+of+the+same+owner%27s+address+in+a+different+chain)

## [05] Fix typos & documentations _(Multiple instances)_

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

This: " /// @dev transfer tokens from legacy erc20 bridge or mailbox and set chainBalance as part of migration process"

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

## [06] There are currently no assurances that funds specified for operation are rightly matched

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

Potential having excess funds in the Governance.sol, i.e when the msg.value is way greater than the total call.value needed for the transaction, or not enough funds being available for the execution which then leads to eating up funds that have been sent to the contract for different operations

### Recommended Mitigation Steps

Check that msg.value == the total call value needed, if protocol plans on routing the logic via the balance too, then check if the `msg.value + contract's balance of eth` is enough for transaction.

## [07] Protocol is susceptible to synchronizing issues cause reverted system contract upgrade batches must stiill be committed between L1 and L2 upgrades due to wrongly assuming just reverting in the bootloader is enough

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

Now during the current execution, [if for any reason this attempt fails, say the execution runs out of gas, the execution reverts](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/bootloader/bootloader.yul#L1010-L1015), which is a direct fix to the **primary issue** from the previous audits, i.e https://github.com/code-423n4/2023-10-zksync-findings/issues/214#issuecomment-1795027489, but this is not enough fix to ensure that the synchronization is always in play.

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

Bug flow should be seen from the [attached report](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+No+way+of+preventing+the+upgrade+from+happening+even+if+it+has+a+critical+vulnerability+is%3Aclosed), now the protocol's plan to solve this is by overriding `s.l2SystemContractsUpgradeTxHash` in order to cancel the buggy upgrade, but this wouldn't work, cause that upgrade [must be carried out in the next batch](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/docs/Smart%20contract%20Section/Handling%20L1%E2%86%92L2%20ops%20on%20zkSync.md?plain=1#L59-L65), so it gives zero time for protocol to code and then even deploy the new upgrader, now within this time frame, an attacker aware of the bugs in the implementation can exploit the system.

For case [2](https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+if+a+batch+committed+with+system+contract+upgrades+is+reverted+via+revertBatches%28%29+to+prevent+execution+of+that+batch%2C+new+batches+intended+to+be+committed+with+no+system+contract+upgrades+will+be+committed+as+batches+with+system+contract+upgrades.+is%3Aclosed), the core of the issue is the same, i.e it lies in the protocol's failure to delete the transaction hash associated with a system contract upgrade when reverting a batch. This leads to a scenario where subsequent batches, even those not intended to include a system contract upgrade, are processed as if they do, due to the presence of the leftover upgrade transaction hash. This misprocessing causes unintended execution of system contract upgrades or reverts due to mismatched expectations about the batch's content.

Now, the protocol's design allows for the reverting of batches to undo changes not yet executed. However as previously highlighted, it inadequately addresses the cleanup of system contract upgrade markers, specifically the transaction hash (`s.l2SystemContractsUpgradeTxHash`). While it resets the batch number indicating an upgrade (`s.l2SystemContractsUpgradeBatchNumber`), it neglects the corresponding transaction hash. This leads to confusion in the `_commitBatches()` function, take a look at this https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L215-L248

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

Here we see that the new logic for EIP-4844, requires only one batch to be committed at a time due to restriction of blobs per block, but this doesn't solve the root case, cause regardless, `if (systemContractsUpgradeTxHash == bytes32(0) || s.l2SystemContractsUpgradeBatchNumber != 0)` is `false`, which would be the case for our reverted batch, then the execution **always** routes the logic [to commiting with system contract upgrades](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L239-L245).

TLDR: `revert()` will delete upgrade batch number but not the batch tx thus making reverts of batches with system upgrade **non functional** since the system tx hash may still be executed with new batches.

### Impact

Medium _(reason for submitting as QA attached in the  `### Additional Note` section )_, this is cause for the first case, we show how protocol have timelocked themself from being able to to stop the upgrade to a buggy implementation, that might even have critical bug implementations that an attacker could exploit while they code and attempt deploying a non buggy implementation, and for the second case, similar to the first we can see how if for whatever reason `l2SystemContractsUpgradeTxHash` is to be stopped from executing with a batch, it is not possible to do so, [due to `s.l2SystemContractsUpgradeTxHash` not being reverted in `revertBatches()`](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L490-L494)

### Recommended Mitigation Steps

Modify the `revertBatches()` function to ensure comprehensive cleanup after a batch revert. This includes not only resetting the batch number associated with a system contract upgrade but also clearing the related transaction hash (`s.l2SystemContractsUpgradeTxHash`).
While reverting batches both `l2SystemContractsUpgradeBatchNumber` `s.l2SystemContractsUpgradeTxHash` should be provided and deleted.

### Additional Note

> NB: This wasn't intended to be a QA submission, but these lines exist in the readMe:https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/README.md#L35-L38

```markdown
### Acknowledged issues from the previous audits

All unfixed issues from the previous audits are considered out of scope.
- https://era.zksync.io/docs/reference/troubleshooting/audit-bug-bounty.html
```

Now, whereas navigating to the attached link from the `readMe` we can't see the audit where the idea of this bug has been coined attached, we still assume  that it is part of the _previous_ findings, now we just don't know if this was "acknowledged" or "confirmed" since we can see that the [team clearly "confirmed" the bug case](https://github.com/code-423n4/2023-10-zksync-findings/issues/214#issuecomment-1795027489) and applied a fix to it [in this commit](https://github.com/code-423n4/2024-03-zksync/compare/2023-10-zksync...main) provided for this audit, albeit an insufficient one... due to all these we've decided that this issue somewhat subjective and we'd leave it to the judge if they deem it fit to be be upgraded.

## [08] Shadow upgrades would currently have their executional data leaked if they fail

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

Note that these types of upgrades are designed to keep upgrade details confidential until execution. However, if an upgrade attempt fails, the information within the `Operation calldata _operation` parameter, which is bundled with the call specifics via [execute()](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/governance/Governance.sol#L168-L182), becomes public.

### Impact

A failed shadow upgrade unintentionally exposes critical upgrade details to the public, which can include sensitive call data and operational parameters. Malicious actors could exploit this information to discover system vulnerabilities and mount attacks before the deployment of a security patch, note that the current upgrade to the `Governance.sol` even marks these functions (i.e execute() & executeInstant() ) as payable, which suggests that now native token values could be attached to this window.

### Recommended Mitigation Steps

Enforce a protective mechanism that automatically puts the system in a freeze mode upon failure.

## [09] Fix bugs present in the precomcompiles or clearly document the bugs for users/developers

### Proof of Concept

Take a look at https://github.com/code-423n4/2023-10-zksync-findings/issues?q=175

Focus on the primary issue and its' duplicate, they all talk about how they are behavorial inconsistencies in precompiles when they are delegate called into, with suggesting that the delegateCall() function of the EfficientCall() should be reimplemented to check if this precompiles are to be called and instead pass the call in as a staticcall, issue is that, as shown in the snippet below no change has been made to this function attached with the fact that no documentations attached to the natspec with this bug case, i.e https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/EfficientCall.sol#L83-L95

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

## [10] Consider renaming `CURRENT_MAX_PRECOMPILE_ADDRESS` to `MAX_POSSIBLE_PRECOMPILE_ADDRESS`

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

Case is that the current name suggests that there are 255 addresses already, where as is should mean that the maximal possible address of an L1-like precompile should be 255 as [this comment](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/Constants.sol#L43) hints.

### Impact

Confusing code, makes it harder to understand protocol

### Recommended Mitigation Steps

Consider changing `CURRENT_MAX_PRECOMPILE_ADDRESS` to `MAX_POSSIBLE_PRECOMPILE_ADDRESS`.

## [11] Users funds could still be stuck due to lack of access to `ETH` on the `L2` through `L1->L2 `transactions so this should be clearly documented

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

> NB: Submitting as QA cause whereas sponsors "confirmed" this bug from the previous audit, they tagged it as a `disagree with severity`... but still of the opinion that this is a borderline medium severity bug and leaving at the discretion of the judge.

### Recommended Mitigation Steps

Enable the creation of L1->L2 transactions that can draw upon ETH in the L2 balance as part of the transaction value. Alternatively, implement functionality in the `DefaultAccount::executeTransactionFromOutside` function to ensure it operates as initially intended or this should be clearly documented

## [12] If the pending admin becomes malicious there is no specific way to stop them from accepting the admin

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

## [13] Protocol does not consider EIP-4844 and still assumes more than one batch can be committed

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

### Additional Note

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

## [14] Missing getter functions for key internal `ZkSyncStateTransitionStorage` variables should be introduced

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

## [15] upgrades are automatically immediately possible instead of being able to have a kick in time in the future

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

## [16] The placeholder `_postUpgrade()` has no implementation and is not meant to be used but is being queried twice via both the genesis and normal upgrade pattern

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

## [17] New instances of missing natspec comments

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

## [18] Setters do not have `equality/zero` checkers

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

No input validation in this case leading to an unnecessary execution of code if the value is the same, or even if it's zero.

### Recommended Mitigation Steps

Implement equality checkers in setter functions.

## [19] Multiple instances of where messages within `require` are not descriptive

### Proof of Concept

This is fairly rampant in code, taking the `Admin.sol` as the primary case to prove this bug.
Take a look at these instances:

```solidity
        require(msg.sender == pendingAdmin, "n4"); // Only proposed by current admin address can claim the admin rights


        require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");


        require(_newFeeParams.maxPubdataPerBatch >= _newFeeParams.priorityTxMaxPubdata, "n6");


        require(!diamondStorage.isFrozen, "a9"); // diamond proxy is frozen already


```

Other instances can be scoped out by using this search keyword: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+require%28+NOT+language%3ATypeScript+NOT+language%3AMarkdown&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+require%28+NOT+language%3ATypeScript+NOT+language%3AMarkdown&type=code)

### Impact

Where as some instances have the errored out cases commented out it still does not provide a descriptive case for the `require()` and as such this causes lack of understanding of protocol.

### Recommended Mitigation Steps

Consider adding descriptive messages after each `require()`.

## [20] Deviation from Solidity best styling practices in scoped contracts

### Proof of Concept

Multiple instances of going against the best styling practices one of such can be seen in Executor.sol

Take a look athttps://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L6

```solidity
import {COMMIT_TIMESTAMP_NOT_OLDER, COMMIT_TIMESTAMP_APPROXIMATION_DELTA, EMPTY_STRING_KECCAK, L2_TO_L1_LOG_SERIALIZE_SIZE, MAX_L2_TO_L1_LOGS_COMMITMENT_BYTES, PACKED_L2_BLOCK_TIMESTAMP_MASK, PUBLIC_INPUT_SHIFT, POINT_EVALUATION_PRECOMPILE_ADDR} from "../../../common/Config.sol";
```

Covers the whole screen which should instead include a line break for better readability.

### Impact

Difficulties while reading through code.

### Recommended Mitigation Steps

Follow best styling practices.

## [21] Remove unnecessary code irrelevant to final production

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

Remove this assertion from final released code.

## [22] Alpha period code is still in production despite the period ending in April 2023

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

## [23] Redeployment considerations for `L2ContractHelper/Config.sol` in case of updates

### Proof of Concept

Several functions and constants within `L2ContractHelper/Config.sol` are utilized by multiple Diamond facets across the smart contract system. Modifications to these shared elements necessitate Governor intervention to update all relevant facets. Non-compliance can lead to inconsistencies and potentially critical issues due to mismatched functionality across facets.

A search using the following query confirms this concern:[https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+L2ContractHelper.hashL2Bytecode&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+L2ContractHelper.hashL2Bytecode&type=code)

The search results demonstrate that the `hashL2Bytecode` function is employed within various facets, including `BaseZkSyncUpgrade.sol`, `Mailbox.sol`, `L1ERC20Bridge.sol`, and `L1EthBridge.sol`. Consequently, a change to `hashL2Bytecode` would necessitate redeploying all four of these facets.

### Impact

Low

### Recommended Mitigation Steps

To eliminate the need for widespread redeployments upon updates to `L2ContractHelper` and `Config.sol`, we propose integrating them as Diamond facets themselves. This approach enables other facets to access the functions and constants through cross-facet calls, while external contracts can interact with them via the Diamond. With this structure, modifications only require redeploying and replacing the specific facet containing the updated elements.

This mitigation strategy streamlines the update process for shared functionalities, minimizing the need for extensive redeployment across multiple facets.

## [24] `L1SharedBridge.sol` might encounter accounting errors

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

Now whereas protocol does not work currently with `FOT` tokens, there are tokens that exist that could have their implementations be update to support fees, effectively breaking protocol if that were to happen.

### Impact

Funds are potentially stuck in the ERC20 bridge, also core functionality is broken, being that `transferFundsFromLegacy()` won't work for these tokens.

### Recommended Mitigation Steps

In as much as the aim of transfering these tokens from the ERC20 bridge is to clear the bridge of the tokens in it, then the finalization check could be changed from `balanceAfter - balanceBefore == amount` and instead implemented as a check that ensures that `IERC20(_token).balanceOf(address(legacyBridge)) == 0` after the transaction.

## [25] The `Ecrecover` gas cost been massively increased without significant increases in executional cost

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

## [26] zkEVM's `CodeOracle` Precompile somewhat deviates from EVM's `extcodecopy` behavior

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

## [27] Protocol currently does not consider all windows in regards to `minDelay`

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

One window allows the owner to bypass the security council's oversight by setting the minimum approval delay for operations to zero. This timeframe, known as `minDelay`, is crucial because it gives the security council time to review and potentially cancel operations proposed by the admin. With `minDelay` at zero, the security council's approval becomes irrelevant, and the admin can execute operations unilaterally. This undermines the two-actor security model intended for governance.

> NB: It might as well not be `zero`, but a very short time frame, idea is still the same.

Another window stems from inconsistencies between different time delays used during upgrade scheduling. These delays include `minDelay` (time for security council review), `UPGRADE_NOTICE_PERIOD` (user notification window), and `executionDelay` (delay before upgrade execution on L1). If `minDelay` or `UPGRADE_NOTICE_PERIOD` are shorter than `executionDelay`, it can lead to unpredictable outcomes for users. Users' withdrawal requests might be stuck in limbo or executed before the upgrade, causing them to miss out on crucial information or protections.

For instance, the time delay inconsistencies could be problematic to the upgrade process in a way that impacts users attempting to withdraw ETH before an upgrade, say the `finalizeEthWithdrawal()` gets updgraded to function a bit different, users who had their transactions going on would be directly impacted.

### Recommended Mitigation Steps

Enforce minimum `minDelay`, the `updateDelay` function should be modified to include a requirement that `_newDelay` be greater than `ValidatorTimelock.executionDelay()` with an additional buffer of at least 2 days to account for potential validator delays. This ensures the security council has sufficient time to review operations.

Also, consider establishing a dependency between `minDelay` (or `UPGRADE_NOTICE_PERIOD`) and `executionDelay`. This could involve enforcing `minDelay` to be always greater than `executionDelay` with a reasonable buffer.

## [28] `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion()` should not allow the protocol version difference to be up to `MAX_ALLOWED_PROTOCOL_VERSION_DELTA`

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

## [29] Users failed tx could be unclaimable from the shared bridge

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

Function is inevitably called when claiming the failed deposits case here is that the logic for this hardcodes the receiver and expects it to be able to deal with the tokens, now different things could be the cause of the address not being able to handle tokesn, for example say the `_depositSender` can't handle eth or has no receive function, or for the case of a normal token, assume they get blacklisted or some other sort of issues, tokens are indefinitely locked in the bridge.

### Impact

Low, since this somewhat relies on user not using an address that can accept their failed deposits from the get go.

### Recommended Mitigation Steps

As a popular receommendation, it's advisable to implement a pull method for withdrawals, i.e users should be allowed to provide a fresh deposit address than forcing it into the one that made the deposit.

> NB: Whereas acknowledged findings have been said to be OOS, I'm considering a fresh case of the bug and submitting since this is a new contract and hasn't been reported before.

## [30] Apply fixes to commented out bug cases

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

## [31] Unnecessary duplication of checks

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

The check can be left just to the internal function while finalizing the withdrawal.

## [32] Non-existent facets would be assumed to be unfreezable due to the wrong conditional keyword in `isFacetFreezable()`

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

Users would be confused at this, since there is no difference between unfreezable facets and non-existent ones considering the current implementation of `isFacetFreezable()`.

### Recommended Mitigation Steps

Consider changing the `if()` condition to `require()` that way only real unfreezable facets would return `false`.

## [33] Remove the trailing comma after queries to `isNotEnoughGasForPubdata` in the bootloader to enforce no error in the Yul Syntax

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

## [34] Consider rightly passing the elements of the `BridgehubL2TransactionRequest` in `_requestL2Transaction()`

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

One can see that, within the `requestL2Transaction()` execution the positions of `l2GasLimit` and the `calldata` bytes are swapped which would cause the ABI encoding/decoding of this struct be faulty or even cause an issue with the generation of the proof of this transaction

### Impact

Better code structure.

### Recommended Mitigation Steps

Consider passing in the struct in the right manner

## [35] Resolve newly introduced TODOs

### Proof of Concept

Using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20TODO&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20TODO&type=code) we can see that there are more than 22 code files that are left with multiple todos (a notable mention is that some contracts have only one nonetheless this should be fixed)

### Impact

Open Todos often hint that the codes are not ready for final production/deployment.

### Recommended Mitigation Steps

Fix open todos

 ## [36]  `OperationState.Waiting` should be considered the case even when `timestamp == block.timestamp`

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

Low, info on better code structure.

### Recommended Mitigation Steps

Make the `OperationState.Waiting` check inclusive.

## [37] Redundant return of the nonce deployed

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

Redundant code, bad structure.

### Recommended Mitigation Steps

Always remove redundant code from production code.

## [38] Chunking the pubdata should be made more efficient

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

Wastage of gas.

### Recommended Mitigation Steps

Consider making the change in as much as the values are going to be constants.

## [39] Owner can still access `renounceOwnership()`

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

## [40] There exist a light deviation between the Ethereum VM and zK's in regards to eth deposits

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

## [41] `0.8.20` is vulnerable to some bugs and compiler version should be updated to be on the safe side

### Proof of Concept

See https://github.com/ethereum/solidity/blob/afda6984723fca99e82ebf34d0aec1804f1f3ce6/docs/bugs_by_version.json#L1865-L1871
we can see that this compiler version is vulnerable to:

- Use this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20.selector&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync%20.selector&type=code), we can see that protocol in multiple instances implement the `.selector()` query, would be key to note that, as explained in [this blog](https://soliditylang.org/blog/2023/07/19/missing-side-effects-on-selector-access-bug/) there are multiple side effects with accessing .selector() for the current compiler version, since it could cause potentially incorrect behavior of contracts compiled using the legacy pipeline.

-Considering the protocol's heavy use of `yul`, a different version of compiler should be used, cause this version is vulnerable to the full inliner non expression split argument evaluation order bug, explained [here](https://blog.soliditylang.org/2023/07/19/full-inliner-non-expression-split-argument-evaluation-order-bug/), do note that this could heavily cause reordering reverts in the bootloader or even it's return may lead to storage writes, memory writes, or event emissions not being performed. It may also lead to the contract not reverting (and therefore not rolling back some operations) when it should or vice-versa, and as such an updated version should be used.

- Lastly, would be key to note that `verbatim` is also used heavily protocol, for example even in the blob versioned hash receiver https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/utils/BlobVersionedHashRetriever.yul but this is also a tad affected by this compiler's verion of being vulnerable to the [verbatim invalid deduplication bug](https://soliditylang.org/blog/2023/11/08/verbatim-invalid-deduplication-bug/), note that the TLDR of this bug as understood is that wherein equivalent assembly blocks are identified and merged. `verbatim` assembly items surrounded by identical opcodes were incorrectly considered identical and unified, that's in the Block Deduplicator optimizer step, currently the `BlobVersionedHashRetriever.yul` only queries the verbatim, just once so no issue of the bug coming in place to unify similar blocks.

### Recommended Mitigation Steps

Consider updating the solididity compiler version.

## [42] `execute()` & `executeInstant()` could use `msg.value` in a better manner

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

## [43]&nbsp;`StateTransitionManager.sol::createNewChain()` has some nuances with it's `initData`

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

Evidently, the logic for `initData` seems to expect 292 bytes, hence this comment: " /// all together 4+9&ast;32=292 bytes" but going through the logic below, we can see that the function after passing in the `292` bytes, i.e the selector and all 9 `byte32` elements, it still passes the initData to be concated, which seems as a flawed logic as the whole concated value is later on set as the same `initData`.

### Impact

Bad code structure, `initData` is expected to be `292` bytes but is accepted to be longer.

### Recommended Mitigation Steps

Consider clearly limiting this to `292` bytes or clearly document that this is to be extended in the future.

## [44] Double addressed tokens can be stolen from the bridge

### Proof of Concept

While depositing the contract calls to see if the deposits have been cleared with token addresses, case here is that in most of the logic, it doesn't consider that a user can just specify the second address if the first one doesn't go through.

### Recommended Mitigation Steps

Consider not supporting these types of tokens.

## [45] Fix bootloader's documentation in regards to unread memory points

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

## [46] Protocol should consider supporting deposits of pure erc20s

### Proof of Concept

Here is how a token's deposit gets finalized: https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L97

That is the contract creates the token address if the deposit for this token has never been made, but before that the user needs to deposit their tokens via the L1 shared bridge.

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

Reimplement a logic to allow for the support of pure eip20 tokens.

## [47] Remove instances of unnecessary casting

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

Remove the unnecessary casting.

## [48] Always update comments in code if it's already the deadline

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

Consider having a more specific time in regards to when the breaking change would occur.

## [49] Fix documentation in regards to timing requirements so code doesn't deviate from docs

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

## [50] Airdrops are automatically lost for the `L1ERC20Bridge`

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol

Contract is obviously a bridge that allows for the depositing of ERC20 tokens to hyperchains, this means that the contract at some point would hold a lot of tokens and could be eligible for some airdrops, since its most likely going to be based on the snapshot of the token balance, now clearly this contract does not entail any sweeping functions and as such all airdrops sent to this contract are effectively stuck

### Impact

Leak of value since there are no methods to get hold of the airdrops.

### Recommended Mitigation Steps

Introduce a sweeper functionality for these cases.

## [51] `TransactionHelper::isEthToken()` is not used anywhere, so it should be removed

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L89-L97

```solidity

    function isEthToken(uint256 _addr) internal pure returns (bool) {
        return _addr == uint256(uint160(address(BASE_TOKEN_SYSTEM_CONTRACT))) || _addr == 0;
    }

```

This function is used to know whether the `address` passed is th `Ether` address, and also returns true if the address passed is `0x0` (for conveniency) as stated [here](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/system-contracts/contracts/libraries/TransactionHelper.sol#L92), issue with this is tht using this search command: [https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+isEthToken&type=code](https://github.com/search?q=repo%3Acode-423n4%2F2024-03-zksync+isEthToken&type=code) we can see that this function is not used anywhere.

### Impact

Remove redundant code as they most of the time hint flawed implementation.

### Recommended Mitigation Steps

Remove the `isEthToken()` function since it's not being used anywhere.

## [52] The` storedBatchHash()` fails to distinguish between reverted and unreverted batches

### Proof of Concept

Take a look at https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Getters.sol#L121-L125

```solidity
    /// @inheritdoc IGetters
    function storedBatchHash(uint256 _batchNumber) external view returns (bytes32) {
        return s.storedBatchHashes[_batchNumber];
    }
```
Now consider this previously confirmed issue: https://github.com/code-423n4/2023-10-zksync-findings/issues?q=is%3Aissue+is%3Aopen+Inaccurate+Batch+Stored+Hash+Retrieval+in+Getters+Contract

Case with the function's implementation is that, it returns zero for uncommitted batch numbers, but it lacks the capability to distinguish between a reverted and an unreverted batch. For example, if batch number 500 has been reverted, and a user queries `storedBatchHash(500)`, it returns a non-zero value, which may create the impression that the batch is unreverted. However, it should ideally return zero in such scenarios.

Now evidently this is from a past report, but whereas protocol pronounced "acknowledged" findings to be OOS, this was `confirmed` and as such must have forgotten to be fixed.

### Impact

Users would be misled on the status for batches in zkSync.

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

## [53] Users would assume proof verification is performed twice in `proveBatches()` due to a wrongly commenting out the `else` keyword and lack of documentation

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
This function eventually gets called when proving the batches, now as tagged by "@audit", evidently, if the proof is not empty, it gets verified, due to the `if` block.

Where as one might look at this and assume there to be a logical error, as naturally if we are having an `if/else` conditional arrangement, then the else block should entain a different execution, but here that's not the case cause the preprocessor is going to remove one of the ` _verifyProof(proofPublicInput, _proof);`

### Impact

Bad code structure, unclear documentation.

### Recommended Mitigation Steps

Correctly apply the documentations attached to this.

## [54] Wrong error message in `BaseZkSyncUpgradeGenesis::_setNewProtocolVersion`

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

Inaccurate error messages, code confusion.

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
***

# Gas Optimizations

For this audit, 12 reports were submitted by wardens detailing gas optimizations. The [report highlighted below](https://github.com/code-423n4/2024-03-zksync-findings/issues/55) by **lsaudit** received the top score from the judge.

*The following wardens also submitted reports: [ChaseTheLight](https://github.com/code-423n4/2024-03-zksync-findings/issues/74), [slvDev](https://github.com/code-423n4/2024-03-zksync-findings/issues/68), [Pechenite](https://github.com/code-423n4/2024-03-zksync-findings/issues/58), [DadeKuma](https://github.com/code-423n4/2024-03-zksync-findings/issues/42), [hihen](https://github.com/code-423n4/2024-03-zksync-findings/issues/32), [oualidpro](https://github.com/code-423n4/2024-03-zksync-findings/issues/23), [Sathish9098](https://github.com/code-423n4/2024-03-zksync-findings/issues/19), [rjs](https://github.com/code-423n4/2024-03-zksync-findings/issues/129), [aua\_oo7](https://github.com/code-423n4/2024-03-zksync-findings/issues/108), [Bauchibred](https://github.com/code-423n4/2024-03-zksync-findings/issues/106), and [K42](https://github.com/code-423n4/2024-03-zksync-findings/issues/83).*

To improve the report readability and its transparency - the report is divided into two sections. The first section contains issues evaluated during the manual process of code-review. It focuses on two types of findings:
* Full optimizations - e.g., "Function `X()` can be optimized" - which describes multiple of optimizations related to a single feature. Each issue requires some code refactoring.
* Issue related optimization - e.g., repacking of structs, changing orders of `require` statements, etc. Each of these issue required a manual review, which allowed us to confirm that the optimization would indeed save some gas. The manual process allowed us to provide a short explanation, why the proposed solution will save gas.

The second section - is related to automated findings. These findings - will - most likely - be ignored and their proposed fixes not implemented, because they significantly affect the code readability and provide just a minimal gas savings. These findings describe issues like: using assembly for simple operations, marking constructors as payable, etc. Nonetheless, we've decide to contain them in the report for the completeness. 
Since during the automated process - we have been using own tooling, we've decide to simplify some of its detectors and re-write them as a simple `grep` commands. To improve the report quality and readability, we've decide to not list the exact instances found during the automated process - but instead, we've provided a simple `grep` instruction, which allows to identified those issue by the reader.
Finding marked as `[AUTOMATED-FINDING-N]` describes how to use `grep` to identify most of the instances related to each finding. Please notice, that those `grep` instructions won't identify every affected instance - but in most cases - they will report enough results to understand the crux of the issue.
In the automated findings, we've piped our `grep` detectors by `| wc -l`, just to demonstrate how many instances are affected. To list exact lines affected, please remove it from the command.

## [G-01] Function `_revertBatches()` can be optimized

**File:** `Executor.sol`

This issue contains multiple of optimizations which requires code refactoring. Thus it was reported as separated finding.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L481)
```solidity
481:     function _revertBatches(uint256 _newLastBatch) internal {
482:         require(s.totalBatchesCommitted > _newLastBatch, "v1"); // The last committed batch is less than new last batch
483:         require(_newLastBatch >= s.totalBatchesExecuted, "v2"); // Already executed batches cannot be reverted
484: 
485:         if (_newLastBatch < s.totalBatchesVerified) {
486:             s.totalBatchesVerified = _newLastBatch;
487:         }
488:         s.totalBatchesCommitted = _newLastBatch;
489: 
490:         // Reset the batch number of the executed system contracts upgrade transaction if the batch
491:         // where the system contracts upgrade was committed is among the reverted batches.
492:         if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) {
493:             delete s.l2SystemContractsUpgradeBatchNumber;
494:         }
495: 
496:         emit BlocksRevert(s.totalBatchesCommitted, s.totalBatchesVerified, s.totalBatchesExecuted);
```
At line 488, we assign `_newLastBatch` to state variable `s.totalBatchesCommitted`. Since this value is not being changed, we can re-use `_newLastBatch` at line 496, to avoid additional reading of a state variable: `emit BlocksRevert(_newLastBatch, s.totalBatchesVerified, s.totalBatchesExecuted);`.

Moreover, `s.totalBatchesExecuted` is used twice and can be cached.

At line 485, when the condition if fulfilled, we will be reading `s.totalBatchesVerified` three times (line 485, 486, 487). We can re-factor the code to avoid additional reading of `s.totalBatchesVerified`. This is what needs to be done:
1. move `s.totalBatchesCommitted = _newLastBatch` higher 
2. move `if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch)` higher
3. rewrite `if (_newLastBatch < s.totalBatchesVerified)` to `if`-`else` condition, when `if` block will be executed, we will avoid additional reading.
Please notice that in that case, we will read `s.totalBatchesVerified` only twice (explained in the comment section)

```
   function _revertBatches(uint256 _newLastBatch) internal {
        require(s.totalBatchesCommitted > _newLastBatch, "v1"); 
        uint256 cachedtotalBatchesExecuted = s.totalBatchesExecuted;
        require(_newLastBatch >= cachedtotalBatchesExecuted, "v2"); 

        s.totalBatchesCommitted = _newLastBatch;  // line 488 can be moved higher

        if (s.l2SystemContractsUpgradeBatchNumber > _newLastBatch) { // line 497 can be moved higher
            delete s.l2SystemContractsUpgradeBatchNumber;
        }

        if (_newLastBatch < s.totalBatchesVerified) { // first read of `s.totalBatchesVerified`
            s.totalBatchesVerified = _newLastBatch;  // when if returns true, 2nd read of `s.totalBatchesVerified`
            emit BlocksRevert(_newLastBatch, _newLastBatch, cachedtotalBatchesExecuted);  // we can use _newLastBatch now
        } else  {
            emit BlocksRevert(_newLastBatch, s.totalBatchesVerified, cachedtotalBatchesExecuted); // when if returns false, 2nd read of `s.totalBatchesVerified`
        }
 
    }
```
## [G-02] Function `setNewBatch()` from `SystemContext.sol` can be optimized

**File:** `SystemContext.sol`
This issue requires code-refactoring of some code, thus it was reported separately.

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L452)
```solidity
452:         require(previousBatchNumber + 1 == _expectedNewNumber, "The provided block number is not correct");
453: 
454:         _ensureBatchConsistentWithL2Block(_newTimestamp);
455: 
456:         batchHashes[previousBatchNumber] = _prevBatchHash;
457: 
458:         // Setting new block number and timestamp
459:         BlockInfo memory newBlockInfo = BlockInfo({number: previousBatchNumber + 1, timestamp: _newTimestamp});
```
There's unnecessary addition, which can be removed from above function. Let's take a look at lines 452 and 459: `previousBatchNumber + 1`.
Since line 452 requires, that `previousBatchNumber + 1 == _expectedNewNumber` (otherwise, function will revert), we can be sure, that `_expectedNewNumber == previousBatchNumber + 1`. This implies, that at line 459, instead of using addition again, we can simply use `_expectedNewNumber` instead:

```
459:         BlockInfo memory newBlockInfo = BlockInfo({number: _expectedNewNumber, timestamp: _newTimestamp});
```

This will save us from spending additional gas on unnecessary operation.

## [G-03] Function `initialize()` in `L2SharedBridge.sol` can be optimized

**File:** `L2SharedBridge.sol`

This issue requires code-refactoring of some code, thus it was reported separately.

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L60)
```solidity
60:         l1Bridge = _l1Bridge;
61:         l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;
62: 
63:         if (block.chainid != ERA_CHAIN_ID) {
64:             address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
65:             l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
66:             l2TokenBeacon.transferOwnership(_aliasedOwner);
67:         } else {
68:             require(_l1LegecyBridge != address(0), "bf2");
69:             // l2StandardToken and l2TokenBeacon are already deployed on ERA, and stored in the proxy
70:         }
```
When `block.chainid` is `ERA_CHAIN_ID` and `_l1LegecyBridge` is `address(0)` - we can revert earlier, without wasting gas on reading state variables: `l1Bridge` and `l2TokenProxyBytecodeHash`.
Moreover, we can use `==` operator, instead of `!=`.

```
        if (block.chainid == ERA_CHAIN_ID) {
        require(_l1LegecyBridge != address(0), "bf2");
        } else {
            address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
            l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
            l2TokenBeacon.transferOwnership(_aliasedOwner);
        }
        l1Bridge = _l1Bridge;
        l2TokenProxyBytecodeHash = _l2TokenProxyBytecodeHash;

```
## [G-04] Refactor `Diamond.sol` by inlining `_saveFacetIfNew()` function

**File:** `Diamond.sol`

This issue is reported as a separate finding, since it requires multiple of changes in the code base.
Our recommendation is to inline `_saveFacetIfNew()` to avoid additional SSTORE performed by `DiamondStorage storage ds = getDiamondStorage()`.

[File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L189)
```solidity
189:     function _saveFacetIfNew(address _facet) private {
190:         DiamondStorage storage ds = getDiamondStorage();
191: 
192:         uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;
193:         // If there are no selectors associated with facet then save facet as new one
194:         if (selectorsLength == 0) {
195:             ds.facetToSelectors[_facet].facetPosition = ds.facets.length.toUint16();
196:             ds.facets.push(_facet);
197:         }
198:     }
```
Function `_saveFacetIfNew()` executes `DiamondStorage storage ds = getDiamondStorage();` (line 189).
We can spot, that function `_saveFacetIfNew()` is called inside `_addFunctions()` and `_replaceFunctions()`. Those functions - at the beginning of their implementation perform the same operation: `DiamondStorage storage ds = getDiamondStorage();`.
This basically means, that `DiamondStorage storage ds = getDiamondStorage();` is redundant in the `_saveFacetIfNew()`. We can inline `_saveFacetIfNew()` in `_addFunctions()` and `_replaceFunctions()` to avoid repeating `DiamondStorage storage ds = getDiamondStorage();`.

## [G-05] Alter some struct's fields datatype to improve packing

**Files:** `Messaging.sol`, `BaseZkSyncUpgrade.sol`, `IExecutor.sol`

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L28)
```solidity
28: struct ProposedUpgrade {
29:     L2CanonicalTransaction l2ProtocolUpgradeTx;
30:     bytes[] factoryDeps;
31:     bytes32 bootloaderHash;
32:     bytes32 defaultAccountHash;
33:     address verifier;
34:     VerifierParams verifierParams;
35:     bytes l1ContractsUpgradeCalldata;
36:     bytes postUpgradeCalldata;
37:     uint256 upgradeTimestamp;
38:     uint256 newProtocolVersion;
39: }
```
`newProtocolVersion` is being increases every time upgrade is made. `upgradeTimestamp` contains the timestamp of the upgrade. Both these fields can be `uint128` (instead of `uint256`) to fit into one slot.

[File: code/contracts/ethereum/contracts/common/Messaging.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/Messaging.sol#L098)
```solidity
098: struct L2CanonicalTransaction {
099:     uint256 txType;
100:     uint256 from;
101:     uint256 to;
102:     uint256 gasLimit;
103:     uint256 gasPerPubdataByteLimit;
104:     uint256 maxFeePerGas;
105:     uint256 maxPriorityFeePerGas;
106:     uint256 paymaster;
107:     uint256 nonce;
108:     uint256 value;
```

Both `nonce` and `txType` fields can be `uint128 ` to fit into single slot.
Both `gasLimit` and `gasPerPubdataByteLimit` can be `uint128` to fit into single slot.

[File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83)
```solidity
83:     struct StoredBatchInfo {
84:         uint64 batchNumber;
85:         bytes32 batchHash;
86:         uint64 indexRepeatedStorageChanges; 
87:         uint256 numberOfLayer1Txs;
88:         bytes32 priorityOperationsHash;
89:         bytes32 l2LogsTreeRoot;
90:         uint256 timestamp;
91:         bytes32 commitment;
92:     }
```
`timestamp` field can be `uint64`. Then, it can be moved after `batchNumber` to fit a single slot (`uint64` + `uint64`).

## [G-06] State variables may be packed into fewer storage slots

**File:** `Governance.sol`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L26)
```solidity
26:     address public securityCouncil;
27: 
28:     /// @notice A mapping to store timestamps when each operation will be ready for execution.
29:     /// @dev - 0 means the operation is not created.
30:     /// @dev - 1 (EXECUTED_PROPOSAL_TIMESTAMP) means the operation is already executed.
31:     /// @dev - any other value means timestamp in seconds when the operation will be ready for execution.
32:     mapping(bytes32 operationId => uint256 executionTimestamp) public timestamps;
33: 
34:     /// @notice The minimum delay in seconds for operations to be ready for execution.
35:     uint256 public minDelay;
```
Consider changing `minDelay` type from `uint256` to `uint64`. Then, it could be packed in a single storage slot with `address public securityCouncil`.

## [G-07] In `NonceHolder.sol`, ID mappings can be combined into a single `mapping` of an ID to a `struct`

**File:** `NonceHolder.sol`

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L36)
```solidity
36:     mapping(uint256 account => uint256 packedMinAndDeploymentNonce) internal rawNonces;
37: 
38:     /// Mapping of values under nonces for accounts.
39:     /// The main key of the mapping is the 256-bit address of the account, while the
40:     /// inner mapping is a mapping from a nonce to the value stored there.
41:     mapping(uint256 account => mapping(uint256 nonceKey => uint256 value)) internal nonceValues;
```

## [G-08] Repack struct by putting data types that fit together into one slot next to each other

This issue, in comparison to `# [5] Alter some struct's fields datatype to improve packing`  is related to changing the order of fields in the struct (while `[5]` suggests changing the datatype of fields) - thus it's being reported separately.

**File:** `IExecutor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-interfaces/IExecutor.sol#L83)
```solidity
83:     struct StoredBatchInfo {
84:         uint64 batchNumber;
85:         bytes32 batchHash;
86:         uint64 indexRepeatedStorageChanges; 
87:         uint256 numberOfLayer1Txs;
88:         bytes32 priorityOperationsHash;
89:         bytes32 l2LogsTreeRoot;
90:         uint256 timestamp;
91:         bytes32 commitment;
92:     }
```

`batchNumber` and `indexRepeatedStorageChanges` will fit into one slot.


## [G-09]  Avoid reading state variable twice

**Files:** `SystemContext.sol`, `L2StandardERC20.sol`

Reading state variables costs a lot of gas. It's better to always cache the state variable into local variable and read the local variable instead.

[File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L093)
```solidity
093:         try this.decodeUint8(decimalsBytes) returns (uint8 decimalsUint8) {
094:             // Set decoded value for decimals.
095:             decimals_ = decimalsUint8;
096:         } catch {
097:             getters.ignoreDecimals = true;
098:         }
099: 
100:         availableGetters = getters;
101:         emit BridgeInitialize(_l1Address, decodedName, decodedSymbol, decimals_);
```
Variable `decimals_` is a state variable, thus reading it costs more gas than local variable.
Please notice, that we're reading this variable twice - firstly, at line 95, then at line 101.

Reading state variables multiple of times costs a lot of gas. Much more effective solution would be to just read it once and cache the result into local variable.

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L117)
```solidity
117:     function getCurrentPubdataSpent() public view returns (uint256) {
118:         uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
120:     }
```

To avoid reading `basePubdataSpent` twice, above code can be rewritten to:

```
    function getCurrentPubdataSpent() public view returns (uint256) {
        uint256 cachedBasePubdataSpent = basePubdataSpent;
        uint256 pubdataPublished = SystemContractHelper.getZkSyncMeta().pubdataPublished;
        return pubdataPublished > cachedBasePubdataSpent ? pubdataPublished - cachedBasePubdataSpent : 0;
    }
```

## [G-10] Refactor functions with events which emit both new and old values

**Files:** `StateTransitionManager.sol`, `Admin.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L23)
```solidity
23:     function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
24:         // Save previous value into the stack to put it into the event later
25:         address oldPendingAdmin = s.pendingAdmin;
26:         // Change pending admin
27:         s.pendingAdmin = _newPendingAdmin;
28:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
29:     }
```

To avoid creating additional variable `oldPendingAdmin` which stores `s.pendingAdmin` before the update - we can move emitting event one line above:

```
   function setPendingAdmin(address _newPendingAdmin) external onlyAdmin {
        emit NewPendingAdmin(s.pendingAdmin, _newPendingAdmin);
        s.pendingAdmin = _newPendingAdmin;  
    }
```

The same issue was observed in other instances:

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110)
```solidity
110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
111:         // Save previous value into the stack to put it into the event later
112:         address oldPendingAdmin = pendingAdmin;
113:         // Change pending admin
114:         pendingAdmin = _newPendingAdmin;
115:         emit NewPendingAdmin(oldPendingAdmin, _newPendingAdmin);
116:     }
```

Should be changed as above.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L58)
```solidity
58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager { 
59:         require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
60: 
61:         uint256 oldPriorityTxMaxGasLimit = s.priorityTxMaxGasLimit;
62:         s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
63:         emit NewPriorityTxMaxGasLimit(oldPriorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
64:     }
```

can be changed to:

```
    function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager { 
        require(_newPriorityTxMaxGasLimit <= MAX_GAS_PER_TRANSACTION, "n5");
        emit NewPriorityTxMaxGasLimit(s.priorityTxMaxGasLimit, _newPriorityTxMaxGasLimit);
        s.priorityTxMaxGasLimit = _newPriorityTxMaxGasLimit;
        
    }
```
## [G-11] Do not calculate the length of array multiple of times

**Files:** `L2ContractHelper.sol`, `Compressor.sol`, `BaseZkSyncUpgrade.sol`, `PubdataChunkPublisher.sol`, `Executor.sol`, `DiamondProxy.sol`

While calculating the length of an array costs a lot of gas - it's recommended to calculate it once and then, cache the result inside the local variable.
Please notice that this is NOT the same issue as bot-report mentions. The bot-report contains instances of calculating array's length in the loop iterator, e.g.: `for (uint i=0; i < array.length; i++)`, while this issue reports that the length of the array is calculated within the loop (line 42).

[File: code/system-contracts/contracts/PubdataChunkPublisher.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/PubdataChunkPublisher.sol#L36)
```solidity
36:         for (uint256 i = 0; i < MAX_NUMBER_OF_BLOBS; i++) {
37:             uint256 start = BLOB_SIZE_BYTES * i;
38: 
39:             // We break if the pubdata isn't enough to cover 2 blobs. On L1 it is expected that the hash
40:             // will be bytes32(0) if a blob isn't going to be used.
41:             if (start >= _pubdata.length) {
42:                 break;
43:             }
```

In function `chunkAndPublishPubdata()`, the length of array is calculated on every loop iteration.

[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L52)
```solidity
52:                 encodedData.length * 4 == _bytecode.length,
53:                 "Encoded data length should be 4 times shorter than the original bytecode"
54:             );
55: 
56:             require(
57:                 dictionary.length / 8 <= encodedData.length / 2,
58:                 "Dictionary should have at most the same number of entries as the encoded data"
59:             );
60: 
61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
63:                 require(indexOfEncodedChunk < dictionary.length, "Encoded chunk index is out of bounds");
```

`encodedData.length` is calculated 3 times (lines 52, 57, 61). Calculate it once and cache its value to local variable.
`dictionary.length` is calculated 2 times (line 57, 63). Calculate it once and cache its value to local variable.

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L23)
```solidity
23:         require(_bytecode.length % 32 == 0, "pq");
24: 
25:         uint256 bytecodeLenInWords = _bytecode.length / 32;
```
`_bytecode.length` is calculated twice, it would be more efficient to calculate it once and cache the result before line 23.

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223)
```solidity
223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
225: 
226:         for (uint256 i = 0; i < _factoryDeps.length; ++i) {
```
`_factoryDeps.length` is calculated 3 times (lines 223, 224, 226). Calculate it once and cache the result into local variable before line 223.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L25)
```solidity
25:         require(msg.data.length >= 4 || msg.data.length == 0, "Ut");
```

`msg.data.length` is calculated twice. Calculate it once and cache the result into local variable.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L631)
```solidity
631:         require(_pubdataCommitments.length > 0, "pl");
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
634:         blobCommitments = new bytes32[](MAX_NUMBER_OF_BLOBS);
635: 
636:         for (uint256 i = 0; i < _pubdataCommitments.length; i += PUBDATA_COMMITMENT_SIZE) {
```

`_pubdataCommitments.length` is calculated 4 times (lines 631, 632, 633m 636). Calculate it once and cache the result into local variable.

## [G-12] Proof verification in `Executor.sol` is performed twice 

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L429)
```solidity
429:         if (_proof.serializedProof.length > 0) {
430:             _verifyProof(proofPublicInput, _proof);
431:         }
432:         // #else
433:         _verifyProof(proofPublicInput, _proof);
434:         // #endif
```

When `_proof.serializedProof.length > 0` function will call `_verifyProof(proofPublicInput, _proof)` twice - at line 430 and at line 433.

## [G-13] Divide loop in `_commitBatchesWithSystemContractsUpgrade()` to avoid redundant `if`

**File:** `Executor.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289)
```solidity
289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             // The upgrade transaction must only be included in the first batch.
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
292:             _lastCommittedBatchData = _commitOneBatch(
293:                 _lastCommittedBatchData,
294:                 _newBatchesData[i],
295:                 expectedUpgradeTxHash
296:             );
```

In function `_commitBatchesWithSystemContractsUpgrade()` - on every loop iteration - we check if `i == 0` (line 291). This condition is obviously `true` only during the first loop iteration. It's recommended to divide the loop into two parts:  
```
for (uint256 i = 0; i < 1; i = i.uncheckedInc())
```

```
for (uint256 i = 1; i < _newBatchesData.length; i = i.uncheckedInc())
```

Moreover, this would allow us to declare `expectedUpgradeTxHash` outside the loop - thus we won't spend additional gas on declaring this variable during every loop iteration.

That way, in the second loop we will be able to remove `i == 0` condition.

## [G-14] Pre-compute and cache `domainSeparator` in `TransactionHelper.sol`

**File:** `TransactionHelper.sol`

[File: code/system-contracts/contracts/libraries/TransactionHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/TransactionHelper.sol#L138)
```solidity
138:         bytes32 domainSeparator = keccak256(
139:             abi.encode(EIP712_DOMAIN_TYPEHASH, keccak256("zkSync"), keccak256("2"), block.chainid)
140:         );
```

It's a common pattern to pre-compute and cache domain separator and then, compare it with pre-computed, cached value, instead of calculating it every time.

## [G-15] Create one, specific event, instead of emitting two events in a row

**Files:** `StateTransitionManager.sol`, `Bridgehub.sol`, `Admin.sol`

Instead of spending gas on emitting two events at once, it's better to create one, single event and emit it once.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L40)
```solidity
40:         emit NewPendingAdmin(pendingAdmin, address(0));
41:         emit NewAdmin(previousAdmin, pendingAdmin);
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L127)
```solidity
127:         emit NewPendingAdmin(currentPendingAdmin, address(0));
128:         emit NewAdmin(previousAdmin, pendingAdmin);
```

[File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L68)
```solidity
68:         emit NewPendingAdmin(currentPendingAdmin, address(0));
69:         emit NewAdmin(previousAdmin, pendingAdmin);
```

## [G-16] Redundant casting in `getSize()`

**File:** `PriorityQueue.sol`

[File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L45)
```solidity
45:     function getSize(Queue storage _queue) internal view returns (uint256) {
46:         return uint256(_queue.tail - _queue.head);
47:     }
```

Since both `_queue.tail` and `_queue.head` are `uint256`, there's no need to cast `_queue.tail - _queue.head` to `uint256`. 

## [G-17] Utilize post-incrementing to optimize `pushBack()` function

**File:** `PriorityQueue.sol`

This issue is reported as separate finding, because proposed optimizations require code refactoring.

[File: code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/PriorityQueue.sol#L55)
```solidity
55:     function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {
56:         // Save value into the stack to avoid double reading from the storage
57:         uint256 tail = _queue.tail;
58: 
59:         _queue.data[tail] = _operation;
60:         _queue.tail = tail + 1;
61:     }
```

We can get rid of variable `tail` by using `_queue.tail++` directly in `_queue.data`:

```
function pushBack(Queue storage _queue, PriorityOperation memory _operation) internal {
    _queue.data[_queue.tail++] = _operation;
}
```
## [G-18] Redundant casting of addresses in `isSystemContract()`

**File:** `SystemContractHelper.sol`

[File: code/system-contracts/contracts/libraries/SystemContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L338)
```solidity
338:     function isSystemContract(address _address) internal pure returns (bool) {
339:         return uint160(_address) <= uint160(MAX_SYSTEM_CONTRACT_ADDRESS);
340:     }
```

Solidity allows to compare two addresses without casting them to integer first. This means, that above code can be changed to:

```
return _address <= MAX_SYSTEM_CONTRACT_ADDRESS;
```
## [G-19] Checking balance after the transfer cannot underflow, thus can be unchecked

**File:** `L1ERC20Bridge.sol`

This issue has been reported as separate finding, as it uses different invariant for underflow detection. While another finding uses the invariant that subtraction won't underflow, because `require` guarantees that subtrahend is lower than minuend, this one utilizes the fact that after the transfer, the balance cannot be lower then the balance before the transfer, thus line 165 won't underflow and can be unchecked.

[File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L161)
```solidity
161:         uint256 balanceBefore = _token.balanceOf(address(sharedBridge));
162:         _token.safeTransferFrom(_from, address(sharedBridge), _amount);
163:         uint256 balanceAfter = _token.balanceOf(address(sharedBridge));
164: 
165:         return balanceAfter - balanceBefore;
```

Balance after the transfer cannot be lower then before the transfer, thus `balanceAfter - balanceBefore` won't underflow and can be unchecked.

## [G-20] Removing code related to testing - to decrease the contract size and the deployment costs

**File:** `SystemContext.sol`

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L469)
```solidity
469:     /// @notice A testing method that manually sets the current blocks' number and timestamp.
470:     /// @dev Should be used only for testing / ethCalls and should never be used in production.
471:     function unsafeOverrideBatch(
472:         uint256 _newTimestamp,
473:         uint256 _number,
474:         uint256 _baseFee
475:     ) external onlyCallFromBootloader {
476:         BlockInfo memory newBlockInfo = BlockInfo({number: uint128(_number), timestamp: uint128(_newTimestamp)});
477:         currentBatchInfo = newBlockInfo;
478: 
479:         baseFee = _baseFee;
480:     }
```

Both NatSpec and the code-base suggests that above code is just for testing and should not be on the production.
While it's not possible to use this code in a non-testing environment (`onlyCallFromBootloader` modifier won't let to call this code directly), it's recommended to remove this function.
Getting rid of redundant functions will decrease the contract size, thus less gas will be spent during the deployment process.

## [G-21] Do not assign `offset` in the last call of `UnsafeBytes.readUint256()` in `_parseL2WithdrawalMessage()`

**File:** `L1SharedBridge.sol`

A simple test in Remix IDE has been created, to compare gas usage of assigning more than one value from function call:

```
  function getUints() public pure returns (uint, uint) {return (1, 2);}
   function funcA() public view {
    uint a; uint b; 
    (a, b) = getUints();
    uint g = gasleft();
    (a, b) = getUints();
    console.log(g - gasleft());
   }
    function funcB() public view {
    uint a; uint b; 
    (a, b) = getUints();
    uint g = gasleft();
    (a, ) = getUints();
    console.log(g - gasleft());
   }
```

`funcB()` costs 74 gas, while `funcA()` costs 82 gas. This implies, that we shouldn't assign every parameter from function call if it's not needed.

[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L520)
```solidity
520:             (amount, offset) = UnsafeBytes.readUint256(_l2ToL1message, offset);
```

In the last call of `UnsafeBytes.readUint256(_l2ToL1message, offset)` (line 520), we won't need `offset` anymore, thus we can remove `offset` and change this line to: `(amount, ) = UnsafeBytes.readUint256(_l2ToL1message, offset)`.

## [G-22] Operations capped by `totalSupply` in `L2BaseToken` can be unchecked

**File:** `L2BaseToken.sol`

[File: code/system-contracts/contracts/L2BaseToken.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L2BaseToken.sol#L64)
```solidity
64:     function mint(address _account, uint256 _amount) external override onlyCallFromBootloader {
65:         totalSupply += _amount;
66:         balance[_account] += _amount;
67:         emit Mint(_account, _amount);
68:     }
```
User's balance is capped by `totalSupply`. When `totalSupply += _amount` won't revert (due to overflow) - we can be sure, that `balance[_account] += _amount` won't overflow either, thus line 66 can be unchecked.
Important - please notice, that only line 66: `balance[_account] += _amount` can be unchecked.

## [G-23] Use `delete` to clear data, instead of assigning data to `0`

**File:** `L1Messenger.sol`

[File: code/system-contracts/contracts/L1Messenger.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/L1Messenger.sol#L328)
```solidity
328:         /// Clear logs state
329:         chainedLogsHash = bytes32(0);
330:         numberOfLogsToProcess = 0;
331:         chainedMessagesHash = bytes32(0);
332:         chainedL1BytecodesRevealDataHash = bytes32(0);
```
## [G-24] Redundant `require` in `BaseZkSyncUpgradeGenesis`

**File:** `BaseZkSyncUpgradeGenesis.sol`

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgradeGenesis.sol#L22)
```solidity
22:         require(
23:             // Genesis Upgrade difference: Note this is the only thing change > to >=
24:             _newProtocolVersion >= previousProtocolVersion,
25:             "New protocol version is not greater than the current one"
26:         );
27:         require(
28:             _newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA,
29:             "Too big protocol version difference"
30:         );
```

To not revert, two conditions must occur: `_newProtocolVersion >= previousProtocolVersion` and `_newProtocolVersion - previousProtocolVersion <= MAX_ALLOWED_PROTOCOL_VERSION_DELTA`.
However, please notice, that the first `require` (lines 23-26) is redundant and can be removed. When `_newProtocolVersion < previousProtocolVersion`, function will already revert due to underflow in the second `require` at line 28.
This basically means, that it's enough to leave just only the second `require`: (when the first condition won't be fulfilled, function will revert due to underflow in the 2nd `require`).

## [G-25] Use de Morgan's laws to reduce number of negations 

**File:** `DiamondProxy.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondProxy.sol#L31)
```solidity
31:         require(!diamondStorage.isFrozen || !facet.isFreezable, "q1"); // Facet is frozen
```

According to de Morgan's laws: `!A || !B <=> !(A & B)`, which means we can reduce one negation and rewrite above line to:

```
require(!(diamondStorage.isFrozen && facet.isFreezable), "q1"); // Facet is frozen
```

## [G-26] Do not repeat `if` checks in `_constructContract()`

**File:** `ContractDeployer.sol`

Function `_constructContract()` performs the same conditional `if` check twice. This is a waste of gas:

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L332)
```solidity
332:             if (value > 0) {
333:                 BASE_TOKEN_SYSTEM_CONTRACT.transferFromTo(address(this), _newAddress, value);
334:             }
335:             // 2. Set the constructed code hash on the account
336:             _storeConstructingByteCodeHashOnAddress(_newAddress, _bytecodeHash);
337: 
338:             // 3. Call the constructor on behalf of the account
339:             if (value > 0) {
340:                 // Safe to cast value, because `msg.value` <= `uint128.max` due to `MessageValueSimulator` invariant
341:                 SystemContractHelper.setValueForNextFarCall(uint128(value));
342:             }
```

Firstly, there's a check (line 332) if `value` is bigger then 0. Then, at line 339, the same check is being made again.

## [G-27] Do not import the whole library, when only a few functions from that library are being used

**File:** `Mailbox.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L5)
```solidity
5: import {Math} from "@openzeppelin/contracts/utils/math/Math.sol";
```

`Mailbox.sol` imports the whole `Math.sol` library, while it only uses `Math.max()` function.

## [G-28] Calculate simple operations at once

**File:** `TransactionValidator.sol`

[File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L77)
```solidity
77:             costForComputation = L1_TX_INTRINSIC_L2_GAS;
78: 
79:             // Taking into account the hashing costs that depend on the length of the transaction
80:             // Note that L1_TX_DELTA_544_ENCODING_BYTES is the delta in the price for every 544 bytes of
81:             // the transaction's encoding. It is taken as LCM between 136 and 32 (the length for each keccak256 round
82:             // and the size of each new encoding word).
83:             costForComputation += Math.ceilDiv(_encodingLength * L1_TX_DELTA_544_ENCODING_BYTES, 544);
84: 
85:             // Taking into the account the additional costs of providing new factory dependencies
86:             costForComputation += _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_L2_GAS;
87: 
88:             // There is a minimal amount of computational L2 gas that the transaction should cover
89:             costForComputation = Math.max(costForComputation, L1_TX_MIN_L2_GAS_BASE);
```

Above code performs redundant addition at lines 83, 86. Every time it adds the value to `costForComputation`, instead of doing it only once:

```
            costForComputation = Math.max(L1_TX_INTRINSIC_L2_GAS + Math.ceilDiv(_encodingLength * L1_TX_DELTA_544_ENCODING_BYTES, 544) + _numberOfFactoryDependencies * L1_TX_DELTA_FACTORY_DEPS_L2_GAS, L1_TX_MIN_L2_GAS_BASE);
```

## [G-29] Use `calldata` instead of `memory`, when struct is not being changed

**File:** `TransactionValidator.sol`

[File: code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/TransactionValidator.sol#L46)
```solidity
46:     function validateUpgradeTransaction(L2CanonicalTransaction memory _transaction) internal pure {
```

Function `validateUpgradeTransaction()` verifies fields of `_transaction`, but does not alter it. This implies, that instead of `memory`, `calldata` should be used.

## [G-30] Some operations which won't underflow may be unchecked

**Files:** `GasBoundCaller.sol`, `SystemContext.sol`, `MsgValueSimulator.sol`

[File: code/system-contracts/contracts/GasBoundCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L49)
```solidity
49:         uint256 pubdataAllowance = _maxTotalGas > expectedForCompute ? _maxTotalGas - expectedForCompute : 0;
```

Since `_maxTotalGas > expectedForCompute`, we know that `_maxTotalGas - expectedForCompute` won't underflow, thus it can be unchecked.

[File: code/system-contracts/contracts/GasBoundCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L63)
```solidity
63:         uint256 pubdataSpent = pubdataPublishedAfter > pubdataPublishedBefore
64:             ? pubdataPublishedAfter - pubdataPublishedBefore
65:             : 0;
```

Since `pubdataPublishedAfter > pubdataPublishedBefore`, we know that `pubdataPublishedAfter - pubdataPublishedBefore` won't underflow, thus it can be unchecked.

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L119)
```solidity
119:         return pubdataPublished > basePubdataSpent ? pubdataPublished - basePubdataSpent : 0;
```
Since `pubdataPublished > basePubdataSpent`, we know that `pubdataPublished - basePubdataSpent` won't underflow, thus it can be unchecked.

[File: code/system-contracts/contracts/MsgValueSimulator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/MsgValueSimulator.sol#L53)
```solidity
53:         uint256 userGas = gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS
54:             ? gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS
55:             : 0;
```

Since `gasInContext > MSG_VALUE_SIMULATOR_STIPEND_GAS`, we know that `gasInContext - MSG_VALUE_SIMULATOR_STIPEND_GAS` won't underflow, thus it can be unchecked.

## [G-31]  Use `require` which costs less gas first

**Files:** `Executor.sol`, `BaseZkSyncUpgrade.sol`, `L2SharedBridge.sol`, `Admin.sol`

Because failed `require` revert the whole operation - it's more profitable to use `require` which spends less gas first.

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L87)
```solidity
87:         require(
88:             AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1Bridge ||
89:                 AddressAliasHelper.undoL1ToL2Alias(msg.sender) == l1LegacyBridge,
90:             "mq"
91:         );
92:         require(msg.value == 0, "Value should be 0 for ERC20 bridge");
```

Reading `msg.value` costs less gas than reading `l1Bridge` and `l1LegacyBridge`, thus order of `require` can be changed.

[File: code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/upgrades/BaseZkSyncUpgrade.sol#L223)
```solidity
223:         require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
224:         require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
```

Comparing `_factoryDeps.length` to constant `MAX_NEW_FACTORY_DEPS` costs less gas than comparing it to length of another array: `_expectedHashes.length`. Above code should be changed to:

```
require(_factoryDeps.length <= MAX_NEW_FACTORY_DEPS, "Factory deps can be at most 32");
require(_factoryDeps.length == _expectedHashes.length, "Wrong number of factory deps");
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L105)
```solidity
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
110:         require(
111:             s.protocolVersion == _oldProtocolVersion,
112:             "StateTransition: protocolVersion mismatch in STC when upgrading"
113:         );
```

`s.protocolVersion == _oldProtocolVersion` uses less gas than `cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion)`. The second `require` is just reading, while the first one - calling external function `upgradeCutHash()`. Thus the order of `require` should be changed.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L226)
```solidity
226:         require(
227:             IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion,
228:             "Executor facet: wrong protocol version"
229:         );
230:         // With the new changes for EIP-4844, namely the restriction on number of blobs per block, we only allow for a single batch to be committed at a time.
231:         require(_newBatchesData.length == 1, "e4");
```

`_newBatchesData.length == 1` uses less gas than calling `protocolVersion()` in the first `require`: `IStateTransitionManager(s.stateTransitionManager).protocolVersion() == s.protocolVersion` (especially, that we expect `_newBatchesData.length` to be equal to 1). This implies, that the order of `require` statements should be changed.

## [G-32] Execute `require` before other operations 

**Files:** `GasBoundCaller.sol`, `Executor.sol`

Because `require` reverts the whole operation, it's better to perform `require` statements before any other operation. When `require` reverts, function won't use additional gas for other operations.

[File: code/system-contracts/contracts/GasBoundCaller.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/GasBoundCaller.sol#L40)
```solidity
40:         uint256 expectedForCompute = gasleft() + CALL_ENTRY_OVERHEAD;
[...]
46:         require(_maxTotalGas >= gasleft(), "Gas limit is too low");
```

We can move `require` from line 46 above line 40. When `_maxTotalGas` won't be greater or equal `gasleft()` - function will revert immediately, thus we won't waste additional gas on `expectedForCompute` assignment.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L356)
```solidity
356:         uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
357:         s.totalBatchesExecuted = newTotalBatchesExecuted;
358:         require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.
```

We can move `require` from line 358, before line 357. When condition `newTotalBatchesExecuted <= s.totalBatchesVerified` won't be fulfilled, function will revert without wasting gas on executing line 357. The fixed code should look like this:

```
        uint256 newTotalBatchesExecuted = s.totalBatchesExecuted + nBatches;
        require(newTotalBatchesExecuted <= s.totalBatchesVerified, "n"); // Can't execute batches more than committed and proven currently.
        s.totalBatchesExecuted = newTotalBatchesExecuted;
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L629)
```solidity
629:         uint256 versionedHashIndex = 0;
630: 
631:         require(_pubdataCommitments.length > 0, "pl");
632:         require(_pubdataCommitments.length <= PUBDATA_COMMITMENT_SIZE * MAX_NUMBER_OF_BLOBS, "bd");
633:         require(_pubdataCommitments.length % PUBDATA_COMMITMENT_SIZE == 0, "bs");
```

Move `require` statements from lines 631, 632, 633 above line 629. If any of these `require` revert, function won't waste additional gas on `versionedHashIndex` initialization.
 
## [G-33] Use short-circuiting in OR operations

**File:** `NonceHolder.sol`

Solidity uses short-circuiting while performing OR operations. This means, that in the expression `A() OR B()` - when `A()` evaluates to `true` - expression `B()` won't be executed (because `true OR whatever` evaluates to `true`).
This behavior suggests, that it's better to use less-gas-costly operation first (if it will be evaluated to `true`, Solidity won't waste gas on executing the 2nd operation). 

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L156)
```solidity
156:         return (_nonce < getMinNonce(_address) || nonceValues[addressAsKey][_nonce] > 0);
```

Function `getMinNonce()` reads state variable and performs multiple of other operations. This means, that it uses more gas than just reading `nonceValues[addressAsKey][_nonce]` state variable and comparing it to `0`. Above code should be rewritten to:

```
 return (nonceValues[addressAsKey][_nonce] > 0 || _nonce < getMinNonce(_address));
```

## [G-34] Do not declare variables inside loop

**Files:** `Compressor.sol`, `Mailbox.sol`, `ImmutableSimulator.sol`, `ValidatorTimelock.sol`, `Executor.sol`

Move variable declaration outside the loop. While the variable is declared inside the loop - every loop iteration will spend gas on that variable declaration.

[File: code/system-contracts/contracts/ImmutableSimulator.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ImmutableSimulator.sol#L38)
```solidity
38:             for (uint256 i = 0; i < immutablesLength; ++i) {
39:                 uint256 index = _immutables[i].index;
40:                 bytes32 value = _immutables[i].value;
```

should be changed to:

```
    uint256 index;
    bytes32 value;
    for (uint256 i = 0; i < immutablesLength; ++i) {
        index = _immutables[i].index;
        value = _immutables[i].value;
```
[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L61)
```solidity
61:             for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
```

should be changed to:

```
            uint256 indexOfEncodedChunk;
            for (uint256 encodedDataPointer = 0; encodedDataPointer < encodedData.length; encodedDataPointer += 2) {
                indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L289)
```solidity
289:         for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
290:             // The upgrade transaction must only be included in the first batch.
291:             bytes32 expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
```

Should be changed to:

```
        bytes32 expectedUpgradeTxHash;
        for (uint256 i = 0; i < _newBatchesData.length; i = i.uncheckedInc()) {
            // The upgrade transaction must only be included in the first batch.
            expectedUpgradeTxHash = i == 0 ? _systemContractUpgradeTxHash : bytes32(0);
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L356)
```solidity
356:         for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
357:             bytes32 hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```

Should be changed to:

```
        bytes32 hashedBytecode;
        for (uint256 i = 0; i < factoryDepsLen; i = i.uncheckedInc()) {
            hashedBytecode = L2ContractHelper.hashL2Bytecode(_factoryDeps[i]);
```

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L185)
```solidity
185:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
186:                 uint256 commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
```

Should be changed to:

```
            uint256 commitBatchTimestamp;
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                commitBatchTimestamp = committedBatchTimestamp[ERA_CHAIN_ID].get(
```
[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L209)
```solidity
209:             for (uint256 i = 0; i < _newBatchesData.length; ++i) {
210:                 uint256 commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```

Should be changed to:

```
            uint256 commitBatchTimestamp;
            for (uint256 i = 0; i < _newBatchesData.length; ++i) {
                commitBatchTimestamp = committedBatchTimestamp[_chainId].get(_newBatchesData[i].batchNumber);
```

## [G-35] Avoid declaring unused variables

**File:** `Constants.sol`

[File: code/system-contracts/contracts/Constants.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Constants.sol#L93)
```solidity
93: /// @dev The maximal msg.value that context can have
94: uint256 constant MAX_MSG_VALUE = 2 ** 128 - 1;
```

Constant `MAX_MSG_VALUE` is not used anymore, thus it should be removed from `Constants.sol`

## [G-36] Use bitwise operators instead of multiplication/division by value of 2 to the power of N

**Files:** `L2ContractHelper.sol`, `Compressor.sol`, `Executor.sol`, `Merkle.sol`

[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L52)
```solidity
52:                 encodedData.length * 4 == _bytecode.length,
[...]
57:                 dictionary.length / 8 <= encodedData.length / 2,
[...]
62:                 uint256 indexOfEncodedChunk = uint256(encodedData.readUint16(encodedDataPointer)) * 8;
[...]
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
```

[File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L33)
```solidity
33:             _index /= 2;
```
[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L25)
```solidity
25:         uint256 bytecodeLenInWords = _bytecode.length / 32;
26:         require(bytecodeLenInWords < 2 ** 16, "pp"); // bytecode length must be less than 2^16 words
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Executor.sol#L581)
```solidity
581:             blobAuxOutputWords[i * 2] = _blobHashes[i];
582:             blobAuxOutputWords[i * 2 + 1] = _blobCommitments[i];
```
## [G-37] Code related to local testing should be removed

**Files:** `StateTransitionManager.sol`, `DiamondInit.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/DiamondInit.sol#L49)
```solidity
49:         // While this does not provide a protection in the production, it is needed for local testing
50:         // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
51:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32); 
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L104)
```solidity
104:         // While this does not provide a protection in the production, it is needed for local testing
105:         // Length of the L2Log encoding should not be equal to the length of other L2Logs' tree nodes preimages
106:         assert(L2_TO_L1_LOG_SERIALIZE_SIZE != 2 * 32); 
```

Above `assert()` is just a waste of gas in the production environment. Moreover it increases the size of the contract, thus increases the deployment cost. Our recommendation is to get rid of code related to local testing only.

## [G-38] Dot notation for struct assignment costs less gas

**File:** `Diamond.sol`

Using named arguments for struct means that the compiler needs to organize the fields in memory before doing the assignment, which wastes gas. Set each field directly in storage (use dot-notation), or use the unnamed version of the constructor.

[File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L218)
```solidity
218:         ds.selectorToFacet[_selector] = SelectorToFacet({
219:             facetAddress: _facet,
220:             selectorPosition: selectorPosition,
221:             isFreezable: _isSelectorFreezable
222:         });
```

should be optimized to:

```
ds.selectorToFacet[_selector].facetAddress = _facet;
ds.selectorToFacet[_selector].selectorPosition = selectorPosition;
ds.selectorToFacet[_selector].isFreezable = _isSelectorFreezable;
```

## [G-39] Use AND operators instead of modulo (%) to check if number is odd/even

**Files:** `L2ContractHelper.sol`, `Utils.sol`, `Merkle.sol`, `KnownCodesStorage.sol`

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L43)
```solidity
43:         require(bytecodeLen(_bytecodeHash) % 2 == 1, "uy"); // Code length in words must be odd
```

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L27)
```solidity
27:         require(bytecodeLenInWords % 2 == 1, "ps"); // bytecode length in words must be odd
```

[File: code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Merkle.sol#L30)
```solidity
30:             currentHash = (_index % 2 == 0)
```

[File: code/system-contracts/contracts/KnownCodesStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L78)
```solidity
78:         require(Utils.bytecodeLenInWords(_bytecodeHash) % 2 == 1, "Code length in words must be odd");
```

[File: code/system-contracts/contracts/libraries/Utils.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/Utils.sol#L88)
```solidity
88:         require(lengthInWords % 2 == 1, "pr"); // bytecode length in words must be odd
```

## [G-40] else-block is not required in `getOperationState()`

**File:** `Governance.sol`

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L105)
```solidity
105:     function getOperationState(bytes32 _id) public view returns (OperationState) {
106:         uint256 timestamp = timestamps[_id];
107:         if (timestamp == 0) {
108:             return OperationState.Unset;
109:         } else if (timestamp == EXECUTED_PROPOSAL_TIMESTAMP) {
110:             return OperationState.Done;
111:         } else if (timestamp > block.timestamp) {
112:             return OperationState.Waiting;
113:         } else {
114:             return OperationState.Ready;
115:         }
116:     }
```

The `else` instruction at line 113 can be removed. When previous conditions won't be fulfilled, function will still return `OperationState.Ready`. Getting rid of redundant `else` instruction saves additional gas.

## [G-41] Inline `modifier`s that are only used once, to save gas

**Files:** `ContractDeployer.sol`, `KnownCodesStorage.sol`

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L213)
```solidity
213:     function forceDeployOnAddress(ForceDeployment calldata _deployment, address _sender) external payable onlySelf {
```

[File: code/system-contracts/contracts/KnownCodesStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L39)
```solidity
39:     function markBytecodeAsPublished(bytes32 _bytecodeHash) external onlyCompressor {
```

Modifiers `onlySelf` and `onlyCompressor` where used only once, thus they can be inlined.

## [G-42] Use `""` instead of `new bytes(0)`

**Files:** `StateTransitionManager.sol`, `Mailbox.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L308)
```solidity
308:             signature: new bytes(0),
309:             factoryDeps: _hashFactoryDeps(_factoryDeps),
310:             paymasterInput: new bytes(0),
311:             reservedDynamic: new bytes(0)
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L196)
```solidity
196:             signature: new bytes(0),
197:             factoryDeps: uintEmptyArray,
198:             paymasterInput: new bytes(0),
199:             reservedDynamic: new bytes(0)
```

## [G-43] `public` functions which are not called by the contract should be declared as `external`

**File:** `Mailbox.sol`

When `public` function is never called internally and is only expected to be invoked externally, it is more gas-efficient to explicitly declare it as `external`.

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L74)
```solidity
74:     function proveL1ToL2TransactionStatus(
75:         bytes32 _l2TxHash,
76:         uint256 _l2BatchNumber,
77:         uint256 _l2MessageIndex,
78:         uint16 _l2TxNumberInBatch,
79:         bytes32[] calldata _merkleProof,
80:         TxStatus _status
81:     ) public view returns (bool) {
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L143)
```solidity
143:     function l2TransactionBaseCost(
144:         uint256 _gasPrice,
145:         uint256 _l2GasLimit,
146:         uint256 _l2GasPerPubdataByteLimit
147:     ) public view returns (uint256) {
```

## [G-44] Do not emit events with empty data

**File:** `Admin.sol`

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L139)
```solidity
139:         emit Freeze();
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L149)
```solidity
149:         emit Unfreeze();
```

## [G-45]  Do not declare local variables used only once

<details>

**Files:** `L2ContractHelper.sol`, `Compressor.sol`, `L2SharedBridge.sol`, `Mailbox.sol`, `L1ERC20Bridge.sol`, `NonceHolder.sol`, `DefaultAccount.sol`, `EfficientCall.sol`, `AccountCodeStorage.sol`, `L1SharedBridge.sol`, `Diamond.sol`, `L2StandardERC20.sol`, `SystemContractHelper.sol`, `KnownCodesStorage.sol`, `Admin.sol`, `ContractDeployer.sol`

[File: code/contracts/zksync/contracts/bridge/L2StandardERC20.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2StandardERC20.sol#L119)
```solidity
119:         address beaconAddress = _getBeacon();
120:         require(msg.sender == UpgradeableBeacon(beaconAddress).owner(), "tt");
```

Variable `beaconAddress` is used only once, thus this variable is redundant. Above code can be rewritten to:

```
require(msg.sender == UpgradeableBeacon(_getBeacon()).owner(), "tt");
```

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L64)
```solidity
64:             address l2StandardToken = address(new L2StandardERC20{salt: bytes32(0)}());
65:             l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(l2StandardToken);
```

Variable `l2StandardToken` is used only once, thus it is redundant. Above code can be changed to:

```
l2TokenBeacon = new UpgradeableBeacon{salt: bytes32(0)}(address(new L2StandardERC20{salt: bytes32(0)}()));
```

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L110)
```solidity
110:         bytes32 salt = _getCreate2Salt(_l1Token);
111: 
112:         BeaconProxy l2Token = _deployBeaconProxy(salt);
```

Variable `salt` is used only once, thus it is redundant. Above code can be changed to:

```
BeaconProxy l2Token = _deployBeaconProxy(_getCreate2Salt(_l1Token));
```

[File: code/contracts/zksync/contracts/bridge/L2SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/zksync/contracts/bridge/L2SharedBridge.sol#L150)
```solidity
150:         bytes32 constructorInputHash = keccak256(abi.encode(address(l2TokenBeacon), ""));
151:         bytes32 salt = _getCreate2Salt(_l1Token);
152:         return
153:             L2ContractHelper.computeCreate2Address(address(this), salt, l2TokenProxyBytecodeHash, constructorInputHash);
```

Variables `constructorInputHash` and `salt` are used only once, thus they are redundant. Above code can be changed to:

```
return
    L2ContractHelper.computeCreate2Address(address(this), _getCreate2Salt(_l1Token), l2TokenProxyBytecodeHash, keccak256(abi.encode(address(l2TokenBeacon), "")));
```

[File: code/system-contracts/contracts/libraries/EfficientCall.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/EfficientCall.sol#L261)
```solidity
261:         uint32 shrinkTo = uint32(msg.data.length - (_data.length + dataOffset));
262:         SystemContractHelper.ptrShrinkIntoActive(shrinkTo);
263: 
264:         uint32 gas = Utils.safeCastToU32(_gas);
265:         uint256 farCallAbi = SystemContractsCaller.getFarCallABIWithEmptyFatPointer(
266:             gas,
```

`shrinkTo` and `gas` are used only once, thus there's no need to declare them at all:

```
        SystemContractHelper.ptrShrinkIntoActive(uint32(msg.data.length - (_data.length + dataOffset)));

        uint256 farCallAbi = SystemContractsCaller.getFarCallABIWithEmptyFatPointer(
            Utils.safeCastToU32(_gas),
```

[File: code/system-contracts/contracts/libraries/SystemContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/libraries/SystemContractHelper.sol#L217)
```solidity
217:         uint256 shifted = (meta << (256 - size - offset));
218:         // Then we shift everything back
219:         result = (shifted >> (256 - size));
```

`shifted` is used only once, thus there's no need to declare this variable at all:

```
result = ((meta << (256 - size - offset)) >> (256 - size));
```

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L92)
```solidity
92:         uint256 addressAsKey = uint256(uint160(msg.sender));
93: 
94:         nonceValues[addressAsKey][_key] = _value;
```

`addressAsKey` is used only once, thus there's no need to declare this variable at all:

```
 nonceValues[uint256(uint160(msg.sender))][_key] = _value;
```

[File: code/system-contracts/contracts/NonceHolder.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/NonceHolder.sol#L103)
```solidity
103:         uint256 addressAsKey = uint256(uint160(msg.sender));
104:         return nonceValues[addressAsKey][_key];
```

`addressAsKey` is used only once, thus there's no need to declare this variable at all:

```
 return nonceValues[uint256(uint160(msg.sender))][_key];
```

[File: code/system-contracts/contracts/KnownCodesStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/KnownCodesStorage.sol#L75)
```solidity
75:         uint8 version = uint8(_bytecodeHash[0]);
76:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```

`version` is used only once, thus there's no need to declare this variable at all:

```
require(uint8(_bytecodeHash[0]) == 1 && _bytecodeHash[1] == bytes1(0), "Incorrectly formatted bytecodeHash");
```

[File: code/system-contracts/contracts/DefaultAccount.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/DefaultAccount.sol#L099)
```solidity
099:         uint256 totalRequiredBalance = _transaction.totalRequiredBalance();
100:         require(totalRequiredBalance <= address(this).balance, "Not enough balance for fee + value");
```

`totalRequiredBalance` is used only once, thus there's no need to declare this variable at all:

```
require(_transaction.totalRequiredBalance() <= address(this).balance, "Not enough balance for fee + value");
```

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L121)
```solidity
121:         bytes32 hash = keccak256(
122:             bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))
123:         );
124: 
125:         newAddress = address(uint160(uint256(hash)));
```

`hash` is used only once, thus there's no need to declare this variable at all:

```
newAddress = address(uint160(uint256(keccak256(bytes.concat(CREATE_PREFIX, bytes32(uint256(uint160(_sender))), bytes32(_senderNonce))))));
```

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L302)
```solidity
302:         uint256 knownCodeMarker = KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash);
303:         require(knownCodeMarker > 0, "The code hash is not known");
```

`knownCodeMarker` is used only once, thus there's no need to declare this variable at all:

```
require(KNOWN_CODE_STORAGE_CONTRACT.getMarker(_bytecodeHash) > 0, "The code hash is not known");
```

[File: code/system-contracts/contracts/Compressor.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/Compressor.sol#L65)
```solidity
65:                 uint64 encodedChunk = dictionary.readUint64(indexOfEncodedChunk);
66:                 uint64 realChunk = _bytecode.readUint64(encodedDataPointer * 4);
67: 
68:                 require(encodedChunk == realChunk, "Encoded chunk does not match the original bytecode");
```

`encodedChunk` and `realChunk` are used only once, thus there's no need to declare those variables at all:

```
require(dictionary.readUint64(indexOfEncodedChunk) == _bytecode.readUint64(encodedDataPointer * 4), "Encoded chunk does not match the original bytecode");
```

[File: code/system-contracts/contracts/AccountCodeStorage.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/AccountCodeStorage.sol#L60)
```solidity
60:         bytes32 constructedBytecodeHash = Utils.constructedBytecodeHash(codeHash);
61: 
62:         _storeCodeHash(_address, constructedBytecodeHash);
```

`constructedBytecodeHash` is used only once, thus there's no need to declare this variable at all:

```
_storeCodeHash(_address, Utils.constructedBytecodeHash(codeHash));
```

[File: code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/libraries/Diamond.sol#L192)
```solidity
192:         uint256 selectorsLength = ds.facetToSelectors[_facet].selectors.length;
193:         // If there are no selectors associated with facet then save facet as new one
194:         if (selectorsLength == 0) {
```

`selectorsLength` is used only once, thus there's no need to declare this variable at all:

```
if (ds.facetToSelectors[_facet].selectors.length == 0) {
```

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L40)
```solidity
40:         uint8 version = uint8(_bytecodeHash[0]);
41:         require(version == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```

`version` is used once, thus there's no need to declare this variable at all:

```
require(uint8(_bytecodeHash[0]) == 1 && _bytecodeHash[1] == bytes1(0), "zf"); // Incorrectly formatted bytecodeHash
```

[File: code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/common/libraries/L2ContractHelper.sol#L66)
```solidity
66:         bytes32 senderBytes = bytes32(uint256(uint160(_sender)));
67:         bytes32 data = keccak256(
68:             bytes.concat(CREATE2_PREFIX, senderBytes, _salt, _bytecodeHash, _constructorInputHash)
69:         );
70: 
71:         return address(uint160(uint256(data)));
```

`senderBytes` and `data` are used once, thus there's no need to declare those variables:

```
return address(uint160(uint256( keccak256(
            bytes.concat(CREATE2_PREFIX, bytes32(uint256(uint160(_sender))), _salt, _bytecodeHash, _constructorInputHash)
        ))));
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L104)
```solidity
104:         bytes32 cutHashInput = keccak256(abi.encode(_diamondCut));
105:         require(
106:             cutHashInput == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
107:             "StateTransition: cutHash mismatch"
108:         );
109: 
```

`cutHashInput` is used only once, thus there's no need to declare this variable at all:

```
        require(
            keccak256(abi.encode(_diamondCut)) == IStateTransitionManager(s.stateTransitionManager).upgradeCutHash(_oldProtocolVersion),
            "StateTransition: cutHash mismatch"
        );
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L41)
```solidity
41:         uint256 amount = address(this).balance;
42:         address sharedBridgeAddress = s.baseTokenBridge;
43:         IL1SharedBridge(sharedBridgeAddress).receiveEth{value: amount}(ERA_CHAIN_ID);
```

`amount` and `sharedBridgeAddress` are used only once, thus there's no need to declare those variables at all:

```
IL1SharedBridge(s.baseTokenBridge).receiveEth{value: address(this).balance}(ERA_CHAIN_ID);
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L123)
```solidity
123:         bytes32 calculatedRootHash = Merkle.calculateRoot(_proof, _index, hashedLog);
124:         bytes32 actualRootHash = s.l2LogsRootHashes[_batchNumber];
125: 
126:         return actualRootHash == calculatedRootHash;
```

`calculatedRootHash` and `actualRootHash` are used only once, thus there's no need to declare those variables at all:

```
return Merkle.calculateRoot(_proof, _index, hashedLog) == s.l2LogsRootHashes[_batchNumber];
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L148)
```solidity
148:         uint256 l2GasPrice = _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit);
149:         return l2GasPrice * _l2GasLimit;
```

`l2GasPrice` is used only once, thus there's no need to declare this variable at all:

```
return _deriveL2GasPrice(_gasPrice, _l2GasPerPubdataByteLimit) * _l2GasLimit;;
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Mailbox.sol#L271)
```solidity
271:         uint256 baseCost = _params.l2GasPrice * _params.l2GasLimit;
272:         require(_mintValue >= baseCost + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost
```

`baseCost` is used only once, thus there's no need to declare this variable at all:

```
require(_mintValue >= _params.l2GasPrice * _params.l2GasLimit + _params.l2Value, "mv"); // The `msg.value` doesn't cover the transaction cost
```

[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L160)
```solidity
160:             uint256 amount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _amount); // note if _prevMsgSender is this contract, this will return 0. This does not happen.
161:             require(amount == _amount, "3T"); // The token has non-standard transfer logic
```

`amount` is used only once, thus there's no need to declare this variable at all:

```
require(_depositFunds(_prevMsgSender, IERC20(_l1Token), _amount) == _amount, "3T"); // The token has non-standard transfer logic
```

[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L205)
```solidity
205:             uint256 withdrawAmount = _depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount);
206:             require(withdrawAmount == _depositAmount, "5T"); // The token has non-standard transfer logic
```

`withdrawAmount` is used only once, thus there's no need to declare this variable at all:

```
 require(_depositFunds(_prevMsgSender, IERC20(_l1Token), _depositAmount) == _depositAmount, "5T"); // The token has non-standard transfer logic
```

[File: code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1SharedBridge.sol#L340)
```solidity
340:                 bytes32 dataHash = depositHappened[_chainId][_l2TxHash];
341:                 bytes32 txDataHash = keccak256(abi.encode(_depositSender, _l1Token, _amount));
342:                 require(dataHash == txDataHash, "ShB: d.it not hap");
```

`dataHash` and `txDataHash` are used only once, thus there's no need to declare those variables at all:

```
require(depositHappened[_chainId][_l2TxHash] == keccak256(abi.encode(_depositSender, _l1Token, _amount)), "ShB: d.it not hap");
```

[File: code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridge/L1ERC20Bridge.sol#L76)
```solidity
76:         bytes32 constructorInputHash = keccak256(abi.encode(l2TokenBeacon, ""));
77:         bytes32 salt = bytes32(uint256(uint160(_l1Token)));
78: 
79:         return L2ContractHelper.computeCreate2Address(l2Bridge, salt, l2TokenProxyBytecodeHash, constructorInputHash);
```

`constructorInputHash` and `salt` are used only once, thus there's no need to declare those variables at all:

```
return L2ContractHelper.computeCreate2Address(l2Bridge,  bytes32(uint256(uint160(_l1Token))), l2TokenProxyBytecodeHash, keccak256(abi.encode(l2TokenBeacon, "")));
```

</details>

## [G-46] Use `msg.value` directly, instead of assigning it to variable

**File:** `ContractDeployer.sol`

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L329)
```solidity
329:         uint256 value = msg.value;
```

## [G-47] Storage values shouldn't be updated when value is not being changed

<details>

**Files:** `SystemContext.sol`, `Bridgehub.sol`, `ValidatorTimelock.sol`, `Governance.sol`, `StateTransitionManager.sol`, `Admin.sol`, `ContractDeployer.sol`

It's recommended to add additional `require` statement, which will verify if the value is really changed, before we will store it in the storage variables
E.g., let's consider a function `setChainId()` from `SystemContext.sol`. When `chainId` is `1` and we will call `setChainId(1)`, function will re-store the same value (Gsreset (900 gas)).

[File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L51)
```solidity
51:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
```

[File: code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L108)
```solidity
108:     function setSharedBridge(address _sharedBridge) external onlyOwner {
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L132)
```solidity
132:     function setValidatorTimelock(address _validatorTimelock) external onlyOwnerOrAdmin {
[...]
137:     function setInitialCutHash(Diamond.DiamondCutData calldata _diamondCut) external onlyOwner {
[...]
142:     function setNewVersionUpgrade(
[...]
152:     function setUpgradeDiamondCut(
```

[File: code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/StateTransitionManager.sol#L110)
```solidity
110:     function setPendingAdmin(address _newPendingAdmin) external onlyOwnerOrAdmin {
```

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L73)
```solidity
73:     function setStateTransitionManager(IStateTransitionManager _stateTransitionManager) external onlyOwner {
```

[File: code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/ValidatorTimelock.sol#L96)
```solidity
96:     function setExecutionDelay(uint32 _executionDelay) external onlyOwner { 
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L79)
```solidity
79:     function setTokenMultiplier(uint128 _nominator, uint128 _denominator) external onlyAdminOrStateTransitionManager {
[...]
89:     function setValidiumMode(PubdataPricingMode _validiumMode) external onlyAdmin {
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L45)
```solidity
45:     function setValidator(address _validator, bool _active) external onlyStateTransitionManager {
[...]
51:     function setPorterAvailability(bool _zkPorterIsAvailable) external onlyStateTransitionManager {
[...]
58:     function setPriorityTxMaxGasLimit(uint256 _newPriorityTxMaxGasLimit) external onlyStateTransitionManager { 
```

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L84)
```solidity
84:     function setChainId(uint256 _newChainId) external onlyCallFromForceDeployer {
```

[File: code/system-contracts/contracts/SystemContext.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/SystemContext.sol#L099)
```solidity
099:     function setTxOrigin(address _newOrigin) external onlyCallFromBootloader {
[...]
105:     function setGasPrice(uint256 _gasPrice) external onlyCallFromBootloader {
[...]
112:     function setPubdataInfo(uint256 _gasPerPubdataByte, uint256 _basePubdataSpent) external onlyCallFromBootloader {
```

[File: code/contracts/ethereum/contracts/governance/Governance.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/governance/Governance.sol#L249)
```solidity
249:     function updateDelay(uint256 _newDelay) external onlySelf {
[...]
256:     function updateSecurityCouncil(address _newSecurityCouncil) external onlySelf {
```

[File: code/system-contracts/contracts/ContractDeployer.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/system-contracts/contracts/ContractDeployer.sol#L65)
```solidity
65:     function updateAccountVersion(AccountAbstractionVersion _version) external onlySystemCall {
```

[File: code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol](https://github.com/code-423n4/2024-03-zksync/blob/main/code/contracts/ethereum/contracts/state-transition/chain-deps/facets/Admin.sol#L67)
```solidity
67:     function changeFeeParams(FeeParams calldata _newFeeParams) external onlyAdminOrStateTransitionManager {
```

</details>

# Automated-Findings

<details>

## [AUTOMATED-FINDING-1] Using `bool`s for storage incurs overhead

Booleans are more expensive than uint256 or any type that takes up a full word because each write operation emits an extra SLOAD to first read the slot's contents, replace the bits taken up by the boolean, and then write back. This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled.

Above code detects every instance of  mappings which utilizes boolean instead of uint
```
% grep "=>" -ri . | grep mapping | grep bool | wc -l                    
       9
```

## [AUTOMATED-FINDING-2] Mark constructor as payable

Payable functions cost less gas to execute, since the compiler does not have to add extra checks to ensure that a payment wasn't provided. A constructor can safely be marked as payable, since only the deployer would be able to pass funds, and the project itself would not pass any funds.

```
% grep "constructor(" -ri . |  grep -v "//" | grep "{" | grep -v "payable" | grep -v "/test"  | wc -l
      16
```

## [AUTOMATED-FINDING-3] Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier such as onlyOwner is used, the function will revert if a normal user tries to pay the function. Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. 

```
% grep "function" -ri . |  grep -v "//" | grep "{" | grep "only" | grep -v "payable" | grep -v "/test" | grep only | wc -l
      64
```

## [AUTOMATED-FINDING-4] Index all 3 parameters in events

```
% grep "event " -ri . |  grep -v "//" | grep -v "/test" | grep ";" | grep -v indexed | grep -v "()" | wc -l
      19
```

Above detector identifies events which are not properly indexed.

## [AUTOMATED-FINDING-5] Nesting if-statements is cheaper than using &&

Nesting if-statements avoids the stack operations of setting up and using an extra jumpdest, and saves 6 gas. This basically means that: `if (A && B)` can be represented as `if (A) { if (B) }`.

```
% grep "if (" -r . | grep "&&" | grep -v "/test" | grep ".sol" | wc -l
       9
```

## [AUTOMATED-FINDING-6] Assembly: Use scratch space for calculating small keccak256 hashes

If the arguments to the encode call can fit into the scratch space (two words or fewer), then it's more efficient to use assembly to generate the hash (80 gas)

Below code detects only the instances where there's a single argument in `keccak256`.
```
% grep "keccak256(" -r . | grep ")" | grep -v "/test" | grep ".sol" | grep -v ":=" | grep -v "," | grep -v "//" | grep -v "constant" | wc -l
      17
```

## [AUTOMATED-FINDING-7] Assembly: Use scratch space when building emitted events with two data arguments

To efficiently emit events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.

Below code detects only the instances where there's a single (or no) argument in the event.

```
% grep "emit " -r . | grep ")" | grep -v "/test" | grep ".sol" | grep -v "," | grep -v "//" | wc -l
      12
```

## [AUTOMATED-FINDING-8] `abi.encode()` is less efficient than `abi.encodePacked()`

```
% grep "abi.encode" -r . | grep -v "//" | grep -v "/test" | wc -l
      63
```

## [AUTOMATED-FINDING-9] `""` has the same value as `new bytes(0)` but costs less gas

```
% grep "new bytes(0)" -ri . | wc -l
      17
```

## [AUTOMATED-FINDING-10] Function names can be optimized to save gas

Function that are public/external and public state variable names can be optimized to save gas.

Method IDs that have two leading zero bytes can save 128 gas each during deployment, and renaming functions to have lower method IDs will save 22 gas per call, per sorted position shifted.

You can use the [Function Name Optimizer Tool](https://emn178.github.io/solidity-optimize-name/) to find new function names.

## [AUTOMATED-FINDING-11] Integer increments by one can be unchecked

```
% grep  "+= 1;" -r . | wc -l
       9
```

## [AUTOMATED-FINDING-12] Low-level call can be optimized with assembly

returnData is copied to memory even if the variable is not utilized: the proper way to handle this is through a low level assembly call and save 159 gas.

```
% grep "call{" -ri . | wc -l
      11
```

## [AUTOMATED-FINDING-13] Operator >=/<= costs less gas than operator >/<

The compiler uses opcodes GT and ISZERO for solidity code that uses >, but only requires LT for >=, which saves 3 gas. If < is being used, the condition can be inverted.

```
% grep -E "if \(|require\(" -r . | grep ">" | grep -v ">=" | grep ".sol" | wc -l
      42
```

```
% grep -E "if \(|require\(" -r . | grep "<" | grep -v "<=" | grep ".sol" | wc -l
      15
```

## [AUTOMATED-FINDING-14] Reduce deployment gas costs by fine-tuning IPFS file hashes

Solc currently by default appends the IPFS hash (in CID v0) of the canonical metadata file and the compiler version to the end of the bytecode. This value is variable-length CBOR-encoded i.e. it can be optimized in order to reduce deployment gas costs.

## [AUTOMATED-FINDING-15] Simple checks for zero can be done using assembly to save gas

Using assembly for simple zero checks on unsigned integers can save gas due to lower-level, optimized operations.

Below code returns only the simple `if` conditions without additional `&&` and `||` operators, such as: `if (A == 0)`

```
% grep "if (" -r . | grep -v "//" | grep -v "&&" | grep -v "||"  | grep " == 0)" | grep .sol | wc -l
      14
```

## [AUTOMATED-FINDING-16] Use assembly to validate msg.sender

We can use assembly to efficiently validate msg.sender with the least amount of opcodes necessary.

Below code returns only the simple `if` conditions without additional `&&` and `||` operators, such as: `if (msg.sender == 0)`

```
% grep -E "require|if \(" -r . | grep -v "//" | grep -v "&&" | grep -v "||"  | grep ")" | grep .sol | grep "msg.sender" | wc -l
      29
```

## [AUTOMATED-FINDING-17] Use assembly in place of abi.decode to save gas

Instead of using abi.decode, we can use assembly to decode our desired calldata values directly. This will allow us to avoid decoding calldata values that we will not use.

```
% grep "abi.decode" -r . | grep -v "//" | wc -l
      13
```

## [AUTOMATED-FINDING-18] Counting down in `for`-loop is more gas efficient

Counting down is more gas efficient than counting up because neither we are making zero variable to non-zero variable and also we will get gas refund in the last transaction when making non-zero to zero variable

```
% grep "for (" -r . | grep " = 0" | grep "++" | grep -v "/test" | grep ".sol" | wc -l
      18
```

## [AUTOMATED-FINDING-19] `do`-`while` is cheaper than `for`-loops when the initial check can be skipped

Using do-while loops instead of for loops can be more gas-efficient. Even if you add an if condition to account for the case where the loop doesn't execute at all, a do-while loop can still be cheaper in terms of gas.

```
% grep "for (" -r . | grep " = 0" | grep "++" | grep -v "/test" | grep ".sol" | wc -l
      18
```

## [AUTOMATED-FINDING-20]  Use direct `unchecked` block, instead of importing it from the library
Library `UncheckedMath.sol` implements a simple `uncheckedInc()` function which is responsible for performing unchecked incrementation. This function is used in multiple of loops in the code-base.
However, it's cheaper to use `unchecked` block directly, like that:

```
for (uint256 i = 0; i < length;) {
      ...
      unchecked {
            ++i;
      }
}
```

instead using imported function:

```
for (uint256 i = 0; i < length; i = i.uncheckedInc()) {
      ...
}
```

Below code detects the instances where `i.uncheckedInc()` is used inside the loops:

```
% grep "uncheckedInc()" -r . | grep "for (" | wc
      12     154    1772
```

</details>

**[saxenism (zkSync) confirmed and commented](https://github.com/code-423n4/2024-03-zksync-findings/issues/55#issuecomment-2062871292):**
 > Best Report. The effort put in by the warden is apparent. The team will surely be picking up a few pointers from the suggestions listed here.

***

# Disclosures

C4 is an open organization governed by participants in the community.

C4 audits incentivize the discovery of exploits, vulnerabilities, and bugs in smart contracts. Security researchers are rewarded at an increasing rate for finding higher-risk issues. Audit submissions are judged by a knowledgeable security researcher and solidity developer and disclosed to sponsoring developers. C4 does not conduct formal verification regarding the provided code but instead provides final verification.

C4 does not provide any guarantee or warranty regarding the security of this project. All smart contract software should be used at the sole risk and responsibility of users.
