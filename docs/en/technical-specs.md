---
title: XCash-Labs Technical Specification
---
# XCash-Labs Technical Specs

## Live

* XCash-Labs blockchain is live since 2026-01-10 (genesis)

## No premine, no instamine, no ICO, no token

* XCash-Labs launched with no premine and no instamine
* No ICO / no presale / no airdrop
* XCK is the native coin of the network (not a token)

## Delegated Proof of Private Stake (DPoPS)

* DPOPS
    * Consensus: DPoPS (Delegated Proof of Private Stake)
    * Active since: genesis (block height 0/1)
    * Based on Monero protocol era v18 (core codebase v0.18)

## Difficulty retarget

* XCash-Labs uses DPoPS block production, therefore PoW difficulty retargeting is not used (PoW hash fields may exist for format compatibility)

## Block time

* 1 minute

## Block reward

* smoothly decreasing and subject to penalties for blocks greater than median size of the last 100 blocks (M100)
* 47.070 XMR as of February ; for the current reward check the coinbase transaction of the [latest block](https://xmrchain.net/)

## Block size

* dynamic
* Block size penalties apply when blocks exceed the median size window

## Current blockchain size

* Pruned node: ~{{ lmdb_size_pruned }} GiB as of {{ lmdb_size_updated }}
* Full node: ~{{ lmdb_size_full }} GiB as of {{ lmdb_size_updated }}

## Emission curve

### Main emission

* ~50% emitted (~50M XCK): ~2.8 years
* ~90% emitted (~90M XCK): ~9.2 years
* Emission model: Monero-style exponential decay toward the supply target, with a fixed tail emission floor


### Tail emission

* Tail emission begins when remaining supply is ~1,468,006.4 XCK, meaning about 98,531,993.6 XCK are emitted beforehand
* The tail emission kick in after main emission is done (around ~16.8 years after genesis)
* Tail emission: 0.700000 XCK per minute (after main emission drops below the floor)
* tail emission produces ~367,920 XCK/year, which is: ~0.37% annual inflation at 100M supply and will decrease over time

## Max supply

* Total intended base supply: 100,000,000 XCK (6 decimals; 1 XCK = 1,000,000 atomic units)
* technically infinite but practically deflationary if accounted for lost coins

## Divisibility

* XCash-Labs is divisible up to 0.000001 XCK (6 decimals)

## Sender privacy

* ring signatures
    * the ring size is 16 (15 decoys)
* assurance: probabilistic / plausible deniability

## Recipient privacy

* stealth addresses
* assurance: strong

## Amount privacy

* ring confidential transactions
* assurance: strong

## Network privacy (IP layer)

###Full nodes (DPoPS nodes)

* XCash Labs full nodes are DPoPS consensus nodes
* Nodes communicate directly with other delegates / committee peers
* The network layer is not designed to provide IP anonymity by default
* Operators should assume delegate IP addresses are public / discoverable
* IP-layer privacy is separate from on-chain privacy (ring signatures / stealth addresses / RingCT)

###Recommended protection for node operators:

* run nodes behind a firewall and strict allowlists
* restrict inbound ports and enforce rate limits
* monitor connectivity and latency (DPoPS relies on stable networking)
 
Note: Tor-style routing is not a default assumption for DPoPS nodes because the protocol depends on reliable timing, availability, and stable peer connectivity.