# Deep Answer — deployment status comparison

Status: primary-source status review completed for the four comparator subjects, with product/version and application/base-chain boundaries retained.

| Project | Base network status | Status of the subject/application compared here | Safe comparison label |
|---|---|---|---|
| Ethereum | Ethereum Mainnet is a live public production blockchain. | Ethereum privacy is an ecosystem of applications/protocols; each one's deployment must be assessed separately. Visa announced a specific USDC settlement pilot over Ethereum in 2021 and lists Ethereum among chains supported by its 2026 multi-chain settlement pilot. | **Production base network; application-specific privacy/deployment status.** |
| Canton | MainNet is the production environment; Canton Foundation publishes MainNet SV/network status. | Canton FAQ names institutional applications such as Goldman Sachs DAP, Broadridge DLR, and Versana; individual application launch scope should be sourced separately. | **Production network; application-specific permissions/deployments.** |
| R3 Corda 5.2 | Corda 5.2 supports dynamic application networks for production; Corda Enterprise 4.10 is a commercial edition. | Reviewed sources establish production-capable architecture and an Enterprise 4.10 regulator observer-node tutorial, not a specific named live Corda 5.2 deployment. | **Production-capable permissioned platform; named deployment not verified in this evidence pack.** |
| Rayls Enygma Public | Rayls Public Chain Mainnet launched 2026-04-30; validator admission remains permissioned under the documented onboarding model. | Enygma Public itself is a testnet pilot using no-value test tokens (testnet chain ID 7295799). Enygma Sovereign is a separate edition described as in production with banks. | **Public-chain Mainnet live; Enygma Public testnet pilot. Do not conflate with Enygma Sovereign.** |

## Interpretation rules

- A production base chain does not automatically make every application on it a production deployment.
- Product capability to deploy in production is not proof that a named network has launched.
- A testnet pilot can demonstrate flows and technical behavior but does not prove production readiness, real-value usage, or commercial adoption.
- Institutional examples should be dated and described at the scope stated by the primary source. Do not imply that all partner activity uses the same blockchain or that a pilot is a general production rollout.

## Sources

- Ethereum: [Ethereum Networks](https://ethereum.org/developers/docs/networks/); [Visa 2021 Ethereum settlement pilot](https://usa.visa.com/about-visa/newsroom/press-releases.releaseld.17821.html); [Visa 2026 multi-chain settlement pilot](https://corporate.visa.com/en/sites/visa-perspectives/newsroom/visa-expands-stablecoin-settlement-adds-five-blockchains.html).
- Canton: [SV Network Status](https://canton.foundation/sv-network-status-2/); [SV-operated networks and use-cases](https://docs.global.canton.network.sync.global/app_dev/testing/networks_and_usecases.html); [Canton FAQ](https://www.canton.network/faq).
- Corda: [Corda 5.2 Developing Applications](https://docs.r3.com/en/platform/corda/5.2/developing-applications.html); [Corda Enterprise 4.10](https://docs.r3.com/en/platform/corda/4.10/enterprise.html); [Enterprise 4.10 observer nodes](https://docs.r3.com/en/platform/corda/4.10/enterprise/get-started/tutorials/supplementary-tutorials/tutorial-observer-nodes.html).
- Rayls: [Public Chain Mainnet launch](https://www.rayls.com/blog/rayls-public-chain-mainnet-launches); [validator onboarding](https://docs.rayls.com/docs/running-a-rayls-public-chain-validator); [Enygma Public product status](https://www.rayls.com/products/enygma-public); [Enygma Public testnet guide](https://docs.rayls.com/docs/try-enygma-public-on-testnet).

## Open boundary

This file records published network/product status as of 2026-11-28. It does not independently audit any named institution's use of an application or its exact production configuration.
