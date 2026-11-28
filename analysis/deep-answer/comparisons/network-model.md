# Deep Answer — network model comparison

Status: cross-project synthesis of current official network documentation, retrieved 2026-11-28.

| Project | Base/network model | Admission and participation | Application/data boundary |
|---|---|---|---|
| Ethereum | Public Proof-of-Stake L1 | Public read/transaction access; direct validators deposit 32 ETH and operate validator infrastructure | Mainnet base ledger is publicly visible; application privacy must be added separately. Sepolia uses a permissioned validator set. |
| Canton | Public network of interoperable applications, with a decentralized Global Synchronizer | Validator nodes may be requested, but sponsorship is currently needed; Global Synchronizer operated by Super Validators with 2/3 BFT ordering/confirmation | Permissioning is configured application by application; participants receive party/contract-scoped views. |
| R3 Corda 5.2 | Permissioned application networks | MGM membership registration; operator decides who joins; KYC/due diligence may be applied | Peer-to-peer flows distribute transaction data to relevant counterparties; notary model adds protocol-specific trust/disclosure trade-offs. |
| Rayls | Public EVM-compatible Public Chain plus separate permissioned Private Network/Sovereign environments | Public Chain validator admission is currently described as a permissioned Foundation-led set with partner onboarding; future permissionless approval is a roadmap | Enygma Public is an open-to-users smart-contract privacy pilot on testnet; Enygma Sovereign is a separate institutional private-network edition. |

## Key distinctions

1. **Public network does not always mean permissionless validator admission.** Canton currently requires sponsorship for validator onboarding; Rayls documents a permissioned validator set on its Public Chain while describing an open public application layer.
2. **Permissioning can exist above a public network.** Canton applications set their own participation rules. Enygma Public lets users interact with shielded contracts, but an application-specific auditor and registry are part of its model.
3. **Corda's permissioning is membership-based.** Corda 5.2 application network members register with an MGM before transacting.
4. **Ethereum Mainnet and Sepolia differ.** Do not use Sepolia's permissioned validator configuration to describe Mainnet.

## Sources

- [Ethereum Networks](https://ethereum.org/developers/docs/networks/)
- [Canton FAQ](https://www.canton.network/faq)
- [Global Synchronizer overview](https://docs.global.canton.network.sync.global/overview/overview.html)
- [Corda 5.2 — Planning Application Networks](https://docs.r3.com/en/platform/corda/5.2/application-networks/plan.html)
- [Corda 5.2 — Developing Applications](https://docs.r3.com/en/platform/corda/5.2/developing-applications.html)
- [Rayls high-level architecture](https://docs.rayls.com/docs/rayls-high-level-architecture)
- [Rayls Public Chain validator onboarding](https://docs.rayls.com/docs/running-a-rayls-public-chain-validator)

## Limitations

This comparison is about documented base-network and application participation models. It does not assert that all application deployments use the same settings, or that each validator set is permissionless.
