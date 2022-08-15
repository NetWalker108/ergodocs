---
tags:
  - P2P
---

# P2P Protocol Overview

The Ergo network protocol allows full nodes (peers) to collaboratively maintain a peer-to-peer network for block and transaction exchange.

## Introduction

The **Full Node** downloads and verifies every block (and transaction) before it relays them to other nodes. 

Significant improvements have been made to the P2P layer over the past few months.

- [P2P layer optimizations - part I #1290](https://github.com/ergoplatform/ergo/pull/1290)
- [Rust implementation of Ergo peer-to-peer networking](https://github.com/ergoplatform/ergo-p2p)
- [p2p issues on Ergo Repo](https://github.com/ergoplatform/ergo/issues?q=p2p)

## [Handshake](/dev/p2p/p2p-handshake)


Nodes perform *handshaking* by sending each other `handshake messages.`

## [Network Messages](/dev/p2p/network)

## [Modifier Exchange](/dev/p2p/modifiers)

## Syncing


## Misc

- On mainnet P2P uses port `9030` (`9053` for the API)
- For crawling [https://libp2p.io/](libp2p.io/)

### P2P Smart Contracts

Ergo allows truly P2P smart contracts. Just run the node and a local interface.


- [Mixicles - simple private contracts on top of oracle data](https://research.chain.link/mixicles.pdf) - Implementation-wise, onchain part would simple, p2p off-chain interaction is needed (and would be the most labour-intensive part likely)
- P2P Pools