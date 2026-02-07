---
title: Register Delegate
description: Once your server is set up and the necessary programs installed, you will be able to register yourself as a delegate.
---

# Register Delegate

## Introduction

Once you have correctly [set up your instance](node-installation.md) and installed the different programs, you can now register as a delegate of the X-Cash Public Network.

You will need to have all the services already running to generate the necessary parameters to register yourself as a delegate.

## 1. Register yourself as a delegate

You should have noted your block verifier keys during the [program installation](node-installation.md). You will need to prepare a **delegate name**, your **server IP address** or **domain name**, and the **block verifier public key**. You will register from the wallet that will be used to collect the reward.

!!! warning
    Choose your delegate name wisely, as you won't be able to change it later.

    If you want to change the name, you will need to generate a new block verifier key pair and register again — but you will lose your previous delegate stats.

First, stop the wallet service (if it is currently running in the background):

```bash
systemctl stop xcash-rpc-wallet
```

Open and let your wallet synchronize (the wallet you generated during node installation with the [Auto Installer Scrip](node-installation.md##auto-installer)):

```bash
~/xcash-official/xcash-core/build/release/bin/xcash-wallet-cli --wallet-file ~/xcash-official/xcash-wallets/<WALLET_NAME>
```

Replace **`<WALLET_NAME>`** with your wallet name.

!!! info
    If you installed with the auto-installer script, the wallet name is **`delegate-wallet`**.

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

Verify your node appears in the delegates explorer:
- https://delegates.xcash.foundation/

Exit the wallet, then restart the wallet service:

```bash
systemctl restart xcash-rpc-wallet
```

## 2. Update public information

Each registered delegate is displayed in the delegates explorer along with statistics and public information. At registration, the minimum displayed information is your **delegate name** and **IP address**. You can add additional details to help others identify you and decide to vote for you.

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
delegate_update <item> <value>
```

Available items:

| Item | Type | Description |
|---|---|---|
| `about` | **String** *(1024 char max)* | Short description about you and your motivations as a delegate. Example: `delegate_update about Even the smallest delegate can change the course of the future.` |
| `IP_address` | **String** *(255 char max)* | Update the IP address or domain name of your delegate node. (Must be IPv4 format per the original docs.) Example: `delegate_update IP_address mydomain.com` |
| `website` | **String** *(255 char max)* | Link to your landing page or website related to your delegate. Example: `delegate_update website my-delegate-website.com` |
| `team` | **String** *(255 char max)* | Team name, names, or profiles (if managed by multiple people). Example: `delegate_update team Manager: @tic | Treasury: @tac` |
| `shared_delegate_status` | **String** *(255 char max)* | One of: `solo`, `shared`, `group`. `shared` delegates set a fee and redistribute reward share. `group` is for private groups (see below). Example: `delegate_update shared_delegate_status group` |
| `delegate_fee` | **Number** | Percent fee `[0 - 100]` with up to 6 decimals. Example: `delegate_update delegate_fee 12.354321` |
| `server_specs` | **String** *(255 char max)* | Description of server hardware/specs. Example: `delegate_update server_specs Operating System = Ubuntu 20.04 - CPU = 6 threads (Intel E5-2630 v4 - 2.20GHz) - RAM = 16GB DDR4 - Hard drive = 400GB SSD - Bandwidth Transfer = Unlimited` |

You will be prompted to wait for the next valid data interval. Once accepted, you should see:

`The delegate info has been updated successfully`

Exit the wallet and restart the wallet service:

```bash
systemctl start xcash-rpc-wallet
```

## 3. Private group

A shared delegate can choose to run a private group, where the delegate decides which voters receive a share of the block reward. This is useful for a closed group that wants shared rewards but with a controlled distribution list.

To set this up, you will:

1. Create a configuration file listing voter/payment addresses.
2. Update `xcash-dpops.service` to use `--private-group <path-to-configuration-file>`.

Create the configuration file:

```bash
nano ~/xcash-official/xcash-dpops-configuration.txt
```

Add entries in this format:

```text
# Comment
wallet1|voting-address|payment-address
wallet2|voting-address|payment-address
```

Where:

- `voting-address` is the wallet address used to vote for the delegate
- `payment-address` is the wallet address that will receive the reward share

!!! info
    `voting-address` and `payment-address` can be the same.

!!! info
    The maximum number of `payment-address` entries allowed is **100**.

Once the config file is ready, update the systemd service:

1) Stop programs via the installer script:

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/X-CASH-official/xcash-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

Choose **option 13** to stop the programs.

2) Edit the service file and add `--private-group ...` to the `ExecStart` line:

```bash
nano /lib/systemd/system/xcash-dpops.service
```

Example `xcash-dpops.service`:

```ini
[Unit]
Description=X-Cash DPOPS Daemon background process

[Service]
Type=simple
LimitNOFILE=infinity
User=root
WorkingDirectory=~/xcash-official/xcash-dpops/build
ExecStart=~/xcash-official/xcash-dpops/build/xcash-dpops --private-group ~/xcash-official/xcash-dpops-configuration.txt --block-verifiers-secret-key BLOCK_VERIFIER_SECRET_KEY
Restart=always

[Install]
WantedBy=multi-user.target
```

3) Restart programs by running **option 12** of the auto-installer script:

```bash
bash -c "$(curl -sSL https://raw.githubusercontent.com/X-CASH-official/xcash-dpops/master/scripts/autoinstaller/autoinstaller.sh)"
```

## 4. Prepare shared delegate payments

As a shared delegate (normal or private group), you will distribute a share of the block reward to your voters.

On the first payment threshold, the program will automatically distribute the voters' share from the delegate wallet. However, the delegate wallet may be empty at first and you may be missing unspents to pay voters smoothly.

It is recommended to pre-fund your delegate wallet when first setting it up.

**Recommendation:** pre-fund between **500k to 1M XCASH** into the delegate wallet.
