---
title: Mainnet, Stagenet, Testnet
---
# Networks

!!! note ""
    XCash-Labs plans to offers multiple network environments to support both real-world usage and future development/testing:

    [**mainnet**](#mainnet)    
    [**stagenet**](#stagenet)    
    [**testnet**](#testnet)    

    Every network has its own genesis block and is entirely separate from others.

## Nodes & Explorers

!!! danger "Spy Nodes and Explorers"
    Be cautious when using **_any_** remote node or block explorer.

    Malicious service providers may log and associate your IP address, TXIDs, addresses, and more.
    If you must use untrusted nodes, consider using them over Tor (Onion) or I2P whenever supported.

### Nodes

- Nodes - Self-Hosted (Recommended)
    - Run your own XCash-Labs node
    - Use a node which is controlled by somebody you trust

- Nodes - Remote (Use caution)
    - Remote nodes are convenient, but may reduce privacy
    - Prefer nodes operated by trusted community members or infrastructure providers


### Block Explorers - Self-Hosted

- XCash-Labs Explorer (self-hosted) *(recommended)*
- Community explorers *(when available)*


## Mainnet

!!! info ""
    Mainnet is the "production" network and blockchain.

    Mainnet is the only blockchain where **XCK units have value**.

    Mainnet is the default network.

??? tip "Mainnet Block Explorers"
    - XCash-Labs Explorer: *(https://explorer.xcashlabs.org/)*

??? abstract "Mainnet TCP ports"
    - 18280 - [Default] P2P Network
    - 18281 - [Default] Unrestricted JSON-RPC
    - 18282 - [Default] ZMQ RPC *(if enabled)*
    - 18283 - DPoPS / delegate network transport (XCASH_DPOPS_PORT)
    - 18285 - Wallet RPC
    - 18289 - Restricted JSON-RPC *(if enabled)*

??? abstract "Database - internal services"
    - MongoDB: 127.0.0.1:27017 (DATABASE_CONNECTION)

## Stagenet
    **Stagenet is planned for a future release.**
    Stagenet will be available for users and developers to learn and build on XCash-Labs safely, without using mainnet coins.

    When launched, stagenet will be intended to remain technically equivalent to mainnet, both in terms of features and consensus rules.

??? tip "Stagenet resources"

??? abstract "Stagenet TCP ports"

## Testnet
    **Testnet is planned for a future release.**

    Testnet will be the "experimental" network and blockchain where protocol features can be tested long before mainnet.

    Testnet may fork earlier and more often than mainnet.
    Developers should keep their sources up to date and compile often.

??? tip "Testnet resources"

??? abstract "Testnet TCP ports"

## FAQ

??? question "Why do stagenet and testnet coins have no value?"

    A: This is simply the convention the community embraces.
    Value only comes from a shared belief that mainnet coins will be accepted by other people in the future.
