# Deep Answer research records

Research question: **How can financial institutions make private transactions on a public blockchain?**

This directory stores the Deep Answer Quest evidence in project-specific files. Project evidence is kept separate from cross-project comparisons so each claim can be reviewed without navigating one oversized record.

## Project evidence

| Project | Network model | Transaction privacy | Auditor access |
|---|---|---|---|
| [Ethereum](projects/ethereum/README.md) | Preliminary | Evidence reviewed | Evidence reviewed |
| [Canton Network](projects/canton/README.md) | Preliminary | Evidence reviewed | Evidence reviewed |
| [R3 Corda](projects/corda/README.md) | Preliminary | Corda 5.2 documentation reviewed | Enterprise 4.10 documentation reviewed |
| [Rayls Enygma Public](projects/rayls-enygma/README.md) | Preliminary | Evidence reviewed | Evidence reviewed |

## Cross-project comparisons

- [Auditor access comparison](comparisons/auditor-access.md)
- [Transaction privacy comparison](comparisons/transaction-privacy.md)
- [Final comparison — work in progress](comparisons/final-comparison.md)

## Historical / combined evidence records

- [Auditor access comparison JSON — original combined evidence record](auditor-access-comparison-2026-11-28.json)

The JSON record is retained as a dated audit trail. The project-specific Markdown files are the working structure going forward. Do not delete the JSON record as part of normal cleanup.

## Research discipline

Every project file should distinguish:
- Official documentation claim
- Direct terminal observation / retrieved snapshot
- Independently reproduced behavior
- Inference
- Unknown / not verified

HTTP 200 and a SHA-256 hash identify a retrieved snapshot; they do not by themselves prove every semantic claim in that source.

Do not generalize one product version or deployment to another. In particular:
- Corda transaction privacy findings in the current files refer to Corda 5.2.
- Corda regulator observer-node example refers to Corda Enterprise 4.10.
- Canton Daml contract observers and Participant Node Observation permission are separate mechanisms.
- Rayls Enygma Public is a testnet pilot, and current product documentation does not automatically prove historical transaction behavior.

## Quest stages

1. **Stage 1 — Research scope:** the brief and five subquestions are established.
2. **Stage 2 — Comparator research:** in progress. Evidence exists for auditor access and transaction privacy; network-model and deployment-status comparisons remain to be harmonized.
3. **Stage 3 — Self-verification:** historical Enygma transaction investigation exists, but the brief's requirement to send one private payment personally must be checked separately before claiming it is complete.
