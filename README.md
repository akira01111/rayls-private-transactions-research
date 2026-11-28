# Rayls Private Transactions Research

Research repository examining how financial institutions can use public blockchain infrastructure while preserving transaction confidentiality, auditability, and institutional control.

The repository contains two related research tracks:

1. **Deep Answer comparative research** — compares Ethereum, Canton Network, R3 Corda, and Rayls Enygma Public.
2. **Rayls Enygma forensic investigation** — reconstructs the behavior and deployment history surrounding a historical Enygma Public transaction using transaction data, receipts, logs, contract sources, read-only RPC observations, and upgrade records.

The research distinguishes documented product claims from independently inspected evidence. A feature described in official documentation is not automatically proof that a particular deployment is configured or operating in that way.

---

## Main research question

> **How can financial institutions make private transactions on a public blockchain?**

Five questions structure the work:

1. Why would financial institutions want to use a public blockchain?
2. Which transaction information needs to be protected from public visibility?
3. How can transaction privacy be implemented on public blockchain infrastructure?
4. How can auditors obtain legitimate access to relevant information?
5. How can institutions retain control and meet compliance requirements?

## Current stage status — 2026-11-28

| Stage | Purpose | Status |
|---|---|---|
| **1 — Research scope** | Establish question, subquestions, comparison criteria, and required outputs. | Scope established |
| **2 — Comparator research** | Compare Ethereum, Canton, Corda, and Rayls across network model, privacy, auditor access, deployment status, and relevance. | Network model and deployment status harmonized; privacy/auditor synthesis and final relevance matrix still in progress |
| **3 — Self-verification** | Send one private payment personally on Enygma Public Testnet and inspect its public evidence. | Pending user's own testnet payment; historical transaction does not satisfy this step |

## The four comparators

| Project | Role | Network/deployment boundary |
|---|---|---|
| [Ethereum](analysis/deep-answer/projects/ethereum/README.md) | Public-blockchain reference | Ethereum Mainnet is a live public production network; testnets and privacy applications have separate scopes. |
| [Canton Network](analysis/deep-answer/projects/canton/README.md) | Institutional-network comparator | Public network with application-level permissioning and sponsored validator onboarding; MainNet production environment is active. |
| [R3 Corda](analysis/deep-answer/projects/corda/README.md) | Permissioned DLT comparator | Corda 5.2 documents production-capable dynamic application networks with MGM membership; Enterprise 4.10 observer example is a separate version. |
| [Rayls Enygma Public](analysis/deep-answer/projects/rayls-enygma/README.md) | Main subject | Rayls Public Chain Mainnet is live, but Enygma Public remains a testnet pilot. Enygma Sovereign is a separate institutional edition. |

### Comparison criteria

Every project is assessed using the same five dimensions:

- **Network model** — public/permissioned characteristics, membership, validation, and control.
- **Transaction privacy** — what public observers, counterparties, validators/notaries, relayers, and other participants can see.
- **Auditor access** — how access is granted, what can be read, and whether reading is separated from spending or administration.
- **Deployment status** — Mainnet/production, pilot, testnet, product-version, and application-deployment boundaries.
- **Relevance** — what the architecture demonstrates about private institutional transactions on public or interoperable infrastructure.

## Current comparative findings

### Network model and deployment

The base chain and the privacy application must not be given one shared status:
- Ethereum Mainnet is live production; Sepolia is a testnet with a permissioned validator set.
- Canton is a public network with per-application permissioning; validator sponsorship is currently needed, and MainNet is the production environment.
- Corda 5.2 supports production dynamic networks with MGM membership; this capability does not by itself verify a named live deployment.
- Rayls Public Chain Mainnet launched on 2026-04-30, while Enygma Public remains a testnet pilot using no-value test tokens. Rayls' validator onboarding page describes a permissioned validator set; a future permissionless approval model is roadmap language.

See [network model comparison](analysis/deep-answer/comparisons/network-model.md) and [deployment status comparison](analysis/deep-answer/comparisons/deployment-status.md).

### Why institutions consider shared/public infrastructure

The evidence points to programmability, synchronized shared state, atomic settlement, broader connectivity, asset mobility, and longer settlement windows as possible benefits. These are not exclusive to permissionless public chains, and they come with governance, privacy, and operational trade-offs. See [institutional motivation research](analysis/deep-answer/institutional-motivation.md).

### Transaction privacy and auditor access

- Ethereum's base layer is transparent; privacy comes from application/protocol-specific tools.
- Canton distributes stakeholder-specific views and supports application-level permissions.
- Corda's transaction privacy and notary disclosures depend on protocol choices and product version.
- Rayls Enygma Public documents shielded notes, encrypted notes, nullifiers, commitments, and a deployment auditor. The documented auditor mechanism is not yet independently tested through this researcher's own transaction.

See [transaction privacy comparison](analysis/deep-answer/comparisons/transaction-privacy.md) and [auditor access comparison](analysis/deep-answer/comparisons/auditor-access.md).

## Rayls Enygma forensic investigation

The separate forensic track examines historical transaction:

0x09edab2bb8914aea3c905608ea9fcd09c056a470a5e150df03e0b324eff525bb

- **Block:** 24,825,928
- **Timestamp:** 2026-11-21 09:40:42 UTC
- **Method:** transferV2
- **Destination:** SharedVaultProxy 0x9c5ad5e5ea5b5910e7fd1e1cc7b70ce0e4bf06c2

Batch 01 governance review is complete within scope: all 24 current OwnerMultisig proposal IDs were scanned, all ten direct SharedVaultProxy proposals were identified, and six role grants were mapped. Implementation 0xad966... is the best-supported reconstruction for the November 21 target date, not a direct historical storage-slot observation; historical RPC state was pruned and indirect/non-multisig paths remain outside the scan.

Unresolved transaction semantics include the historical verifier-key slot, token identity/denomination, the meaning of statement value 4416000000000000000, and ownership of the third output note. See the [forensic checkpoint](analysis/rayls-enygma/investigation-checkpoint-2026-11-28.md).

## Stage 3 — self-verification

The historical November 21 transaction must not be represented as the researcher's own newly submitted payment. The required user-run testnet transaction and its public evidence remain pending. See the [Stage 3 checklist](analysis/deep-answer/stage-3-self-verification.md).

## Evidence methodology

Classify each item as:
- **Verified fact / direct observation**
- **Official documentation claim**
- **Current source observation**
- **Reconstruction**
- **Inference**
- **Unknown / not verified**

Prefer primary sources, record retrieval date/version, preserve historical evidence, and do not generalize current source code to historical transactions without demonstrating applicability.

## Key navigation

- [Deep Answer research index](analysis/deep-answer/README.md)
- [Network model comparison](analysis/deep-answer/comparisons/network-model.md)
- [Deployment status comparison](analysis/deep-answer/comparisons/deployment-status.md)
- [Transaction privacy comparison](analysis/deep-answer/comparisons/transaction-privacy.md)
- [Auditor access comparison](analysis/deep-answer/comparisons/auditor-access.md)
- [Final comparison](analysis/deep-answer/comparisons/final-comparison.md)
- [Institutional motivation](analysis/deep-answer/institutional-motivation.md)
- [Stage 3 self-verification checklist](analysis/deep-answer/stage-3-self-verification.md)
- [Rayls forensic checkpoint](analysis/rayls-enygma/investigation-checkpoint-2026-11-28.md)

---

## Scope and limitations

This repository is a research record, not a security audit certification, legal opinion, or proof that a named financial institution has deployed a particular architecture. The final article must distinguish a public network from permissionless validator admission, a production base chain from a testnet application, official product claims from independent tests, and historical transaction evidence from a new self-verification payment.
