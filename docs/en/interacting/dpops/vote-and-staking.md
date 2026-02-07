---
title: Vote & Staking
description: Learn how to stake your coins and vote for a delegate as an XCash-Labs holder, and understand how the voting and staking system works.
---

# Vote & Staking

!!! warning ""
    Currently you can vote from the CLI wallet, Android wallet, and GUI wallet.

## Find Your Delegate

All delegates are listed on the delegate explorer.

!!! danger "Unverified Delegate Information"
    Delegate explorer information may be self-reported by delegates.  
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
  - Typically operated for the delegate’s own staking/voting 

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
    - Spending from the staked wallet balance will invalidate the vote.

## Casting Your Vote


## Desktop Wallet

### Synchronize Your Wallet

You can synchronize by:

1. Running a local daemon (most secure, slower)
2. Connecting to a remote node (faster)

### Remote Node Example

```bash
./xcash-wallet-cli --daemon-address us1.xcash.foundation:18281
```

### Restore Wallet

```bash
./xcash-wallet-cli --restore-deterministic-wallet --daemon-address us1.xcash.foundation:18281
```

### Prepare Your Vote

Before voting, consolidate outputs:

```bash
sweep_all <your_wallet_address>
```

Wait until funds are unlocked again before voting.

### Cast a Vote

```bash
vote <delegate_name_or_address> <amount | all>
```

Your wallet must remain open until the top of the hour for confirmation.

### Revote

If your balance increases:

```bash
revote <amount>
```

## Android Wallet

!!! warning
    The Android wallet is still in beta. Always back up your keys and seed.

Download:  
https://github.com/X-CASH-official/android-wallet/releases

Steps:

1. Open wallet and sync
2. Tap the DPoPS button
3. Select delegate
4. Tap **Vote**
5. Wait for confirmation at the top of the hour

You will receive rewards in this wallet after voting.
