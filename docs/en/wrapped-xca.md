# Wrapped XCash-Klassic (wXCK)

## Introduction

Wrapped **XCash Klassic (wXCK)** is the official ERC-20 representation of native **XCash Klassic (XCK)**, enabling XCK to be used on supported EVM-compatible blockchains. The XCash Bridge currently supports the **Base** and **Polygon** networks, allowing users to seamlessly move assets between the native XCash Klassic blockchain and supported EVM ecosystems.

Every **1 wXCK** is backed by **1 XCK** securely held in reserve by the XCash Labs Bridge, maintaining a fully backed 1:1 relationship between wrapped and native assets. This design enables XCK holders to access decentralized exchanges (DEXs), decentralized applications (dApps), wallets, and other EVM-compatible services without changing the underlying value of their holdings.

This guide explains what wXCK is, how the XCash Bridge operates, and how to safely transfer assets between native XCK and supported EVM networks. It also covers the bridge process, supported networks, contract information, fees, security considerations, and recommended best practices.

## Official wXCK Contract Information

Always verify that you are interacting with the official wXCK smart contract for your network.

| Network  |
|----------|
| **Base** |
| Contract Address|

```text
0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b
```
| **Polygon** |
|0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b|

Base

```text
0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b
```

### Polygon

```text
0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b
```

> **Note:** The official wXCK smart contract uses the same contract address on both the Base and Polygon networks, making it easier to identify the authentic token regardless of the supported network.

> **Important:** Only use the official contract addresses published by XCash Labs. Interacting with unofficial or impersonating contracts may result in the permanent loss of funds.

> **Warning:** Only use the official contract addresses published by XCash Labs. Interacting with unofficial or impersonating contracts may result in the permanent loss of funds.

## Block Explorer

### Base

| Resource | Link |
|----------|------|
| Token | https://basescan.org/token/0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b |
| Verified Contract | https://basescan.org/address/0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b#code |
| Holders | https://basescan.org/token/0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b#balances |
| Transfers | https://basescan.org/token/0x26194f4cC88FfcfbABfa22e1fAF7fE5Eb0eE802b#tokentxns |

### Polygon

*Coming Soon*

The XCash Bridge, along with your complete bridge request history, is available directly within the **XCash Klassic Lite Wallet**:

[XCash Klassic Lite Wallet](https://wallet.xcashlabs.org/)

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

## Converting XCK into wXCK

![XCK to wXCK](../../images/xck-to-wxck.png)

Bridging **XCK** to **wXCK** requires two separate transactions:

- A native **XCK** transaction that sends your XCK to the bridge.
- A **MetaMask** transaction that claims your **wXCK** on the destination network.

To convert native **XCK** into **wXCK**:

1. Open the **XCash Klassic Lite Wallet** and unlock the wallet you want to use.
2. Click the **Bridge** button to open the XCash Bridge.
3. Open **MetaMask** and ensure the connected dApp and selected network match the destination network you want to bridge to.
4. Select the destination network  (**Polygon** or **Base**).
5. Click the arrow to determine the direction for your transfer. Ensure the bridge direction is **XCK → wXCK**.
6. Enter the amount of XCK you want to bridge.
7. Click **Start Bridge**.
8. Review and confirm the XCK transaction, then click **Done**.
9. Wait for **10 XCash blockchain confirmations** (approximately **10 to 11 minutes**) while the bridge verifies your deposit. You can click **Refresh** at any time to check the current bridge status.
10. Once your deposit has been verified, the **Claim wXCK** button will appear.
11. Click **Claim wXCK** and approve the transaction in your connected MetaMask wallet.

After the claim transaction has been confirmed on the destination network, your **wXCK** is available in your connected MetaMask wallet. If this is your first time using wXCK, you will need to import the token into MetaMask before your balance is displayed. You can import the token by clicking the **Import into MetaMask** button from the **Bridge History** screen. Be sure to select the correct bridge record for the network you are using (**Polygon** or **Base**).

The token only needs to be imported once for each network and MetaMask wallet.

Note: You can close the bridge screen once you have clicked the "Start Bridge" button. When you click the bridge button again, any active 
bridge request will be restored automatically.

---

## Converting wXCK back into XCK

![wXCK to XCK](../../images/wxck-to-xck.png)

Bridging **wXCK** back into **XCK** also requires two separate transactions:

- A **MetaMask** transaction that burns your **wXCK** on the selected EVM network.
- A native **XCK** transaction sent by the bridge to your XCash Klassic wallet after the burn has been verified.

To convert **wXCK** back into native **XCK**:

1. Open the **XCash Klassic Lite Wallet** and unlock the wallet you want to receive the XCK.
2. Click the **Bridge** button to open the XCash Bridge.
3. Select the network that currently holds your **wXCK** (**Polygon** or **Base**).
4. Click the arrow to determine the direction for your transfer. Ensure the bridge direction is **XCK ← WXCK**.
5. Open **MetaMask** and verify that the connected dApp and selected network match the network you selected.
6. Enter the amount of **wXCK** you want to bridge.
7. Click **Start Bridge**.
8. Confirm the burn transaction in your connected MetaMask wallet.
9. Wait while the bridge verifies the burn transaction and releases the corresponding native **XCK**.
10. Once the bridge has completed the transfer, the native **XCK** will be sent to your currently unlocked XCash Klassic wallet.

> **Note:** You may close the Bridge window after clicking **Start Bridge**. When you open the Bridge again, any active bridge request will be restored automatically so you can continue where you left off.

---

## Bridge History

![bridge history](../../images/bridge-history.png)

The **Bridge History** screen allows you to view your current and completed bridge requests. Each record includes links to the appropriate blockchain explorers so you can easily verify both the native XCK transaction and the corresponding EVM transaction.

For completed **XCK → wXCK** bridge requests, an **Import into MetaMask** button is available. Clicking this button imports the **wXCK** token definition into MetaMask, allowing your wallet to display your wXCK balance if the token has not already been imported.

The token only needs to be imported once for each MetaMask wallet on each supported network.

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