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

# ---- guide to Monero GUI ----

xcash-gui-wallet-guide.pdf

# ---- main executable files -----------

monerod
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
| `monerod`                  | The full node daemon. Does not require a wallet. <br />[Documentation](../interacting/monerod-reference.md).
| `xcash-wallet-gui`        | Wallet logic and __graphical__ user interface. <br />Requires `monerod` running.
| `xcash-wallet-cli`        | Wallet logic and __commandline__ user interface. <br />Requires `monerod` running.
| `xcash-wallet-rpc`        | Wallet logic and __HTTP API__ (JSON-RPC protocol). <br />Requires `monerod` running.
| `xcash-blockchain-prune`  | Prune existing local blockchain. This saves 2/3 of disk space (down to {{ lmdb_size_pruned }} GiB  as of {{ lmdb_size_updated }}). This is preferable over `monerod --prune-blockchain` which only logically releases space inside the file while the file remains large. The `xcash-blockchain-prune` creates a shrunken copy of the blockchain file. See [tutorial1](https://monero.stackexchange.com/questions/11454/how-do-i-utilize-blockchain-pruning-in-the-gui-xcash-wallet-gui), [tutorial2](https://www.publish0x.com/solareclipse/howto-prune-shrink-the-database-of-the-xcash-blockchain-on-xpgwjx).
| `xcash-gen-ssl-cert`      | Generate 4096 bit RSA private key and self signed TLS certificate for use with `monerod` RPC interface. Note, Monero daemon automatically generates TLS certificate on each restart. Manual generation with this tool is only useful if you want to pin TLS certificate fingerprint in your monero wallet. See the [pull request](https://github.com/xcash-project/monero/pull/5495).
| `xcash-gen-trusted-multisig`          | Tool to generate a set of multisig wallets. <br />See chapter on [multisignatures](../multisignature.md).
| `xcash-blockchain-export` | Tool to export blockchain to `blockchain.raw` file.
| `xcash-blockchain-import` | Tool to import a raw blockchain, ideally your own trusted copy.

## Executables - legacy

You most likely should not bother with these legacy or very specialized tools.

| Executable                 | Description
| -------------------------- |:-----------------------------------------------------------------------------------------------------------------------------------
| `xcash-blockchain-stats`              | Generate stats like tx/day, blocks/day, bytes/day based on your local blockchain.
| `xcash-blockchain-mark-spent-outputs` | Advanced tool to mitigate potential privacy issues related to Monero forks. You normally shouldn't be concerned with that.<br />See the [commit](https://github.com/xcash-project/monero/commit/df6fad4c627b99a5c3e2b91b69a0a1cc77c4be14#diff-0410fba131d9a7024ed4dcf9fb4a4e07) and [pull request](https://github.com/xcash-project/monero/pull/3322).
| `xcash-blockchain-prune-known-spent-data`  | Previous limited pruning tool to prune select "known spent" transaction outputs (from the before RCT era). Nowadays prefer `xcash-blockchain-prune`. This only saves ~200 MB. See the [commit](https://github.com/xcash-project/monero/commit/d855f9bb92dbfab707a0e37505906366de818a14).
| `xcash-blockchain-usage`              | Advanced tool to mitigate potential privacy issues related to Monero forks. You normally shouldn't be concerned with that.<br />See the [commit](https://github.com/xcash-project/monero/commit/0590f62ab64cf023d397b995072035986931a6b4) and the [pull request](https://github.com/xcash-project/monero/pull/3322).
| `xcash-blockchain-ancestry`           | Advanced research tool to learn ancestors of a transaction, block or chain. Irrelevant for normal users. See this [pull request](https://github.com/xcash-project/monero/pull/4147/files).
| `xcash-blockchain-depth`              | Advanced research tool to learn depth of a transaction, block or chain. Irrelevant for normal users. See this [commit](https://github.com/xcash-project/monero/commit/289880d82d3cb206a2cf4ae67d2deacdab43d4f4#diff-34abcc1a0c100efb273bf36fb95ebfa0).


## Interacting

There are quite a few ways you can interact with Monero software.
Perhaps the most surprising for newcomers is that `monerod` daemon accepts interactive keyboard commands while it is running.

Also, please note that `monerod` and `xcash-wallet-rpc` are both accessible via their respective HTTP API / JSON-RPC endpoints.

- [monerod-rpc](../rpc-library/monerod-rpc.md)
- [wallet-rpc](../rpc-library/wallet-rpc.md)

All wallet implementations depend on a fully synchronized `monerod` running.

| Executable                                              | p2p network | commands via keyboard                          | HTTP API                           | GUI |
| ------------------------------------------------------- | :---------: | :--------------------------------------------: | :--------------------------------: | :-: |
| [`monerod`](./monerod-reference.md)                     | ✔           | [✔](./monerod-reference.md#commands)           | [✔](../rpc-library/monerod-rpc.md) |     |
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
