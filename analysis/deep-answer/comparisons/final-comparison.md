# Deep Answer — final comparison

Status: **evidence comparison complete within the documented scope**. This matrix synthesizes the four systems across all five required dimensions. It does not claim independent audits of every named institutional deployment or independent decryption of Rayls' testnet auditor path. Stage 3 remains a separate user-run requirement.

## Five-dimension comparison

| Project | Network model | Transaction privacy | Auditor access | Deployment status | Relevance |
|---|---|---|---|---|---|
| Ethereum | Public Proof-of-Stake L1; public read/transaction access. Testnets differ (Sepolia validator set is permissioned). | Base ledger is transparent. Privacy tools add recipient unlinkability, ZK proofs, privacy pools, or selective disclosure, each with different guarantees. | Public data is readable by everyone; application-level viewing keys or compliance proofs can disclose selected information. No base-layer auditor role. | Mainnet is live production. Privacy application status must be assessed separately. | Baseline for open settlement and public verifiability; demonstrates why privacy must be added above a transparent base ledger. |
| Canton | Public network with decentralized synchronization; validator sponsorship and application-level permissioning currently apply. | Encrypted stakeholder-specific views; participants see entitled contracts/actions; divulgence can expand visibility. | Daml contract observers and OPN Observation are distinct, scoped mechanisms. | MainNet is the production environment; applications have their own deployment and permissioning status. | Demonstrates interoperability with party/contract-level control over data disclosure. |
| R3 Corda 5.2 | Permissioned application networks with MGM membership. | Peer-to-peer flows, filtered transactions, and notary options create different disclosure/trust boundaries. | CorDapp can send signed transaction reports to observer nodes through explicit flows (example is Enterprise 4.10). | Corda 5.2 supports production dynamic networks; a named live Corda 5.2 deployment is not verified here. Enterprise 4.10 example is separate. | Permissioned DLT comparator; demonstrates strong membership control and application-directed disclosure, but is not a public blockchain. |
| Rayls Enygma Public | Privacy application on the public EVM-compatible Rayls Public Chain; validator admission is currently documented as permissioned. | Shielded notes and encrypted notes conceal payment parties/values from public observers while commitments, nullifiers, and public operations remain visible. | Deployment auditor key with encrypted account view keys; read capability is documented as separate from spend authority. | Rayls Public Chain Mainnet launched 2026-04-30; Enygma Public itself remains a testnet pilot. Enygma Sovereign is a separate product. | Main case for layering private payments onto public-chain infrastructure with public cryptographic traces and a documented deployment-level auditor path. |

## What the comparison shows

1. **Public infrastructure does not require public transaction plaintext.** A public ledger can support privacy layers that hide selected payment fields while leaving commitments, proofs, or metadata verifiable.
2. **Privacy is audience-specific.** The relevant question is not simply whether a system is “private,” but which information each observer, counterparty, validator/notary, synchronizer, relayer, and auditor can see.
3. **Auditor access is not one standard feature.** It ranges from public visibility and user-selected disclosure to contract observers, application reporting flows, and deployment-level auditor keys.
4. **The trust boundary moves rather than disappears.** Institutions still rely on cryptographic correctness, key custody, application configuration, notary/synchronizer operation, and governance.
5. **Deployment scope matters.** A production base chain does not prove a specific privacy application is in production. Rayls Public Chain Mainnet and Enygma Public testnet pilot must be reported separately.

## Synthesis for the main question

Financial institutions can use public or interoperable blockchain infrastructure for programmable settlement, shared state, broader connectivity, and atomic workflows while keeping commercially sensitive transaction content from public observers. They do this by separating data needed for public verification from private data needed by counterparties and authorized auditors. Cryptographic proofs, encrypted transaction views, filtered disclosure, and scoped auditor access are different ways to implement that separation.

The architecture is not complete without institutional control: identity and eligibility, key custody, governance of upgrades, operational accountability, and regulatory processes must be designed alongside the privacy mechanism. No single comparator supplies the same balance of openness, privacy, and audit access.

## Remaining validation limits

- The historical Enygma transaction on 2026-11-21 is not the user's required self-verification payment.
- Rayls auditor decryption has not been independently tested in this research.
- Corda's observer-node example is Enterprise 4.10; Corda 5.2 privacy/network findings remain version-specific.
- Named institutional deployments and their exact application configurations are not independently audited here.
- The Rayls forensic reconstruction of implementation 0xad966... is based on confirmed upgrade chronology and authorization review; direct historical EIP-1967 storage was unavailable due to pruned RPC state.

The comparison is complete as an evidence-based architecture review. Final quest completion still requires Stage 3 self-verification and a final editorial/source check before submission.
