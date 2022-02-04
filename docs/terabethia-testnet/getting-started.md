---
date: "1"
---
# Terabethia - Testnet V2

## How it works

Terabethia is based on L1 <> L2 messaging protocol from [Starknet](https://www.cairo-lang.org/docs/hello_starknet/l1l2.html). We support same way of sending/consuming messages between Ethereum and IC. This V2 of the testnet extends Terabethia's security guarantees and utilizes Starknet to relay messages from the Internet Computer to Ethereum (from Ethereum to the Internet Computer that is not used or needed).

To use Terabethia:

- You need to have a pair of contracts (Ethereum and IC) which will send/consume messages
- Consuming message received from Ethereum is triggered automatically on IC
- Consuming message received from IC requires user interaction; we only store proof from L2 -> L1, therefore user needs to initiate the call trying to consume the message

## Is it decentralised?
Not yet. There's a plan for fully non-custodial setup which depends on [ECDSA Threshold signatures](https://forum.dfinity.org/t/threshold-ecdsa-signatures/6152).

---

## The Testnet V2 Bridge - Contracts

Terabethia is currently deployed on Goerli Etherem network at address:

- [0x2E130E57021Bb4dfb95Eb4Dd0dD8CFCeB936148a](https://goerli.etherscan.io/address/0x2E130E57021Bb4dfb95Eb4Dd0dD8CFCeB936148a#code)

The IC canister is deployed on the IC's mainnet, and its canister ID is:

- [timop-6qaaa-aaaab-qaeea-cai](https://ic.rocks/principal/timop-6qaaa-aaaab-qaeea-cai)

---

## Getting Started - Available Methods

In terms of integrating and using Terabethia, the scope is simple. You have two main methods on each side of the bridge (Ethereum, and the Internet Computer) that contracts on each chain can call.

### On Ethereum
There are two methods available. First, **sendMessage** used to send a message/payload through the bridge to a destination canister on the Internet Computer. Here the address is a **Principal ID** in hex format.

```solidity
Terabethia.sendMessage(uint256 canisterId, uint256[] payload) {}
```

Secondly, **consumeMessage** used by Ethereum contracts to manually initiate the call needed to consume a message received from the Internet Computer.

```solidity
Terabethia.consumeMessage(uint256 from_address, uint256[] calldata payload) {}
```

### On the Internet Computer
On the IC, the methods are the same. First, **sendMessage** used to send a message/payload through the bridge to a destination canister on the Internet Computer. Here the destination (to) is an Ethereum contract address as a Principal.

```rust
TerabethiaCanister.send_message(to: Principal, payload: Vec<Nat>)
```

Secondly, **consumeMessage** used by Ethereum contracts to manually initiate the call needed to consume a message received from the Internet Computer. Here, the from is an Ethereum contract address in hex string format.

```rust
TerabethiaCanister.consume_message(from: Principal, payload: Vec<Nat>)
```

### Example Implementations

You can view two quick contract example implementations on each corresponding chain on:

- [WETH Proxy (IC)](https://github.com/Psychedelic/terabethia/blob/master/ic/w_eth/src/eth_proxy/src/lib.rs)
- [WETH Proxy (ETH)](https://github.com/Psychedelic/terabethia/blob/master/eth/contracts/EthProxy.sol)
- [WETH Token Contract (IC)](https://github.com/Psychedelic/terabethia/blob/master/ic/w_eth/src/token/token.did)