# Ethereum — auditor access

Status: base-layer read access and ecosystem selective-disclosure patterns documented. No single Ethereum-wide auditor role is identified by the reviewed sources.

## Public data versus selective disclosure

- Public Ethereum data is readable by anyone. This is general public transparency, not a dedicated auditor permission.
- Ethereum's privacy documentation describes selective disclosure as a way for users to reveal chosen information to chosen parties.
- The guide gives stealth-address users as an example: a user may optionally share a viewing key with authorized third parties such as accountants or tax software.
- Privacy pools are described as generating on-demand cryptographic proofs of compliance (for example, proof-of-innocence style evidence) for auditors and tax records.

## Concrete key distinction: viewing versus spending

ERC-5564 defines a viewing key used to determine whether a stealth address belongs to a recipient and a separate spending key used to control funds. A recipient may share a viewing key to support selective monitoring, but this is not an Ethereum-level auditor role and does not imply that every Ethereum privacy application uses the same key scheme.

## Evidence

1. [Networks](https://ethereum.org/developers/docs/networks/) — public network access.
   - Codespace snapshot SHA-256: 835711ee4021bcac282813c361cb45cf980ef0112c4e4bfc28d4f9157e38c6b8.
2. [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/) — selective disclosure, viewing-key sharing examples, and privacy-pool compliance proofs.
   - Codespace snapshot SHA-256: e09fbcd7fbebd3dd142a0d02defb5aadd6f4738a4cd3192d3428e25f2f4ae2cf.
3. [ERC-5564: Stealth Addresses](https://eips.ethereum.org/EIPS/eip-5564) — separates viewing and spending keys.

## Classification and limits

- **Official documentation claim:** public on-chain data is accessible to anyone.
- **Official ecosystem examples:** viewing-key sharing and privacy-pool proofs can support selected third-party/audit disclosure.
- **Standards specification:** ERC-5564 defines separate viewing and spending keys for a stealth-address scheme.
- **Not established:** a universal auditor identity, global auditor key, or base-layer auditor-only access control.
- Do not equate ordinary public ledger access with private audit access. Application/protocol-specific disclosure must be evaluated separately.
