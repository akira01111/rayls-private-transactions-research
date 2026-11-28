# Deep Answer research records

Research question: **How can financial institutions make private transactions on a public blockchain?**

This directory stores the Deep Answer evidence in project-specific files and cross-project comparison records.

## Project evidence

| Project | Network model | Transaction privacy | Auditor access | Deployment status |
|---|---|---|---|---|
| [Ethereum](projects/ethereum/README.md) | Reviewed | Evidence reviewed | Evidence reviewed | [Reviewed](projects/ethereum/deployment-status.md) |
| [Canton Network](projects/canton/README.md) | Reviewed | Evidence reviewed | Evidence reviewed | [Reviewed](projects/canton/deployment-status.md) |
| [R3 Corda](projects/corda/README.md) | Reviewed (Corda 5.2) | Corda 5.2 documentation reviewed | Enterprise 4.10 documentation reviewed | [Reviewed with version boundary](projects/corda/deployment-status.md) |
| [Rayls Enygma Public](projects/rayls-enygma/README.md) | Reviewed | Evidence reviewed | Official mechanism documented; independent test pending | [Reviewed: Enygma Public is testnet pilot](projects/rayls-enygma/deployment-status.md) |

## Cross-project comparisons

- [Network model comparison](comparisons/network-model.md)
- [Transaction privacy comparison](comparisons/transaction-privacy.md)
- [Auditor access comparison](comparisons/auditor-access.md)
- [Deployment status comparison](comparisons/deployment-status.md)
- [Final comparison — work in progress](comparisons/final-comparison.md)

## Institutional motivation and Stage 3

- [Why financial institutions consider public blockchain infrastructure](institutional-motivation.md)
- [Stage 3 — Enygma Public self-verification checklist](stage-3-self-verification.md)

## Historical / combined evidence records

- [Auditor access comparison JSON — original combined evidence record](auditor-access-comparison-2026-11-28.json)

The JSON record is retained as a dated audit trail. Project-specific Markdown files are the working structure. Do not delete historical JSON records as part of normal cleanup.

## Research discipline

Every claim must be classified as one of:
- Official documentation claim
- Direct terminal observation / retrieved snapshot
- Independently reproduced behavior
- Reconstruction
- Inference
- Unknown / not verified

HTTP 200 and a SHA-256 hash identify a retrieved snapshot; they do not by themselves prove every semantic claim in that source. Do not generalize one product version or deployment to another.

## Quest stages

1. **Stage 1 — Research scope:** established.
2. **Stage 2 — Comparator research:** network-model and deployment-status reviews are now harmonized. Transaction-privacy and auditor-access comparisons still need final claim-level synthesis, and the final relevance matrix remains open.
3. **Stage 3 — Self-verification:** pending the user's own successful Enygma Public testnet private payment and inspection of its public evidence. The historical 2026-11-21 transfer does not satisfy this requirement.
