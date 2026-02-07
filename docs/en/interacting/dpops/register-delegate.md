---
title: Register Delegate
description: Once your server is set up and the necessary programs installed, you will be able to register yourself as a delegate.
---

# Register Delegate

## Introduction

Once you have correctly [set up your instance](node-installation.md) and installed the different programs, you can now register as a delegate of the X-Cash Public Network.

You will need to have all the services already running to generate the necessary parameters to register yourself as a delegate.

## 1. Register yourself as a delegate

You should have noted your block verifier keys during the [node program installation](node-installation.md). You will need to prepare a **delegate name**, your **server IP address** or **domain name**, and the **block verifier public key**. You will register from the wallet that will be used to collect the reward.

!!! warning
    Choose your delegate name wisely, as you won't be able to change it later.

    If you want to change the name, you will need to generate a new block verifier key pair and register again — but you will lose your previous delegate stats.

!!! info
    Shared delegates should pre-fund their wallet to ensure early reward payouts. It is recommended to keep approximately **500k–1M XCASH** in the delegate wallet before rewards begin.

First, stop the wallet service (if it is currently running in the background):

```bash
systemctl stop xcash-rpc-wallet
```

Open and let your wallet synchronize (the wallet you generated during node installation with the [auto installer script](node-installation.md#auto-installer)): 

```bash
~/xcash-official/xcash-core/build/release/bin/xcash-wallet-cli --wallet-file ~/xcash-official/xcash-wallets/<WALLET_NAME>
```

Replace **`<WALLET_NAME>`** with your wallet name.

!!! info
    If you installed with the auto-installer script, the wallet name is **`delegate-wallet`**.

Set the inactivity timeout so it does not time out while waiting on commands to complete.

```bash
set inactivity-lock-timeout 300
```

Once your wallet is fully synchronized, run:

```bash
delegate_register <delegate_name> <IP_address|domain_name> <block_verifier_public_key>
```

Parameter details:

- **`<delegate_name>`**: name displayed on the delegate explorer. *Cannot be updated.*
- **`<IP_address|domain_name>`**: your server IP address or domain name.
  - Recommended: use a domain name, so you can redirect it to a new IP later if you move servers.
  - *Can be updated.*
- **`<block_verifier_public_key>`**: block verifier public key you generated earlier. *Cannot be updated.*

Example:

```bash
delegate_register my_delegate my_delegate.domain.com cf8718d638ce0a831f3538ea60d1e27c3a258c7004a1ad7c547cc5331de7d9d7
```

You will be prompted to wait for the next valid data interval. Once accepted, you should see:

`The delegate has been registered successfully`

!!! info
    Note: it will take 10 mins for your delegate to become active and you do not have to keep the wallet open.

Exit the wallet, then use the "Restart Programs" option from the auto installer script to restart all programs .

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Xcash-Labs/xcash-labs-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

## 2. Update public information

Minimal delegate information is stored at the time of registration. Currently, there is no public interface to view this data, but it may be displayed in future tools or explorer features as they are developed. At a minimum, your delegate name and IP address are recorded. You may also include additional details now so they can be shown later when public viewing tools become available.

Stop the wallet service:

```bash
systemctl stop xcash-rpc-wallet
```

Open and synchronize the wallet you used to register:

```bash
~/xcash-official/xcash-core/build/release/bin/xcash-wallet-cli --wallet-file ~/xcash-official/xcash-wallets/<WALLET_NAME>
```

!!! info
    If you installed with the auto-installer script, the wallet name is **`delegate-wallet`**.

Once synchronized, use:

```bash
delegate_update "<item>"="<value>","<item>"="<value>"
```
You can include one or more <item>=<value> pairs in a single command by separating them with commas. This allows you to update multiple settings at once.

Available items:

| Item | Type | Description |
|---|---|---|
| `about` | **String** *(512 char max)* | Short description about you and your motivations as a delegate. Example: `delegate_update "about"="Even the smallest delegate can change the course of the future."` |
| `IP_address` | **String** *(255 char max)* | Update the IP address or domain name of your delegate node. (Must be IPv4 format per the original docs.) Example: `delegate_update "IP_address"="mydomain.com"` |
| `website` | **String** *(255 char max)* | Link to your landing page or website related to your delegate. Example: `delegate_update "website"="my-delegate-website.com"` |
| `team` | **String** *(255 char max)* | Team name, names, or profiles (if managed by multiple people). Example: `delegate_update "team"-"Manager: @tic | Treasury: @tac`" |
| `delegate_type` | **String** *(255 char max)* | One of: `solo`or `shared`. `shared` delegates set a fee and redistribute reward share and solo delegates will probably want to set solo_addresses. |
| `delegate_fee` | **Number** | Fee percentage `[0–100]`, max 2 decimal places. Default is 5%. Example: `delegate_update "delegate_fee"="5.50"` | |
| `server_specs` | **String** *(255 char max)* | Description of server hardware/specs. Example: `delegate_update "server_specs"="Operating System = Ubuntu 20.04 - CPU = 6 threads (Intel E5-2630 v4 - 2.20GHz) - RAM = 16GB DDR4 - Hard drive = 400GB SSD - Bandwidth Transfer = Unlimited"` |
| `minimum_payout` | **Number** | Minimum payout for stakers `[1 - 10000]`. Larger payout will reduce the number of transactions. Default is 5000. Example: `delegate_update "minimum_payout"="1000"` |
| `solo_addresses` | **String** | For solo delegates, you can specificy a list of up to 10 public wallet addresses that may vote for this solo delegate. This just limites who can vote for the delegate. `delegate_update "solo_addresses"="[address1, address2]"` |

You will be prompted to wait for the next valid data interval. Once accepted, you should see:

`The delegate info has been updated successfully`

Exit the wallet, then use the "Restart Programs" option from the auto installer script to restart all programs. 

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/Xcash-Labs/xcash-labs-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

## 3. Private group

A shared delegate can choose to run a private group, where the delegate decides which voters receive a share of the block reward. This is useful for a closed group that wants shared rewards but with a controlled distribution list.

To set this up, just use the delegate_update and the sole_addresses option to set the public wallet addresses that can vote for this solo delegate. The voting address must then vote for the delegate just as they would for any other delegate.


## 4. Prepare shared delegate payments

As a shared delegate (normal or private group), you will distribute a share of the block reward to your voters.

On the first payment threshold, the program will automatically distribute the voters' share from the delegate wallet. However, the delegate wallet may be empty at first and you may be missing unspents to pay voters smoothly.


