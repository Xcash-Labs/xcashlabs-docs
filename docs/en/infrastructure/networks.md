---
title: Mainnet, Stagenet, Testnet
---
# Networks

!!! note ""
    XCash-Labs plans to offers multiple network environments to support both real-world usage and future development/testing:

    [**mainnet**](#mainnet)      
    [**testnet**](#testnet)   Planned for a future release.

    Every network has its own genesis block and is entirely separate from others.

## Nodes & Explorers

!!! danger "Spy Nodes and Explorers"
    Be cautious when using **_any_** remote node or block explorer.

    Malicious service providers may log and associate your IP address, TXIDs, addresses, and more.

### Nodes

**Delegate Nodes (Standard Model)**  
- XCash Klassic wallets connect to delegate-operated nodes (remote nodes) by design  
- These nodes maintain the full blockchain and participate in block production  
- Most users interact with the network through these delegate nodes  

**Choosing a Remote Node (Use Care)**  
- Remote node operators may observe connection metadata such as IP address and request timing  
- Prefer connecting to trusted or well-known delegates  
- Avoid using unknown public nodes for sensitive activity 


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
