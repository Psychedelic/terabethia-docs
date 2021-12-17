---
date: "1"
---
# Terabethia - Testnet

## How it works

Terabethia is based on L1 <> L2 messaging protocol from [Starknet](https://www.cairo-lang.org/docs/hello_starknet/l1l2.html). We support same way of sending/consuming messages between Ethereum and IC.

- you need to have a pair of contracts (Ethereum and IC) which will send/consume messages
- consuming message received from Ethereum is triggered automatically on IC
- consuming message received from IC requires user interaction; we only store proof from L2 -> L1, therefore user needs to initiate the call trying to consume the message

## Is it decentralised?
Not yet. There's a plan for fully non-custodial setup which depends on [ECDSA Threshold signatures](https://forum.dfinity.org/t/threshold-ecdsa-signatures/6152).

## Deployments

Terabethia is currently deployed on Goerli Etherem network at address [0x7de702c6503bc03b5ebe00221f50af9330ca4c16](https://goerli.etherscan.io/address/0x7de702c6503bc03b5ebe00221f50af9330ca4c16#code). IC canister is deployed at "s5qpg-tyaaa-aaaab-qad4a-cai". 

## Simple ETH -> WETH Bridge Example

We created a simple bridge for ETH/wETH. 

- [ETH Bridge (Solidity)](https://github.com/Psychedelic/terabethia/blob/master/eth/contracts/EthProxy.sol)
- [DIP20 with Proxy that mints/burns wETH](https://github.com/Psychedelic/terabethia/tree/master/ic/w_eth)