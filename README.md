# Rayls Private Transactions Research

This repository examines how financial institutions can use public blockchain infrastructure while preserving transaction confidentiality, auditability, and institutional control.

It contains two related research tracks:

1. **Deep Answer comparative research.** This track compares Ethereum, Canton Network, R3 Corda, and Rayls Enygma Public using a common set of research questions.
2. **Rayls Enygma forensic investigation.** This track examines the behavior and deployment history associated with a specific historical Enygma Public transaction. It uses transaction data, receipts, logs, contract sources, RPC observations, and upgrade records.

The research distinguishes documented product claims from independently inspected evidence. A feature described in official documentation does not, by itself, prove that a particular production deployment is configured or operating in that way.

---

## Main research question

> **How can financial institutions make private transactions on a public blockchain?**

The research addresses five questions:

1. Why would financial institutions want to use a public blockchain?
2. Which transaction information needs to be protected from public visibility?
3. How can transaction privacy be implemented on public blockchain infrastructure?
4. How can auditors obtain legitimate access to relevant information?
5. How can institutions retain control and meet compliance requirements?

The Deep Answer work is organized into three stages:

| Stage | Purpose | Current status |
|---|---|---|
| **Stage 1: Research scope** | Establish the main question, subquestions, comparison criteria, and required outputs. | Scope established |
| **Stage 2: Comparator research** | Examine Ethereum, Canton, R3 Corda, and Rayls Enygma using primary sources. Compare their network models, transaction privacy, auditor access, deployment status, and relevance. | In progress |
| **Stage 3: Self-verification** | Send one private payment on Enygma Public Testnet, inspect its public transaction evidence, and preserve the findings. | Historical transaction research exists. The required personally submitted payment still needs to be confirmed. |

**Important:** The historical Enygma transaction examined in the forensic track must not be presented as the researcher's own newly submitted payment. Stage 3 must remain incomplete until the quest's self-verification requirement has actually been satisfied.

---

## Projects in the comparison

The four projects serve different purposes in this research. They are not assumed to provide equivalent privacy or audit mechanisms.

| Project | Role in this research | Initial architectural focus |
|---|---|---|
| [Ethereum](analysis/deep-answer/projects/ethereum/README.md) | Public blockchain reference | Transparent base-layer ledger, with privacy tools and selective disclosure available across the ecosystem |
| [Canton Network](analysis/deep-answer/projects/canton/README.md) | Institutional network comparator | Sub-transaction privacy, stakeholder-based views, and permissions at the party and contract levels |
| [R3 Corda](analysis/deep-answer/projects/corda/README.md) | Permissioned DLT comparator | Point-to-point transaction distribution, notary privacy trade-offs, and observer-node reporting |
| [Rayls Enygma Public](analysis/deep-answer/projects/rayls-enygma/README.md) | Main subject of the Deep Answer research | Shielded payments on public blockchain infrastructure, encrypted notes, and deployment-level auditor access |

### Comparison criteria

Each project is examined using the same five dimensions:

- **Network model:** Public or permissioned characteristics, membership, participation, and control.
- **Transaction privacy:** What is visible to the public, counterparties, validators or notaries, relayers, and other participants.
- **Auditor access:** How access is granted, what information can be read, and what authority the auditor does or does not receive.
- **Deployment status:** Mainnet, production deployment, pilot, or testnet, including version and environment boundaries.
- **Relevance:** What the architecture demonstrates about private institutional transactions on public blockchain infrastructure.

The comparison is based on the documented behavior and scope of each system, not on marketing labels alone.

---

## Current research findings

### Auditor access

The current evidence review identifies four distinct models:

- **Ethereum:** Public on-chain data is readable by anyone. This is public transparency, not a dedicated auditor role at the base layer. Privacy applications may support selective disclosure.
- **Canton:** Daml contract observers can be assigned to provide visibility into selected contracts. Separately, an Observing Participant Node (OPN) can receive Observation permission for transactions involving a party hosted by that node. These are related but distinct mechanisms.
- **R3 Corda:** The Corda Enterprise observer-node example uses explicit application flows to distribute signed transactions to regulator nodes. This does not provide automatic, network-wide reporting.
- **Rayls Enygma Public:** Official documentation describes a deployment-level auditor key and encrypted copies of account view keys. These allow the auditor to read shielded transactions without obtaining spend authority.

The evidence and its limitations are recorded in the [auditor-access comparison](analysis/deep-answer/comparisons/auditor-access.md) and in each project's evidence files.

### Transaction privacy

The current comparison identifies different approaches to transaction privacy:

- **Ethereum:** The base layer is publicly transparent. Confidentiality can be added through application and protocol tools such as zero-knowledge proofs, stealth addresses, privacy pools, and selective disclosure.
- **Canton:** Transactions are decomposed into stakeholder-specific views and delivered to entitled participants. Divulgence remains an important design consideration.
- **R3 Corda:** Privacy depends on the notary and transaction-verification model. Non-validating and contract-verifying notary designs have different disclosure and trust trade-offs.
- **Rayls Enygma Public:** Shielded payment details are hidden from public observers. Encrypted notes, commitments, nullifiers, relayer information, and some public operations remain visible.

See the [transaction-privacy comparison](analysis/deep-answer/comparisons/transaction-privacy.md). These findings remain preliminary until the network model and deployment status have been fully reviewed across all four projects.

---

## Repository structure

```text
.
├── README.md
├── analysis/
│   ├── deep-answer/
│   │   ├── README.md
│   │   ├── projects/
│   │   │   ├── ethereum/
│   │   │   ├── canton/
│   │   │   ├── corda/
│   │   │   └── rayls-enygma/
│   │   └── comparisons/
│   │       ├── auditor-access.md
│   │       ├── transaction-privacy.md
│   │       └── final-comparison.md
│   └── rayls-enygma/
│       └── investigation-checkpoint-2026-11-28.md
└── sources/
    └── official-docs/
```

### Where to start

- [Deep Answer research index](analysis/deep-answer/README.md) contains the project status, navigation, and research methodology.
- [Ethereum evidence](analysis/deep-answer/projects/ethereum/README.md)
- [Canton evidence](analysis/deep-answer/projects/canton/README.md)
- [R3 Corda evidence](analysis/deep-answer/projects/corda/README.md)
- [Rayls Enygma Public evidence](analysis/deep-answer/projects/rayls-enygma/README.md)
- [Cross-project comparisons](analysis/deep-answer/comparisons/)
- [Rayls Enygma forensic checkpoint](analysis/rayls-enygma/investigation-checkpoint-2026-11-28.md)
- [Official Enygma fee and relayer-flow review](sources/official-docs/enygma-public-fee-and-relayer-flow-2026-11-27.json)

The dated JSON evidence records are retained as historical research records. The project-specific Markdown files provide the working navigation and synthesis structure. The existing forensic records are not replaced by the Deep Answer comparison files.

---

## Rayls Enygma forensic investigation

A separate analysis track examines the following historical transaction:

`0x09edab2bb8914aea3c905608ea9fcd09c056a470a5e150df03e0b324eff525bb`

- **Block:** 24,825,928
- **Timestamp:** 2026-11-21 09:40:42 UTC
- **Method:** `transferV2`
- **Destination:** SharedVaultProxy `0x9c5ad5e5ea5b5910e7fd1e1cc7b70ce0e4bf06c2`

The investigation covers transaction calldata and receipt structure, nullifiers, commitments, encrypted notes, receipt and circuit mapping, relayer and fee interpretation, proxy implementation chronology, OwnerMultisig proposals, and access-control pathways.

One current chronology result is that implementation `0xad9667049f14d1757d147f652c41dc241c57091c` is the **best-supported candidate** for the implementation active at the target transaction date. This conclusion is based on confirmed proposal execution and upgrade logs. Historical EIP-1967 storage could not be read because the RPC provider reported pruned historical state. Therefore, the chronology is not presented as a direct observation of the historical storage slot.

Several transaction semantics remain unresolved. These include the historical verifier-key slot, the exact token identity and denomination, the meaning of statement value `4416000000000000000`, and ownership of the third output note. See the [forensic checkpoint](analysis/rayls-enygma/investigation-checkpoint-2026-11-28.md) before continuing this track.

---

## Evidence and research methodology

Research records use explicit evidence classifications:

| Classification | Meaning |
|---|---|
| **Verified fact or direct observation** | A transaction, receipt, log, RPC response, source code, or downloaded source content that was inspected directly. |
| **Official documentation claim** | A statement made in the project's official documentation. It is not, by itself, independent proof of deployment behavior. |
| **Current source observation** | Behavior or structure found in a source version inspected now. Its historical applicability must be established separately. |
| **Reconstruction** | A result assembled from multiple observations, such as transaction and upgrade chronology. |
| **Inference** | A reasoned interpretation that is not directly established by the available evidence. |
| **Unknown or not verified** | Evidence is missing, inaccessible, ambiguous, or insufficient to support a conclusion. |

### Evidence-handling rules

1. Prefer primary sources, including official documentation, protocol specifications, source code, transaction receipts, event logs, and read-only RPC queries.
2. Record the source URL, retrieval date, product and version scope, and relevant lines or fields.
3. When a source is downloaded, record its HTTP result, final URL, file size, and SHA-256 hash where practical.
4. A successful HTTP 200 response or matching hash confirms retrieval or snapshot identity. It does not prove the truth of every claim on the page.
5. Do not treat an HTTP 403 response as source content. It indicates an access limitation.
6. Do not infer historical contract behavior from a newer implementation without a demonstrated upgrade timeline or historical state.
7. Do not treat missing logs from an incomplete index as proof that an event did not occur.
8. Keep application-level privacy, network-level privacy, public metadata, and auditor access distinct.
9. Keep product versions and editions separate when the evidence is version-specific.
10. Do not promote an inference or an official claim to an independently verified fact without additional evidence.

### Version and scope cautions

- Ethereum privacy tools have different designs and disclosure properties. They must not be treated as one unified protocol.
- Canton Daml contract observers and Participant Node Observation permission are distinct mechanisms.
- Current Corda privacy findings refer to Corda 5.2. The regulator observer-node example refers to Corda Enterprise 4.10. Do not merge these into one release or deployment claim.
- Rayls Enygma Public is treated as a testnet pilot in this research. Current product documentation does not automatically establish the configuration or behavior of a historical transaction.

---

## Research status

**As of 2026-11-28**

| Workstream | Status | Remaining work |
|---|---|---|
| Deep Answer Stage 1: scope | Established | Preserve the required research question and five subquestions. |
| Deep Answer Stage 2: auditor access | Evidence reviewed | Maintain version and access-scope boundaries. No named production deployment has been tested. |
| Deep Answer Stage 2: transaction privacy | Preliminary evidence reviewed | Complete claim-by-claim verification and harmonize the scope. |
| Deep Answer Stage 2: network model | In progress | Verify each model and avoid overbroad labels. |
| Deep Answer Stage 2: deployment status | In progress | Confirm mainnet, production, pilot, or testnet claims for each compared system. |
| Deep Answer Stage 2: final comparison | Not complete | Finalize only after all dimensions have primary-source support. |
| Deep Answer Stage 3: self-verification | Not complete | Confirm the required personally submitted Enygma private payment and preserve its evidence. |
| Rayls Enygma forensic investigation | In progress | Resolve proxy role-grant authority, historical implementation confidence, and remaining transaction semantics. |

---

## Scope and limitations

This repository is a research record. It is not a security audit certification, legal opinion, or proof that a named financial institution has deployed any specific architecture.

The comparison describes documented mechanisms and inspected evidence within the stated product and version scope. It does not assume that:

- all public blockchains provide the same privacy properties;
- all Canton or Corda deployments configure auditor access identically;
- all observers have the same rights;
- an auditor's read access implies spend, freeze, or administrative authority;
- a testnet demonstration proves production readiness; or
- current contract code proves historical transaction behavior.

The final article should make these distinctions clear and support factual claims with traceable sources.

---

## License and reuse

This README does not declare a repository-wide license. Unless a license is added, do not assume that the research notes, collected materials, or third-party source excerpts are offered for unrestricted reuse. Refer to each original source for its own licensing and attribution terms.
