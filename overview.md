# Oeconomia Overview

Oeconomia is a multi-protocol DeFi ecosystem built around the OEC token. Everything is
currently live on the **Sepolia testnet** for testing; there is no mainnet launch yet.

## Protocols
| Protocol | What it does | Docs |
|---|---|---|
| **Eloqura** | Decentralized exchange: swaps, liquidity pools, limit orders | `protocols/eloqura/` |
| **Alluria** | CDP lending: deposit collateral (WETH, WBTC, LINK), mint the ALUD stablecoin, Stability Pool | `protocols/alluria/` |
| **OEC Staking** | Stake OEC in multiple pools for APR rewards; testnet faucet; achievement rewards | `protocols/oec-staking/` |
| **Oeconomia Hub** (oeconomia.io) | Dashboard, analytics, portfolio, ecosystem overview, roadmap, presale page | `protocols/dao-hub/` |

## How they connect
- OEC is the shared token: staked in OEC Staking, traded and paired on Eloqura, and paid
  as rewards (e.g. Alluria Stability Pool OEC rewards).
- ALUD, minted on Alluria, trades on Eloqura.
- Presale funds are planned to go mostly into Eloqura OEC liquidity (see `tokenomics.md`).

## Getting started on testnet
1. Add Sepolia to your wallet and get Sepolia ETH from a public faucet.
2. Claim test OEC from the OEC Faucet (staking site).
3. Try a swap on Eloqura, stake OEC, or open an Alluria position.

Key facts live in one place each: tokenomics in `tokenomics.md`, addresses in `contracts.md`.
