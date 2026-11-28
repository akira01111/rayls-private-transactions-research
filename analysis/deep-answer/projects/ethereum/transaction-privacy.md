# Ethereum — transaction privacy

Status: official documentation reviewed; claims are ecosystem-level unless a specific standard or application design is named. Ethereum Mainnet itself remains a transparent public ledger.

## Base-layer boundary

Ethereum's base ledger does not hide ordinary on-chain actions. Addresses are pseudonymous, but the public transaction graph, token movements, contract calls, and activity patterns can be inspected. Privacy therefore depends on an application or protocol design layered above the base ledger; there is no single Ethereum-wide privacy configuration.

## Concrete mechanism example: ERC-5564 stealth addresses

ERC-5564 is a Final Standards Track ERC for stealth addresses. It lets a sender derive a one-time stealth address from a recipient's stealth meta-address, which contains spending and viewing public keys. The sender emits an announcement with the stealth address, caller, ephemeral public key, and metadata; the recipient uses a viewing key to identify incoming announcements and a spending key to control the funds.

**What it protects:** it makes it harder for public observers to associate the newly generated receiving address with the recipient's published identity or usual address.

**What it does not hide:** it does not make the base-layer transfer or amount confidential by itself. The ERC's recommended announcement metadata includes the token contract and amount for fungible assets (or token ID for NFTs); the public chain still exposes the transaction and its public data. It is therefore a recipient-linkability tool, not a full confidential-payment system.

The ERC defines separate viewing and spending keys. Ethereum's official privacy guide notes that a user can optionally share a viewing key with an authorized third party such as an accountant or tax software. That is user-controlled selective disclosure, not a universal auditor role imposed by Ethereum Mainnet.

## Other documented privacy directions

Ethereum's official privacy guide also describes:
- Zero-knowledge proofs for proving claims such as eligibility without revealing the underlying identity data.
- Privacy pools, which the guide describes as supporting on-demand compliance proofs for auditors or tax records.
- Selective disclosure in identity and financial applications.
- Stealth-address and private-payment tools developed in the ecosystem.

The privacy roadmap groups ongoing work into private reads, private writes, and private proving/identity protection. These are roadmap priorities and must not be described as features already provided uniformly by the base protocol.

## Evidence

1. [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/)
   - User Codespace retrieval: HTTP 200; 447,671 bytes.
   - SHA-256: e09fbcd7fbebd3dd142a0d02defb5aadd6f4738a4cd3192d3428e25f2f4ae2cf.
   - Local snapshot: /tmp/deep-answer-transaction-privacy/ethereum_privacy.html.
2. [ERC-5564: Stealth Addresses](https://eips.ethereum.org/EIPS/eip-5564)
   - Standards Track ERC; defines stealth meta-addresses, separate viewing/spending keys, announcement events, and public metadata structure.
3. [The privacy roadmap for Ethereum](https://ethereum.org/roadmap/privacy/)
   - Describes private reads, private writes, and private proving as roadmap priorities.

## Evidence classification and limits

- **Official documentation claim:** Ethereum's base ledger is transparent; privacy tools and selective-disclosure approaches exist in its ecosystem.
- **Standards specification:** ERC-5564 specifies a method for recipient unlinkability and viewing-key based scanning.
- **Not independently tested:** this research did not deploy a stealth-address wallet or audit a specific privacy application.
- Do not describe stealth addresses as hiding transaction amounts or all metadata.
- Do not treat roadmap objectives as shipped or universally deployed Mainnet capabilities.
- Do not treat the Ethereum ecosystem's collection of tools as one uniform privacy system.

## Institutional relevance

Ethereum demonstrates the difference between public settlement and application-level confidentiality. A stealth address can reduce recipient linkability; a ZK or privacy-pool design can support other forms of selective disclosure. An institution would still need to assess the exact application's disclosure model, key custody, audit process, and deployment status. See [auditor access](auditor-access.md).
