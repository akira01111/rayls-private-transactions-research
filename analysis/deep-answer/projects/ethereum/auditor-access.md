# Ethereum — auditor access

Status: base-layer read access and ecosystem selective-disclosure patterns documented; no single Ethereum-wide auditor role identified.

## Findings

- Public-chain data is readable by anyone. This is public transparency, not a dedicated auditor permission.
- The Ethereum privacy documentation describes selective disclosure as a way for users to reveal chosen information to chosen parties.
- It gives examples of stealth-address users optionally sharing a viewing key with authorized third parties such as accountants or tax software.
- Privacy pools can produce on-demand cryptographic compliance proofs for auditors and tax records.

## Evidence

1. [Networks](https://ethereum.org/developers/docs/networks/) — public network access.
   - Terminal snapshot SHA-256: 835711ee4021bcac282813c361cb45cf980ef0112c4e4bfc28d4f9157e38c6b8.
2. [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/) — selective disclosure, viewing-key sharing examples, and privacy-pool compliance proofs.
   - Terminal snapshot SHA-256: e09fbcd7fbebd3dd142a0d02defb5aadd6f4738a4cd3192d3428e25f2f4ae2cf.

## Classification

- Official documentation claim: public on-chain data is accessible to anyone.
- Official ecosystem examples: viewing-key sharing and privacy-pool proofs can support selected third-party/audit disclosure.
- Not established: a universal auditor identity, global auditor key, or base-layer auditor-only access control.

## Limitations

Do not equate ordinary public ledger access with private audit access. The privacy mechanisms described are application/protocol-specific and must be assessed individually.