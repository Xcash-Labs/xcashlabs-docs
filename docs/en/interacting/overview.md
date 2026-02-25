---
title: Interacting with XCash Klassic
---
# Using XCash Klassic

XCash Klassic by XCash-Labs is a complete rewrite and modernization of the original X-CASH project, built on the Monero v0.18.3.4 codebase. It preserves the core privacy, transaction structure, and reliability of that foundation while introducing a redesigned consensus and governance model focused on long-term stability and coordinated block production. This document provides a high-level overview of the network’s current capabilities and will continue to expand as development progresses.

The XCash-Labs network operates using Delegated Proof-of-Private-Stake (DPoPS), in which the top 50 elected delegates are responsible for producing and validating blocks. This replaces traditional proof-of-work mining with a deterministic, delegate-driven system while maintaining the privacy technologies and transaction model inherited from Monero.

In addition to private transactions, XCash Klassic also supports an optional public transaction mode. Users can choose whether transaction details remain private or are publicly visible, providing flexibility depending on the intended use case.

Rather than requiring every user to run a full blockchain node, XCash Klassic is built around a delegate-based infrastructure. Wallets connect to trusted delegate nodes (remote nodes) instead of downloading and maintaining the full blockchain locally. Operating a full node is currently limited to registered delegate operators.

This architecture is designed to make XCash Klassic more accessible and easier to use for everyday participants. Most users can securely interact with the network through the desktop GUI wallet, command-line interface, or available APIs without needing to manage complex node infrastructure.

## How XCash Klassic differs from Monero

While XCash Klassic shares its privacy technology and transaction structure with Monero, several key areas of the network operate differently:

- **Consensus model**  
  Monero uses proof-of-work mining.  
  XCash Klassic uses Delegated Proof-of-Private-Stake (DPoPS), where elected delegates produce and validate blocks.

- **Network architecture**  
  Monero users typically run full nodes.  
  XCash Klassic users generally connect to delegate-run remote nodes instead of maintaining a full blockchain locally.

- **Governance**  
  Delegates are elected by token holders and are responsible for block production and network validation.

- **Transaction visibility options**  
  Private transactions remain the default, but XCash Klassic also supports optional public transactions for use cases that require transparency.

- **User experience focus**  
  The network is designed so most users can interact through wallets without running full infrastructure, reducing setup complexity while maintaining strong privacy and security.

## Acknowledgments and Open-Source Credits

  XCash Klassic is built on a foundation of open-source work made possible by the broader privacy-focused cryptocurrency community. We would like to acknowledge and thank the teams behind the CryptoNoteStarter, the Monero Project, and the original X-CASH team for developing and maintaining open-source code that made this project possible. Their work provided the technical groundwork upon which XCash Klassic has been rebuilt and modernized.