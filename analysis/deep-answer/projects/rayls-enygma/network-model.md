# Rayls Enygma Public — network model

Status: reviewed against Rayls' current official architecture, public-chain validator, and Enygma Public testnet documentation. The key distinction is between the Public Chain's user-facing openness, its validator admission model, and the separate deployment status of Enygma Public.

## Network model

### Rayls Public Chain
- Rayls describes the Public Chain as an EVM-compatible Layer 1 and a public layer for assets, applications, and liquidity.
- The Public Chain Mainnet launched on 2026-04-30.
- The dedicated validator onboarding documentation says the initial validator set was controlled by the Rayls Foundation and that external partners are being invited into a **permissioned validator set**. The documented future path toward automatic permissionless validator approval is a roadmap item, not the current admission rule described on that page.
- Public-chain access for users and applications must not be conflated with permissionless validator admission.

### Enygma Public
- Enygma Public runs as smart contracts on the Rayls Public Chain; cryptographic proof generation runs in the user's browser.
- It does not require a Rayls Sovereign ledger or a Rayls Private Network.
- Its testnet pilot is open to users with test tokens. The documented testnet chain ID is 7295799.
- The deployment has a deployment-level auditor. The testnet documentation identifies Rayls as the auditor.

### Keep Enygma Sovereign separate
Enygma Sovereign is a distinct institutional edition that operates within Rayls Private Networks and is described by Rayls as being in production with banks. It must not be used as evidence that Enygma Public itself is live on Mainnet.

## Evidence
1. [Rayls high-level architecture](https://docs.rayls.com/docs/rayls-high-level-architecture) — distinguishes Rayls Public Chain, Rayls Private Networks, Enygma Sovereign, and Enygma Public.
2. [How to Run a Rayls Public Chain Validator](https://docs.rayls.com/docs/running-a-rayls-public-chain-validator) — validators initially under Rayls Foundation control and permissioned external-partner onboarding.
3. [Enygma Public](https://docs.rayls.com/docs/enygma-public) — Enygma Public is live on the Rayls Public Chain testnet and runs with test tokens.
4. [Try Enygma Public on testnet](https://docs.rayls.com/docs/try-enygma-public-on-testnet) — user flow and testnet details, including chain ID 7295799.
5. [Rayls Public Chain Mainnet launch announcement](https://www.rayls.com/blog/rayls-public-chain-mainnet-launches) — Mainnet launch date 2026-04-30.
6. [Enygma Public product status](https://www.rayls.com/products/enygma-public) — explicitly states Enygma Public is not live on Mainnet and the pilot runs on the Rayls Public Chain Testnet.

## Classification and limits
- **Official product claim:** Rayls Public Chain Mainnet launched on 2026-04-30.
- **Official validator-model claim:** initial Public Chain validators were Foundation-controlled, with external validators joining a permissioned set under an onboarding process.
- **Official Enygma Public status:** testnet pilot only; test tokens have no value.
- **Official Enygma Sovereign status:** described by Rayls as in production with banks. This is a different product edition and is not evidence of Enygma Public production deployment.
- Do not describe Enygma Public as a Mainnet application merely because the underlying Rayls Public Chain has a Mainnet.
- Do not describe the current validator set as fully permissionless based solely on the Public Chain's public-facing positioning.

## Institutional relevance
Rayls demonstrates a hybrid boundary: a public-chain settlement layer, an institution-oriented private-network architecture, and a privacy application currently in a public testnet pilot. Enygma Public's deployment status must remain explicit in every comparison and article. See [deployment status](deployment-status.md).

## Evidence snapshot metadata retained from Codespaces retrieval

Source: [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what)
- Retrieval method: user-run Bash `curl` in GitHub Codespaces.
- Retrieval date: 2026-11-28; HTTP 200; downloaded size: 196,863 bytes.
- SHA-256: `17704cffaf946d917d32ec35d77b6b2c00acf2aa368b835903ca6aff9e04c0d2`.
- Local snapshots: `/tmp/deep-answer-auditor/rayls.html` and `/tmp/deep-answer-transaction-privacy/rayls_who_sees_what.html`.
- This snapshot supports the documented visibility matrix, but does not prove actual successful auditor decryption for a particular account or historical transaction.
