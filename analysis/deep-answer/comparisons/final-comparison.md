# Deep Answer — final comparison

Status: **in progress; not ready for final article sign-off**. Network-model and deployment-status reviews have been harmonized on 2026-11-28. Transaction-privacy and auditor-access evidence still needs final claim-by-claim synthesis and a clear relevance assessment.

## Required dimensions from the quest brief

- Network model
- Transaction privacy
- Auditor access
- Deployment status
- Relevance to the research question

## Current state

| Dimension | State | Remaining work |
|---|---|---|
| Network model | Reviewed and harmonized | Preserve network-layer vs application-layer permissioning distinctions in final prose. |
| Transaction privacy | Preliminary comparison exists | Verify claims against the cited versions and identify what remains visible/trusted in each system. |
| Auditor access | Preliminary comparison exists | Keep Canton observer vs OPN distinct; Corda Enterprise 4.10 vs Corda 5.2 distinct; Rayls auditor access remains an official claim pending independent test. |
| Deployment status | Reviewed and harmonized | Do not conflate Rayls Public Chain Mainnet with Enygma Public testnet; do not infer a named Corda 5.2 live deployment from production capability alone. |
| Relevance | Synthesis pending | Explain what each comparator contributes to the main question and where each model falls short. |

## Core comparison at a glance

| Project | Network model | Deployment boundary | What it contributes |
|---|---|---|---|
| Ethereum | Public Proof-of-Stake L1 | Mainnet production; application privacy varies | Baseline for open settlement and transparent base-layer verification. |
| Canton | Public network with app-level permissioning and decentralized synchronization | MainNet production; application deployments vary | Shows privacy and interoperability across institution-controlled applications. |
| R3 Corda 5.2 | Permissioned application networks with MGM membership | Production-capable dynamic-network design; named live Corda 5.2 deployment not verified in this evidence pack | Shows strong membership control and peer-to-peer disclosure rather than a public ledger. |
| Rayls Enygma Public | Public-chain privacy application; validator admission on Rayls Public Chain currently permissioned | Rayls Public Chain Mainnet live; Enygma Public still testnet pilot | Main case for shielding payment data while preserving public verification and deployment-level auditor access. |

## Rule

Do not mark the final comparison complete until every claim in every row has a primary source, an evidence class, and a scope/version boundary. Stage 3 must also remain separate: the historical 2026-11-21 transaction is not the user's required personally submitted payment.
