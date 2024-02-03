# dyRPC overlays

## TL;DR
Overlays allow you to add your custom logic to already deployed contracts to simulate new events and new read-only functions on top of them.
With overlays you can create new view functions, modify existing ones, change field visibility, emit new events and query the historical data of any contract with your modified source code. 
The best thing is, your new code is applied instantly for any requested block so you don't need to wait for any data back-filling :sparkles:

## Usecases
### Add `Transfer` events to WETH contract's `deposit()` and `withdraw()`:
The [WETH Contract](https://etherscan.io/address/0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2) does not emit the `Transfer` event on `deposit()` and `withdraw()` because it's optional on the ERC-20 spec and was probably not added to save gas.
With overlays, it's easy to patch the WETH contract and deploy the patched source code.
The modified version will be used instantly for any `eth_getLogs` calls.

Here's an overlay RPC URL created with [this patch](https://github.com/crebsy/dyrpc-overlays/commit/7f8fd586f7c7ebe037ee791dd271cc196b6753bd) that you can use directy in your web3 client app for doing ad-hoc range queries on the WETH contract:

[https://weth-overlay.dyrpc.network](https://weth-overlay.dyrpc.network)

## More info
https://hackmd.io/@crebsy/H1jO9onua

