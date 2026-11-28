# Deep Answer — answer synthesis

Status: evidence-based answer framework completed on 2026-11-28. Claims below distinguish official source statements, observed evidence, and synthesis.

## Main question

**How can financial institutions make private transactions on a public blockchain?**

They can use public or interoperable blockchain infrastructure for shared settlement and public verification while moving sensitive transaction details behind a privacy layer. The privacy layer can use encrypted notes or stakeholder-specific views, commitments and zero-knowledge proofs, filtered transaction disclosure, or application-level selective disclosure. Counterparties receive the data they need to execute a transaction; auditors receive a separately governed read path; public observers see only the data the protocol intentionally exposes.

This is not “make the whole chain invisible.” It separates:
1. public evidence that a state transition or transaction occurred;
2. private transaction content needed by participants;
3. selectively disclosed information needed for audit or compliance; and
4. governance authority over keys, participants, and upgrades.

## 1. Why would financial institutions use public or shared blockchain infrastructure?

The evidence identifies possible benefits:
- **Programmability:** smart contracts can automate financial logic such as collateral transfers, coupon payments, or margin processes.
- **Shared state and reconciliation:** a synchronized ledger can reduce repeated bilateral reconciliation.
- **Atomic settlement:** delivery-versus-payment can make asset and payment legs settle together.
- **Connectivity and interoperability:** a shared infrastructure may connect multiple institutions, applications, assets, and liquidity pools.
- **Longer operating windows:** blockchain-based settlement can support operational windows beyond conventional banking hours, depending on the network, asset, and settlement arrangement.

These benefits are not exclusive to permissionless public blockchains. Permissioned networks can also offer programmability and atomic settlement. The BIS identifies a trade-off: open permissionless networks can create accountability and legal-responsibility problems, while isolated private networks can fragment interoperability. Public-permissioned designs may occupy a middle ground.

**Evidence classes:** IMF and BIS official analysis; dated Visa pilot/settlement announcements; DTCC announced future integration plan. Do not rewrite pilots or plans as universal production adoption.

## 2. Which information needs to be protected?

The specific privacy requirements depend on the asset and transaction, but an institutional design should assess at least:

- **Counterparty identity and linkability:** who is paying whom, and whether multiple transactions can be linked to the same institution, customer, or account.
- **Amount and asset details:** transfer value, token/asset identity, and balance changes.
- **Commercial position and activity patterns:** holdings, trading positions, payment timing, business relationships, and repeated flows that can reveal strategy or liquidity.
- **Transaction payloads:** contract terms, invoice/settlement context, instructions, or other business data.
- **Private note/account state:** the owner and spendable value represented by shielded notes or private account records.

This list is a **design inference**, not a claim that every comparator hides all these fields. Public metadata may still be required for ordering, fees, auditing, proof verification, and network operations. The key is to define which audience is allowed to see each field.

## 3. How can privacy be implemented on public blockchain infrastructure?

The four comparators demonstrate different mechanisms.

### Ethereum — add privacy at the application/protocol layer

Ethereum Mainnet is transparent. ERC-5564 stealth addresses reduce the public link between a recipient's identity and a one-time receiving address, but the public transfer and recommended token/amount metadata remain visible. Zero-knowledge proofs and privacy-pool designs can support other privacy and compliance disclosures. The properties must be evaluated per application; “uses Ethereum” does not mean “is confidential.”

### Canton — distribute encrypted stakeholder views

Canton decomposes transactions into views, encrypts them for entitled recipients, and distributes them to the relevant participants. Signatories, observers, and controllers have distinct rights. Divulgence can reveal related contracts beyond an initial observer list. This provides application/party-scoped privacy over shared synchronization infrastructure.

### R3 Corda — control transaction distribution and notary disclosure

Corda 5.2 participants exchange transaction data through peer-to-peer flows. A non-validating notary sees selected components; a contract-verifying notary receives transaction content so it can verify contracts. Filtered transactions use Merkle proofs to disclose relevant components. The design trades data minimization against trust in the notary and its protocol.

### Rayls Enygma Public — shielded notes and public cryptographic artifacts

Rayls documents shielded payments using notes, encrypted notes, commitments, and nullifiers. Public observers can see that a shielded payment occurred and inspect cryptographic artifacts and relayer/gas metadata, while the documentation says the sender, recipient, amount, and spent notes remain hidden from the public. Shielding, unshielding, and registration remain public operations.

The Enygma Public documentation also describes a deployment-level auditor path. Enygma Public itself remains a testnet pilot, not a production Mainnet app.

## 4. How can auditors obtain legitimate access?

Auditor access should be an explicit disclosure mechanism with defined scope and authority:

- **Ethereum:** public information is readable by everyone; selected private information may be disclosed through viewing keys or cryptographic compliance proofs. There is no base-layer auditor-only role.
- **Canton:** add an auditor as an observer to selected Daml contracts, or use an OPN with Observation permission for a hosted party. These mechanisms are distinct and scoped; Observation alone does not permit submitting or confirming transactions.
- **Corda:** a CorDapp can send digitally signed transaction reports to regulator observer nodes using explicit application flows. This is not automatic for every application.
- **Rayls:** official documentation describes a deployment auditor key. An account's view-key copy is encrypted to that key using ML-KEM-768 and stored in the registry. The view key provides read/decrypt capability; spending requires the separate spend key.

The practical assurance questions are key custody, who authorizes disclosure, what exact data is exposed, whether access is logged and time-bounded, revocation/rotation, and whether the auditor path has been independently tested.

## 5. How can institutions retain control and meet compliance requirements?

Privacy cryptography alone does not establish institutional compliance. An institution still needs controls for:
- participant identity and eligibility;
- key generation, storage, rotation, recovery, and revocation;
- governance of contracts, registries, verifiers, and upgrades;
- authorization for auditors and regulators;
- records and reporting that match legal obligations;
- incident response, dispute handling, and operational accountability.

The comparators make different governance choices: Ethereum's base layer has public participation; Canton combines a public network with sponsored validator onboarding and application-level permissioning; Corda 5.2 uses MGM membership; Rayls documents a Public Chain validator onboarding model and a deployment-level owner multisig for relevant contracts. Enygma Public's testnet status means its documented mechanisms should not be presented as production financial-institution controls proven in live use.

The Rayls forensic Batch 01 review scanned all 24 current OwnerMultisig proposals and identified the direct SharedVaultProxy upgrade and role-grant actions. It found no pre-2026-11-21 direct proxy grant of DEFAULT_OWNER_ROLE among the six decoded grant actions; the best-supported implementation reconstruction for the historical transaction is 0xad966.... This is a scoped reconstruction, not a direct historical storage read: historical EIP-1967 state was pruned, and indirect/non-multisig paths were not ruled out.

## Conclusion

A credible institutional privacy design does not choose between “everything public” and “everything hidden.” It keeps public the evidence needed for shared verification, hides commercially sensitive transaction data from unauthorized observers, provides narrowly scoped and auditable access to legitimate reviewers, and places keys, participants, and upgrade authority under explicit governance. The right balance depends on the asset, participants, jurisdiction, and operational model.

## Important evidence limits

- No named bank's exact deployment configuration is independently audited in this research.
- Rayls Enygma Public remains a testnet pilot; its auditor decryption mechanism is documented but not independently tested.
- The historical 2026-11-21 Rayls transaction is not the user's required self-submitted Stage 3 payment.
- The historical Rayls implementation and some transaction semantics remain a chronology reconstruction or unresolved, as recorded in the forensic checkpoint.
