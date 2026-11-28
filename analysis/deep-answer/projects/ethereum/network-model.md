# Ethereum — network model

Status: preliminary; the model is clear at a high level, but this project file is not yet a complete network-architecture review.

## Supported observations

- Ethereum public networks are accessible to anyone with an internet connection.
- Anyone can read or create transactions on a public blockchain and validate transactions.
- Ethereum Mainnet is described by ethereum.org as the primary public production blockchain.

## Evidence

1. Official documentation: [Networks](https://ethereum.org/developers/docs/networks/)
   - User Codespace terminal retrieval: HTTP 200.
   - Downloaded size: 444,383 bytes.
   - SHA-256: 835711ee4021bcac282813c361cb45cf980ef0112c4e4bfc28d4f9157e38c6b8.
   - Local snapshot at time of review: /tmp/deep-answer-auditor/ethereum.html

## Classification

- Official documentation claim: public network access and ability to read/create/validate transactions.
- Scope limitation: this describes public networks/base-layer access. It does not classify every Ethereum application or Layer 2 as permissionless.

## Still to verify

- Whether the final comparison should describe Ethereum Mainnet only or distinguish Mainnet from the broader Ethereum ecosystem.
- How institutional permissioning and privacy applications sit above the public base layer.