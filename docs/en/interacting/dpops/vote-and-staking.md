---
title: Vote & Staking
description: As an XCash-Labs holder, you can stake your XCA and vote for a preferred delegate. Follow the guide below to understand how the voting and staking system works.
---

# Vote & Staking

!!! info ""
    Currently you can vote from the CLI wallet or GUI wallet.

## Find Your Delegate

All delegates are listed on the [XCash-Labs website](https://xcashlabs.org/delegates).  You will need to know the name of the delegate that you wish to vote for.

!!! danger "Unverified Delegate Information"
    Delegate information may be self-reported by delegates.  
    There may be no automated checks verifying fees, payouts, or claims.

!!! info ""
    Most delegates discuss openly on the official community Discord.  
    We recommend joining the discussion and asking questions before voting.

## Delegate Types

You will find 2 types of delegates:

- **Shared Delegates**
  - Public delegates you can vote for
  - Typically redistribute your share of rewards minus fees
  - As a voter, you should only vote for shared delegates

- **Solo Delegates**
  - Delegates who do not redistribute rewards to voters
  - Typically operated for by a singile XCash-Labs holder or a private group

## Staking Calculation

!!! note ""
    Rewards are **not guaranteed** and are **not a fixed ROI**.

    Block producer selection is based on VRF randomness, where the delegate with the **lowest VRF beta** wins the round.
    Because of this, rewards are probabilistic and may vary significantly over time depending on network conditions,
    total stake distribution, delegate participation, and fees.

## Voting & Staking

!!! info "Voting Rules"
    - **You can only have one vote per wallet.**
    - You need a minimum of `500` coins in the wallet to vote.
    - Only uses account 0 unlocked balance for funds
    - Spending from the staked wallet balance will invalidate the vote.

## Casting Your Vote

## Desktop Wallet

### Synchronize Your Wallet

You can synchronize by connecting to a remote node—ideally a seed node or another trusted delegate. You can find available domains and IP addresses on the [XCash-Labs website](https://xcashlabs.org/delegates). For best performance, choose a node located geographically close to you.

- **Seed Nodes**
    - seeds.xcashseeds.us (North America)
    - seeds.xcashseeds.uk (Europe)
    - seeds.xcashseeds.me (South America)
    - seeds.xcashseeds.cc (Asia)

### Remote Node Example

```bash
./xcash-wallet-cli --daemon-address seeds.xcashseeds.us:18281
```

### Restore Wallet

```bash
./xcash-wallet-cli --restore-deterministic-wallet --daemon-address seeds.xcashseeds.us:18281
```

### Prepare Your Vote

Before voting, consolidate outputs:

```bash
sweep_all <your_wallet_address>
```

Wait until funds are unlocked again before voting. Around 20 blocks or 20 minutes.

### Cast a Vote

```bash
vote <delegate_name_or_address> <amount | all>
```

### Revote

If your balance increases:

```bash
revote <amount>
```

## XCash-Labs Gui Wallet

Download: [https://xcashlabs.org/downloads](https://xcashlabs.org/downloads)

Steps:

1. Open wallet and sync

2. Select the Advanced tab on the left side of the menu

image

3. Select the Delegate you wish to vote from from the drop down and the Vote button will appear.

4. Click the vote button

In some cases, voting may fail because the wallet needs to generate a reserve proof that exceeds the current input size. To resolve this, use the Sweep function to consolidate all funds. After the swept funds unlock (approximately 20 minutes), you can attempt the vote again.

!!! info
    - The current minimum voting requirement is set at 50 XCK to encourage early participation. This threshold is expected to increase gradually as the network grows and distribution becomes broader.