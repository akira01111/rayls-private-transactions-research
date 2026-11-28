# Ethereum — transaction privacy

Status: official documentation snapshot retrieved and its relevant content inspected; claims are ecosystem-level unless explicitly stated otherwise.

## Findings

Ethereum's base ledger is transparent. The official privacy page states that public blockchains like Ethereum operate as immutable, fully transparent ledgers and that every on-chain action is visible to anyone inspecting the ledger. Public-key pseudonymity does not prevent activity-pattern analysis from revealing sensitive information.

Privacy is available through an ecosystem of tools and application designs, including:

- Zero-knowledge proofs for private identity/eligibility proofs.
- Private voting applications.
- On-chain private transaction tools.
- Stealth addresses.
- Privacy pools with proof-of-innocence or association-set-provider compliance models.
- Selective disclosure to chosen parties.

Important distinction: using a ZK rollup does not by itself make transactions confidential. The privacy properties depend on the rollup or application design, such as encrypted state and proving transactions locally.

The page also describes a roadmap that includes private reads, private writes, and private proving. These are roadmap priorities, not proof that every capability is already native or universally deployed on Ethereum Mainnet.

## Evidence

1. Official documentation: [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/)
   - User Codespace terminal retrieval: HTTP 200.
   - Downloaded size: 447,671 bytes.
   - SHA-256: e09fbcd7fbebd3dd142a0d02defb5aadd6f4738a4cd3192d3428e25f2f4ae2cf.
   - Local snapshot: /tmp/deep-answer-transaction-privacy/ethereum_privacy.html
   - Extracted content included the transparent-ledger statement, pseudonymity limitation, ZK proofs, privacy tools, privacy pools, selective disclosure, and the distinction between ZK scaling and confidentiality.

2. Official documentation: [The privacy roadmap for Ethereum](https://ethereum.org/roadmap/privacy/)

3. Base network context: [Networks](https://ethereum.org/developers/docs/networks/)

## Evidence classification

- Official documentation claim: public on-chain actions are transparent and inspectable.
- Official documentation claim: privacy tools and selective-disclosure applications exist in the Ethereum ecosystem.
- Interpretation: privacy is not uniformly provided by the base layer; it can be added through applications and cryptographic mechanisms.

## Limitations

- This review does not audit any specific privacy application or verify its cryptographic implementation.
- The terminal snapshot hash identifies the downloaded page; it does not independently prove the correctness or security of the tools listed.
- No live transaction or privacy application was tested in this research step.

## Open questions

- Select one or two concrete Ethereum privacy applications for deeper mechanism-level review, rather than treating the ecosystem list as one uniform system.
- Compare what is hidden from the public, what is revealed to counterparties, and what can be disclosed to auditors for each selected application.