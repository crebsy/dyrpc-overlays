# dyRPC overlays

## TL;DR
Overlays allow you to add your custom logic to already deployed contracts to simulate new events and new read-only functions on top of them.
With overlays you can create new view functions, modify existing ones, change field visibility, emit new events and query the historical data of any contract with your modified source code. 
The best thing is, your new code is applied instantly for any requested block so you don't need to wait for any data back-filling :sparkles:

## Usecases
### Add `Transfer` events to WETH contract's `deposit()` and `withdraw()`:
The [WETH Contract](https://etherscan.io/address/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2) does not emit the `Transfer` event on `deposit()` and `withdraw()` because it's optional on the ERC-20 spec and was probably not added to save gas.
Apps relying on this event for ERC-20 tokens, handle the missing `Transfer` manually for WETH.

With [dyRPC](https://beta.dyrpc.network)-overlays, anyone can add a modified version of the WETH contract and deploy it under the same address. The new contract can be used instantly as a drop-in replacement of the original contract. Historical and future events can be queried with `eth_getLogs`.  The overlay will preserve all contract state adding the new events and new view functions on top of the deployed on-chain code.

Here's an overlay RPC URL created with [this example patch](https://github.com/crebsy/dyrpc-overlays/commit/7f8fd586f7c7ebe037ee791dd271cc196b6753bd) that you can use directy in your web3 client app for doing ad-hoc range queries on the WETH contract.

`export WEB3_PROVIDER="https://weth-overlay.dyrpc.network"`

## API docs
https://hackmd.io/@crebsy/H1jO9onua

