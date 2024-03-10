# CrossSync Protocol
Cross Chain Messaging Aggregator Protocol

![Architecture](./crossSync.png)


### Detailed Bigger Demo Link :
https://www.loom.com/share/dfed8249187e4150b8041c296999b19f?sid=6e5694c0-c344-4a65-be90-dba9d61d5151



## About
CrossSync Protocol is a cross-chain messaging aggregator protocol. You may have used Hyperlane, Connext, Wormhole, Axelar, Chainlink CCIP, etc, but these protocols come with various challenges for developers and users. Firstly, they support different types of chains, one is available on some chains and another on some other chains. They also have syntax differences. To integrate one, two, or even three of them, developers need to implement numerous interfaces and understand the workings of the underlying protocol, relayer fees, etc.

To address these challenges and provide a common Interface and Gateway for interacting with multiple messaging interoperability protocols CrossSync has been made, With this users only need to implement and interact with CrossSync Protocol Gateway. They have to call the sendMessage function of the CrossSync Gateway and specify the route ID for sending messages, for example, 1 for Using Axelar, 2 for CCIP, 3 for Connext, 4 for Hyperlane, and 5 for Wormhole, 6 for Teleporter. CrossSync Protocol handles the rest and converts all the payload into the payload required for the messenger protocol, you don't have to bother about different kinds of domain IDs, chain names, etc. Additionally, users no longer have to implement individual interfaces to receive messages on the destination chain. A single receiveMessage function is all they need to integrate for receiving the payload.

### Benefits 
- A common relayer fee makes it easy for developers to integrate any of these protocols with ease and less hassle.
- Many of these protocols are available on different kinds of chains, ones you combine all of them into same protocol, you can have cross chain messaging available on almost all chains now
- With Auto Routing users get the lowest fees for cross chain call if many protocols are available on same chain.
- The design of this protocol has be kept modular, any protocol can be integrated easily by just deploying implementation contract for it.
- This protocol benefits users as well as developers from the percepective of UI, Fees, ease of using, ease of integrating, etc.

Its deployed on multiple chains but you can currently test on Polygon, avalanche and Dispatch Subnet!
All contract addresses and abi and details are present in the GitHub repo.

## Testing 
### ROUTE IDs:
- 0: NATIVE(Not Supported Yet)
- 1: AXELAR
- 2: CCIP
- 3: CONNEXT
- 4: HYPERLANE
- 5: WORMHOLE
- 6: TelePorter


## CrossSync Gateway Interfaces

### For Sending Message/Call Contract on Destination Chain
```
interface ICrossSyncGateway {

    struct MessagingPayload{
        address to;
        bytes data;
    }

    function sendMessage(
        uint256 _destinationChainId,
        uint256 _routeId,
        MessagingPayload calldata _payload,
        bytes calldata _routeData
    ) external payable;
}
```

### For Receiving Message on Destination Chain
```
interface ICrossSyncReceiverImplementer {

    function receiveMessage(
        uint256 _sourceChainId,
        address _sourceAddress,
        bytes calldata _payload
    ) external payable ;          
}
```



## Gateway and Implementation  Contracts
https://github.com/mbcse/CrossSync_Protocol_EthOxFord/blob/main/contractAddresses.json


## Transaction hashes, testing contracts and proofs of working
All these destination contract calls were done through crossSync Gateway.

Axelar Scan : https://testnet.axelarscan.io/gmp/0xa8667e0525fcbbad0ed99ccd4fffbdea9ec1ea042c89b558e08c7562ad9eb008

Polygon : https://mumbai.polygonscan.com/tx/0xa8667e0525fcbbad0ed99ccd4fffbdea9ec1ea042c89b558e08c7562ad9eb008

Avalanche: https://testnet.snowtrace.io/tx/0xd958bfa2f126f0542fb8180623992d0ca48e246ff42d9eeb1d6e09da4d031dac/eventlog?chainId=43113

Dispatch subnet : https://subnets-test.avax.network/dispatch/tx/0x2773889fad9d35ea5c1c01e5fece5c67665556e5ddf2b5b826d3140e5add80da?tab=logs

## Future Plans
- Implement Advance Auto Routing
- Implement Token and Other sends
- Implement Common Relayer Fee
- Implement Pay in any token Functionality
- Launch for public use
