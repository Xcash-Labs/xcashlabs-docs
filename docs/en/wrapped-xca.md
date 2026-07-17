# Wrapped XCash-Klassic (wXCK)

## Introduction

Wrapped XCash Klassic (**wXCK**) is an ERC-20 representation of native **XCash Klassic (XCK)** that enables XCK to be used on supported EVM-compatible blockchains. Currently, the XCash Bridge supports the **Polygon** and **Base** networks.

Every **1 wXCK** is backed by **1 XCK** securely held by the XCash Labs Bridge, maintaining a 1:1 backing between wrapped and native assets. This allows XCK holders to interact with decentralized applications (dApps), decentralized exchanges (DEXs), wallets, and other EVM-compatible services while preserving the value of their native XCK.

This guide explains what wXCK is, how the XCash Bridge operates, and how to safely transfer assets between native XCK and supported EVM networks. It also describes the bridge process, associated fees, security considerations, and best practices for using the bridge.

The XCash Bridge and your complete bridge request history are available directly from the **XCash Klassic Lite Wallet**:

**https://wallet.xcashlabs.org/**

To use the bridge, you will need:

- The **XCash Klassic Lite Wallet** for managing your native XCK.
- A compatible EVM wallet, such as **MetaMask** (currently the only wallet officially tested and supported by XCash Labs).
- A small amount of the destination network's native token (for example, **POL** on Polygon or **ETH** on Base) to pay blockchain network fees.

Always verify that you are using the official XCash Labs website before connecting your wallet or initiating a bridge transaction.

---

## How the Bridge Works

The XCash Bridge allows you to move funds securely between the native XCash-Klassic blockchain and supported EVM networks. 

The bridge supports movement in both directions:

- **XCK → wXCK**
- **wXCK → XCK**

Every bridge request is verified before assets are minted or released. The bridge verifies deposits, burn transactions, network confirmations, and available reserves before completing a transfer.

As an additional safety measure, the bridge continuously verifies that sufficient native XCK reserves are available to back all issued wXCK. If the bridge ever detects insufficient reserves, bridge operations are automatically suspended until the issue has been investigated and resolved. This is a protective safeguard and is not expected to occur during normal operation.

---


## Bridge Fees

Using the bridge involves one or more network transaction fees.

### XCK → wXCK

When converting native XCK into wXCK, you are responsible for:

- The native XCK transaction fee when sending XCK to the bridge.
- The EVM network gas fee required to claim your wXCK (for example, Polygon POL or Base ETH).

### wXCK → XCK

When converting wXCK back into native XCK, you are responsible for:

- Any required ERC-20 approval transaction (if applicable).
- The EVM gas fee required to burn your wXCK.
- An estimated XCK network fee. The bridge calculates this fee using the current XCK fee-per-byte rate and an estimated transaction size to ensure sufficient funds are available to complete the withdrawal. Any difference between the estimated fee and the actual XCK network fee is retained by the bridge to support ongoing bridge operation and maintenance.

---

## Converting XCK → wXCK

![XCK to wXCK](../../images/xck-to-wxck.png)

To convert native **XCK** into **wXCK**:

1. Open the **XCash Klassic Lite Wallet** and unlock the wallet you want to use.
2. Click the **Bridge** button to open the XCash Bridge.
3. Select the destination network  (**Polygon** or **Base**).
4. Open **MetaMask** and ensure the connected dApp and selected network match the destination network you want to bridge to.
5. Click the arrow to determine the direction for your transfer. For this transfer whe want the arrow to be in this direction: →
6. Enter the amount of XCK you want to bridge.
7. Click **Start Bridge**.
8. Review and confirm the XCK transaction, then click **Done**.
9. Wait for **10 XCash blockchain confirmations** (approximately **10 to 11 minutes**) while the bridge verifies your deposit. You can click **Refresh** at any time to check the current bridge status.
10. Once your deposit has been verified, the **Claim wXCK** button will appear.
11. Click **Claim wXCK** and approve the transaction in your connected MetaMask wallet.

After the claim transaction is confirmed on the destination network, your **wXCK** will appear in your MetaMask wallet. If this is your first time using wXCK, you may be prompted to add the token to MetaMask.





Note: You can exit out of the bridge screen once you have clicked the "Start Bridge" button.   When you go back in any active 
bridge request will be pulled up automatically.  

---

## Converting wXCK back into XCK

To return to the native blockchain:

1. Open the XCash Bridge.
2. Select **wXCK → XCK**.
3. Select the network that currently holds your wXCK.
4. Connect your wallet.
5. Enter your native XCK address.
6. Enter the amount to bridge.
7. Approve the transaction if necessary.
8. Burn your wXCK.
9. Wait for the bridge to verify the burn.
10. The bridge sends native XCK to the destination address.

---

## Bridge History

To return to the native blockchain:

---

## Supported Networks

The bridge currently supports:

- Polygon
- Base

Additional EVM networks may be added in the future.

---

## Bridge Safety

To protect your funds:

- Always use the official bridge website.
- Verify that your wallet is connected to the correct network.
- Double-check your XCK address before submitting a transaction.
- Never send XCK directly to a smart contract.
- Never share your wallet seed phrase or private keys.
- Wait for the bridge to finish processing before attempting another transfer.

---

# Frequently Asked Questions

## Is wXCK a separate cryptocurrency?

No. wXCK simply represents locked native XCK on another blockchain.

## Is wXCK backed?

Yes. Every wXCK is intended to be backed 1:1 by native XCK held by the bridge.

## Can I trade wXCK?

Yes. Because it is an ERC-20 token, it can be used anywhere that supports the deployed token and network.

## Which wallets can I use?

MetaMask is currently the officially supported wallet for interacting with the XCash Bridge. Additional EVM-compatible wallets may be supported in future release

---

# Need Help?

If you experience a problem while using the bridge:

- Verify that your transaction has received the required number of blockchain confirmations.
- Make sure you selected the correct bridge direction and network.
- Confirm that your destination XCK address is correct.
- If your transaction is still pending after the expected processing time, visit the **#help** section of the official XCash Labs Discord server for assistance.

---

# Important Notice

For your security, only use the official XCash Labs Bridge:

**https://wallet.xcashlabs.org/**

Before connecting your wallet or submitting a transaction, always verify that you are on the correct website.

Transactions sent to unofficial bridge websites, incorrect wallet addresses, or unsupported networks cannot be recovered. Never share your wallet seed phrase or private keys with anyone, including XCash Labs staff.