---
title: Interacting with XCash-Labs
---
# Interacting with XCash-Labs

You can interact with XCash-Labs via desktop GUI, commandline interface, and programming API.

On top of that, XCash-Labs nodes interact with each other in a peer-to-peer network.

## Installation directory overview

Once unpacked you will see several executable files. You will also find a nice PDF guide for the GUI wallet.

XCash-Labs project nicely decouples network node logic from wallet logic.
Wallet logic is offered through three independent user interfaces - the GUI, the CLI, and the HTTP API.

```
# cd xcash-gui-{{ cli_vers }}

# ---- guide to XCash-Labs GUI ----

xcash-gui-wallet-guide.pdf

# ---- main executable files -----------

xcashd
xcash-wallet-gui

# ---- extra executable files -----------

extras/xcash-wallet-cli
extras/xcash-wallet-rpc

extras/xcash-blockchain-prune
extras/xcash-gen-trusted-multisig
extras/xcash-gen-ssl-cert

extras/xcash-blockchain-export
extras/xcash-blockchain-import

# ---- don't bother with these ----------

extras/xcash-blockchain-stats
extras/xcash-blockchain-mark-spent-outputs
extras/xcash-blockchain-prune-known-spent-data
extras/xcash-blockchain-usage
extras/xcash-blockchain-ancestry
extras/xcash-blockchain-depth
```

## Executables

| Executable                 | Description
| -------------------------- |:-----------------------------------------------------------------------------------------------------------------------------------
| `xcashd`                  | The full node daemon. Does not require a wallet. <br />[Documentation](../interacting/xcash-reference.md).
| `xcash-wallet-gui`        | Wallet logic and __graphical__ user interface.
| `xcash-wallet-cli`        | Wallet logic and __commandline__ user interface.
| `xcash-wallet-rpc`        | Wallet logic and __HTTP API__ (JSON-RPC protocol). <br />Requires `xcashd` running.
| `xcash-blockchain-prune`  | Prune existing local blockchain. This saves 2/3 of disk space (down to {{ lmdb_size_pruned }} GiB  as of {{ lmdb_size_updated }}). This is preferable over `xcashd --prune-blockchain` which only logically releases space inside the file while the file remains large. The `xcash-blockchain-prune` creates a shrunken copy of the blockchain file.
| `xcash-gen-ssl-cert`      | Generate 4096 bit RSA private key and self signed TLS certificate for use with `xcashd` RPC interface. Note, XCash-Labs daemon automatically generates TLS certificate on each restart. Manual generation with this tool is only useful if you want to pin TLS certificate fingerprint in your XCash-Labs wallet.
| `xcash-gen-trusted-multisig`          | Tool to generate a set of multisig wallets. <br />See chapter on [multisignatures](../multisignature.md).
| `xcash-blockchain-export` | Tool to export blockchain to `blockchain.raw` file.
| `xcash-blockchain-import` | Tool to import a raw blockchain, ideally your own trusted copy.

## Executables - legacy

You most likely should not bother with these legacy or very specialized tools.

| Executable                 | Description
| -------------------------- |:-----------------------------------------------------------------------------------------------------------------------------------
| `xcash-blockchain-stats`              | Generate stats like tx/day, blocks/day, bytes/day based on your local blockchain.
| `xcash-blockchain-mark-spent-outputs` | Advanced tool to mitigate potential privacy issues related to forks. You normally shouldn't be concerned with that.
| `xcash-blockchain-prune-known-spent-data`  | Previous limited pruning tool to prune select "known spent" transaction outputs (from the before RCT era). Nowadays prefer `xcash-blockchain-prune`. This only saves ~200 MB.
| `xcash-blockchain-usage`              | Advanced tool to mitigate potential privacy issues related to forks. You normally shouldn't be concerned with that.
| `xcash-blockchain-ancestry`           | Advanced research tool to learn ancestors of a transaction, block or chain. Irrelevant for normal users.
| `xcash-blockchain-depth`              | Advanced research tool to learn depth of a transaction, block or chain. Irrelevant for normal users.


## Interacting

There are quite a few ways you can interact with XCash-Labs software.
Perhaps the most surprising for newcomers is that `xcashd` daemon accepts interactive keyboard commands while it is running.

Also, please note that `xcashd` and `xcash-wallet-rpc` are both accessible via their respective HTTP API / JSON-RPC endpoints.

- [xcash-rpc](../rpc-library/xcash-rpc.md)
- [wallet-rpc](../rpc-library/wallet-rpc.md)

All wallet implementations depend on a fully synchronized `xcashdx` running.

| Executable                                              | p2p network | commands via keyboard                          | HTTP API                           | GUI |
| ------------------------------------------------------- | :---------: | :--------------------------------------------: | :--------------------------------: | :-: |
| [`xcashd`](./xcashd-reference.md)                     | ✔           | [✔](./xcashd-reference.md#commands)           | [✔](../rpc-library/xcash-rpc.md) |     |
| [`xcash-wallet-cli`](./xcash-wallet-cli-reference.md) |             | [✔](./xcash-wallet-cli-reference.md#commands) |                                    |     |
| [`xcash-wallet-rpc`](./xcash-wallet-rpc-reference.md) |             |                                                | [✔](../rpc-library/wallet-rpc.md)  |     |
| [`xcash-wallet-gui`](./xcash-wallet-gui-reference.md) |             |                                                |                                    | ✔   |

## Data directory

This is where the blockchain, log files, and p2p network memory are stored.

By default data directory is at:

* `$HOME/.XCASH-LABS/` on Linux and macOS
* `C:\ProgramData\XCASH-LABS\` on Windows

Please mind:

* data directory is hidden as per OS convention

Data directory contains:

* `lmdb/` - the blockchain database directory
* `p2pstate.bin` - saved memory of discovered and rated peers
