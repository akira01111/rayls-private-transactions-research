# Deep Answer — auditor access comparison

Status: documented capabilities compared; specific production deployments not independently tested.

| Project | Documented access model | Scope / boundary | Key limitation |
|---|---|---|---|
| Ethereum | Public read access; privacy applications may use selective disclosure or viewing keys | Public base-layer data is visible to anyone; application-specific disclosure can be selective | No auditor-only role at Ethereum base layer established by the reviewed sources |
| Canton | Daml contract observers and Participant Node Observation permission | Contract observers see selected contracts; OPNs read transactions involving their hosted party | No automatic network-wide auditor |
| R3 Corda | Application-integrated observer node and explicit regulator reporting flows | Transactions/states distributed to the regulator through CorDapp flows; example records ALL_VISIBLE | Not automatic reporting by every application |
| Rayls Enygma Public | Deployment auditor key and escrowed account view keys | Auditor can read shielded transactions within the deployment | Official product claim; no independent testnet decryption performed |

## Critical distinctions

- Ethereum transparency is not a dedicated auditor permission.
- Canton Daml contract observer rights are not the same as OPN hosting Observation permission.
- Corda observer nodes depend on explicit application-flow distribution.
- Rayls documents a deployment-scoped auditor key with read/decrypt capability separate from spend authority.

## Evidence sources

- Ethereum: [Networks](https://ethereum.org/developers/docs/networks/), [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/)
- Canton: [External parties](https://docs.canton.network/overview/reference/external-party), [Topology](https://docs.canton.network/overview/reference/topology), [Privacy model](https://docs.canton.network/overview/learn/privacy-model), [Raw privacy-model MDX](https://raw.githubusercontent.com/canton-network/cf-docs/main/docs-main/overview/learn/privacy-model.mdx)
- Corda: [Observer nodes — Enterprise 4.10](https://docs.r3.com/en/platform/corda/4.10/enterprise/get-started/tutorials/supplementary-tutorials/tutorial-observer-nodes.html)
- Rayls: [Who sees what](https://docs.rayls.com/docs/enygma-public-who-sees-what), [Enygma Public](https://docs.rayls.com/docs/enygma-public)

## Evidence boundary

This table compares capabilities described by official documentation. It does not establish the configuration of a named bank, regulator, or live production network.