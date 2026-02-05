---
title: Get Started
description: Overview of XCash-Labs DPoPS consensus, voting, staking, and how to participate in the network.
---

# Get Started

**DPoPS (Delegated Proof of Private Stake)** is a custom consensus mechanism used by XCash-Labs.  
It combines elements of Delegated Proof of Stake (DPoS), Byzantine Fault Tolerance (BFT), and
Verifiable Random Functions (VRF), while preserving user privacy.

---

## Introduction

The XCash-Labs public network is governed by a fixed set of delegates responsible for block
verification and production.

- Anyone can run an XCash-Labs node
- Anyone may register as a delegate
- Only elected delegates may produce blocks

To become an active block producer, a delegate must be voted into the active delegate set by
network participants.

Delegate positions are **not permanent**. Delegates may lose their position at any time if they
fail to meet network expectations or lose community support.

This documentation helps you:

- understand how DPoPS works
- set up a delegate node
- register as a delegate
- vote and participate in governance
- securely operate within the network

---

## What would you like to do?

### Learn about the consensus

If you want to understand how DPoPS works and what makes it different, start with the
technical documentation describing the consensus design and security model.

DPoPS was designed specifically for XCash-Labs and is built to work alongside a privacy-focused
blockchain.

---

### Become a delegate

To run a delegate node:

1. Prepare a server (Linux recommended)
2. Install the delegate node software
3. Register yourself as a delegate
4. Get elected by voters

Refer to:
- Server setup guide
- Delegate node installation guide
- Delegate registration guide

---

### Vote for a delegate

If you want to support the network without running infrastructure, you can vote for a delegate
using your wallet.

See:
-  [Vote & Staking guide](../interacting/vote-and-staking.md)

---

### Participate in beta testing

During beta phases:

- Delegates must follow additional instructions
- Voters may participate with test rules or limits

Refer to:
- Delegate setup guide
- Vote & Staking guide

---

## Key Characteristics

### Delegates & Consensus

- A fixed number of delegates act as block verifiers
- Consensus requires a supermajority agreement to finalize blocks
- The system tolerates a minority of faulty or offline delegates
- Blocks continue to be produced as long as consensus thresholds are met

---

### Block Producer Selection

- Block producers are selected using **Verifiable Random Functions (VRF)**
- The delegate with the **lowest VRF beta value** is selected for block production
- Selection is random but fully verifiable by the network
- No delegate can predict or influence future selection

---

## Staking Model

- Voting uses **reserve-proof–based staking**
- Staked coins always remain in your wallet
- There is **no lockup period**
- Funds can be spent at any time

!!! note ""
    Spending from a wallet used for voting will invalidate the reserve proof
    and cancel the vote.

- Wallets do **not** need to stay online
- Voting toward shared delegates requires no ongoing maintenance

---

## Voting Rules

- A minimum stake is required to vote for a delegate
- Voting is evaluated continuously by the network
- New votes are applied automatically
- Changing your vote cancels the previous one
- There are no voting fees
- Votes may be changed at any time

---

## Blocks & Data Storage

- Blocks can be inspected using the XCash-Labs daemon
- Voting and reserve-proof data is stored in a decentralized database layer
- Only hashes of this data are stored on-chain
- This design minimizes blockchain growth while preserving verifiability

---

## Summary

XCash-Labs DPoPS provides:

- decentralized governance
- privacy-preserving staking
- verifiable randomness
- no custodial lockups
- no guaranteed rewards
- fair and transparent delegate selection

Continue with the relevant guides to begin participating in the network.
