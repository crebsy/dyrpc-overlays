# dyRPC overlays

## TL;DR
Overlays allow you to add your custom logic to already deployed contracts to simulate new events and new read-only functions on top of them.
With overlays you can create new view functions, modify existing ones, change field visibility, emit new events and query the historical data of any contract with your modified source code. 
The best thing is, your new code is applied instantly for any requested block so you don't need to wait for any data back-filling :sparkles:

## Usecases
### Add `Transfer` events to WETH contract's `deposit()` and `withdraw()`:
The [WETH Contract](https://etherscan.io/address/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2) does not emit the `Transfer` event on `deposit()` and `withdraw()` because it's optional on the ERC-20 spec and was probably not added to save gas.
This causes a few dapps and tools to have custom logic to handle the missing `Transfer` events for updating token balances.

With [dyRPC](https://beta.dyrpc.network)-overlays, anyone can add a modified version of the WETH contract and deploy it to the infra. The new contract will be available at the same contract address and can be used instantly for any `eth_getLogs` calls for historical and future blocks. The overlay will preserve all contract state adding the new events and new view functions on top of the deployed on-chain code.

Here's an overlay RPC URL created with [this example patch](https://github.com/crebsy/dyrpc-overlays/commit/7f8fd586f7c7ebe037ee791dd271cc196b6753bd) that you can use directy in your web3 client app for doing ad-hoc range queries on the WETH contract.

[https://weth-overlay.dyrpc.network](https://weth-overlay.dyrpc.network)

## Read more
https://hackmd.io/@crebsy/H1jO9onua

