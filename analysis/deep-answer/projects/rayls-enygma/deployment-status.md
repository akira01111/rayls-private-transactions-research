# Rayls Enygma Public — deployment status

Status: the underlying Rayls Public Chain Mainnet is live, but **Enygma Public itself remains a testnet pilot** as of the official product documentation reviewed on 2026-11-28.

## Separate the chain from the application

| Layer / product | Documented status | What can safely be said |
|---|---|---|
| Rayls Public Chain | Mainnet launched 2026-04-30 | The underlying public EVM-compatible L1 has a production Mainnet. |
| Rayls Public Chain Testnet | Live test environment | Enygma Public's current pilot runs here; test tokens have no value. |
| Enygma Public | Testnet pilot | The public shielded-payment application is not live on Mainnet. Testnet chain ID: 7295799. |
| Enygma Sovereign | Described by Rayls as in production with banks | A distinct institutional product that runs with Rayls Sovereign chains/Private Networks; do not conflate it with Enygma Public. |

## Validator admission is a separate dimension

Rayls' dedicated validator documentation says the Public Chain launched with all validators under Rayls Foundation control. External partners are invited into a permissioned validator set; the page describes a future move toward permissionless approvals and a DAO role as a roadmap. Therefore, the Public Chain's public-facing user/application layer should not be used to claim that validator admission is already permissionless.

## Evidence
1. [Rayls Public Chain Mainnet launch announcement](https://www.rayls.com/blog/rayls-public-chain-mainnet-launches) — 2026-04-30 launch date and transition to production.
2. [Rayls Public Chain reference](https://docs.rayls.com/docs/public-chain-reference) — Mainnet and testnet chain IDs and endpoints.
3. [How to Run a Rayls Public Chain Validator](https://docs.rayls.com/docs/running-a-rayls-public-chain-validator) — validator control/admission status and roadmap.
4. [Enygma Public product page](https://www.rayls.com/products/enygma-public) — explicitly says Enygma Public is not live on Mainnet and the pilot runs on Testnet.
5. [Try Enygma Public on testnet](https://docs.rayls.com/docs/try-enygma-public-on-testnet) — wallet, registration, shield/send/unshield flow, testnet details.
6. [Enygma Sovereign](https://docs.rayls.com/docs/a-warm-introduction-to-rayls-enygma) — separate institutional edition and its architecture.

## Interpretation limits
- Mainnet availability for Rayls Public Chain is not Mainnet availability for Enygma Public.
- Enygma Sovereign's production claims do not establish Enygma Public production deployment.
- Testnet activity and test tokens do not establish real-value production adoption.
