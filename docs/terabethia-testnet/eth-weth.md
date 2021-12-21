---
date: "1"
---
# Terabethia - Testnet ETH <> WETH Example

## Terabethia - Testnet ETH <> WETH Example

As an example use-case and example implementation of Terabethia, we created Wrapped Ethereum on the IC (using Goerli Ether, of course, so purely a test and no real monetary value). It showcases:

- How contracts can use Terabethia to communicate across the IC<>ETH
- The potential for mirroring assets from Ethereum onto the Internet Computer

It is a three-contract implementation. A proxy contract on Ethereum receives Goerli Ether deposits from a user, locks them, and sends a mint message to the Internet Computer by calling the Terabethia bridge contract.

That message is sent to a WETH proxy canister on the IC that consumes the message and tells the WETH token canister to mint an equivalent amount of Wrapped Ethereum on that network.

Here's the repository of both IC-side contracts (proxy, and token):

- [WETH Proxy (IC)](https://github.com/Psychedelic/terabethia/blob/master/ic/w_eth/src/eth_proxy/src/lib.rs)
- [WETH Proxy (ETH)](https://github.com/Psychedelic/terabethia/blob/master/eth/contracts/EthProxy.sol)
- [WETH Token Contract (IC)](https://github.com/Psychedelic/terabethia/blob/master/ic/w_eth/src/token/token.did)


## Quick Flow Guide 🧰

Let's go through the flow of using the  proxy on Ethereum to mint WETH on the Internet Computer!

> Remember, this it **not real ETH**. It is testnet, Goerli ETH.

--- 

### Deposit ETH in the Ethereum WETH Proxy Contract

First, you need to deposit ETH to the WETH Proxy contract **on Ethereum**. The contract will lock your ETH, and call the WETH proxy contract on the IC through Terabethia to tell the WETH token contract to mint an equivalent balance.

Do so by calling the following method, passing the destination Principal ID (address on the IC that will own the WETH balance).

- ETH Proxy Contract address: `ad212312312312`

> Make sure you have Goerli ETH, get it from a faucet like https://faucet.goerli.mudit.blog/

```
code example of minting&depositing in proxy on eth?
```

### Check your WETH Balance on the Internet Computer

Now that you have minted WETH through the proxy contract on Ethereum, **let's check that you've received an equivalent minted balanced on the IC**!

- WETH Token Contract Canister ID: `tq6li-4qaaa-aaaab-qad3q-cai`

You can check by calling the balanceOf method:

```
code example of balance method
```

Awesome! You have Goerli WETH on the Internet Computer, and can trade and use it on the IC's low-fee and fast transaction ecosystem.

### Burn Your WETH and Get ETH Back on Ethereum



But, what if you want to get your WETH turned back into ETH on Ethereum?

Simple, you need to call WETH's burn function through the proxy, and set a destination address on Ethereum that will receive the unlocked funds on the Ethereum-side proxy contract.

```
code example of doing that
```

### Claiming Your ETH

Last but not least, you need to claim your ETH on the Ethereum Proxy contract.

```
code example of doing that
```