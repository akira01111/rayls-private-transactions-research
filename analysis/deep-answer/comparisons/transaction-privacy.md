# Deep Answer — transaction privacy comparison

Status: comparative review completed against official documentation and standards. This compares documented mechanisms, not independently audited implementations or named institutional deployments.

| Project | Mechanism | Protected information / audience | What remains visible or trusted | Main limitation |
|---|---|---|---|---|
| Ethereum | Transparent public base layer; application/protocol privacy such as ZK proofs, privacy pools, selective disclosure, and ERC-5564 stealth addresses | Depends on the selected tool. ERC-5564 reduces the public link between a recipient's identity and a one-time receiving address. ZK systems can prove selected facts without revealing underlying data. | Mainnet transactions and public contract data remain inspectable. ERC-5564 announcements expose the stealth address, caller, ephemeral public key, view tag, and recommended token/amount metadata. | No uniform Ethereum-wide confidentiality model. A stealth address does not hide transfer amount or all metadata. |
| Canton | Stakeholder-specific sub-transaction views, encrypted to entitled recipients | Parties receive the contract/action views their stakeholder roles entitle them to see; signatories, observers, and controllers have different roles. | Synchronizer coordinates processing and sees encrypted messages and confirmation results. Divulgence can disclose related contracts beyond an initial observer list. | Privacy depends on application contract design, stakeholder definitions, and network topology. |
| R3 Corda 5.2 | Peer-to-peer transaction flows; non-validating or contract-verifying notary; filtered transactions with Merkle proofs | Counterparties receive transaction data required for their participation. A non-validating notary sees limited components; filtered transactions reveal relevant components for verification. | Non-validating notary sees references, output count, time window, notary identity, and metadata. Contract-verifying notary receives transaction content and is trusted to verify contracts. | The privacy configuration changes the notary trust boundary; this is a permissioned DLT architecture, not a public base chain. |
| Rayls Enygma Public | Shielded notes, encrypted notes, nullifiers, commitments, and relayer-mediated transactions | Official documentation says public observers cannot see the sender, recipient, amount, or spent notes of a shielded payment; recipient sees amount/token but not sender identity; relayer cannot see sender/recipient/amount. | Public observers can see that a shielded payment occurred and inspect relayer/gas data, nullifiers, commitments, encrypted notes, registered public keys and public shield/unshield/registration activity. Auditor is documented to see shielded transaction details through a deployment-level view-key process. | Enygma Public is a testnet pilot. Auditor decryption has not been independently tested in this research. |

## Interpretive points

1. **Privacy is audience-specific.** A system may hide information from public observers while disclosing it to counterparties, a notary, a synchronizer, an auditor, or a regulator.
2. **Public evidence is not the same as public plaintext.** Commitments, nullifiers, encrypted notes, and transaction occurrences can remain visible without revealing the private payment values.
3. **Not every privacy tool hides the same fields.** ERC-5564 primarily reduces recipient linkability; it does not provide complete confidential transfers. ZK proofs and privacy pools have different disclosure goals.
4. **Canton and Corda use different distribution boundaries.** Canton distributes encrypted stakeholder views; Corda relies on participant involvement, flows, notary protocol, and filtered transactions.
5. **Rayls' documented model separates public traces and private payment content.** Its deployment auditor is an explicit trusted disclosure path, but current auditor decryption is still an official product claim in this evidence pack.

## Evidence sources

- Ethereum: [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/), [ERC-5564: Stealth Addresses](https://eips.ethereum.org/EIPS/eip-5564), [Privacy roadmap](https://ethereum.org/roadmap/privacy/).
- Canton: [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model), [Participant Node Architecture](https://docs.canton.network/overview/reference/participant-overview), [raw privacy-model MDX](https://raw.githubusercontent.com/canton-network/cf-docs/main/docs-main/overview/learn/privacy-model.mdx).
- Corda: [Transaction Privacy Enhancements — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/enhanced-ledger-privacy.html), [Non-Validating Notary — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/non-validating-notary.html), [Notary Protocols — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/notary-protocols.html).
- Rayls: [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what), [How Enygma Public works](https://docs.rayls.com/docs/how-enygma-public-works).

## Scope limits

- Ethereum examples are ecosystem-level and standards/documentation references, not an audit of a selected live privacy dApp.
- Canton findings describe documented platform architecture, not a specific bank's deployment.
- Corda findings refer to Corda 5.2. They are not automatically applicable to Enterprise 4.10/4.14.
- Rayls findings describe official Enygma Public documentation and remain separate from historical transaction semantics in the Rayls forensic investigation.
