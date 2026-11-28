# Deep Answer — auditor access comparison

Status: documented access mechanisms compared. No named production deployment or independent Rayls auditor decryption test is established by this evidence pack.

| Project | Documented auditor/disclosure mechanism | Access scope | Authority boundary | Main limitation |
|---|---|---|---|---|
| Ethereum | Public ledger read access; application-level viewing keys and privacy-pool compliance proofs | Public data is readable by anyone. A user may share a viewing key or generate selected proofs for a chosen third party. | A viewing key is distinct from a spending key in ERC-5564. There is no Ethereum base-layer auditor-only role. | Selective disclosure is application/protocol-specific; ordinary public read access is not a private auditor permission. |
| Canton | Daml contract observer; Observing Participant Node (OPN) with Observation permission | Contract observer sees selected contract information. OPN reads transactions involving the party hosted by that participant. | An OPN with only Observation cannot submit or confirm for the hosted party. Contract observer rights are contract-scoped; OPN is party/participant-scoped. | These are different mechanisms; no automatic network-wide auditor is documented. |
| R3 Corda | Regulator observer node receiving signed transaction reports through explicit CorDapp flows | The application sends selected transaction/state data to the observer node; the Enterprise 4.10 example records states with ALL_VISIBLE. | Reporting is controlled by the application flow and observer-node deployment. | Not automatic for every Corda application; example is Enterprise 4.10, not Corda 5.2. |
| Rayls Enygma Public | Deployment auditor key; account view-key copy encrypted to the auditor key using ML-KEM-768 and stored in the registry | Official documentation says the deployment auditor can read shielded transaction details for registered accounts in that deployment. | View key provides read/decrypt capability; spend key is separate and required to move funds. | Official product claim only in this research; successful auditor decryption has not been independently tested. |

## Key distinctions

- **Ethereum:** public transparency may satisfy a third party's need to inspect public data, but it does not selectively reveal hidden application data unless the application provides a viewing key or proof.
- **Canton:** a Daml observer is added to specific contracts; an OPN receives a party-scoped transaction feed. Do not conflate contract-level observer rights with Participant Node topology permissions.
- **Corda:** regulator reporting is application-integrated. A CorDapp explicitly sends signed transaction reports to the regulator observer node.
- **Rayls:** auditor access is deployment-level and based on view-key disclosure. It is explicitly separate from spend authority, but relies on auditor key custody and registry configuration.

## Evidence sources

- Ethereum: [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/), [ERC-5564](https://eips.ethereum.org/EIPS/eip-5564).
- Canton: [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model), [External parties](https://docs.canton.network/overview/reference/external-party), [Topology](https://docs.canton.network/overview/reference/topology).
- Corda: [Observer nodes — Corda Enterprise 4.10](https://docs.r3.com/en/platform/corda/4.10/enterprise/get-started/tutorials/supplementary-tutorials/tutorial-observer-nodes.html).
- Rayls: [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what), [Enygma Public](https://docs.rayls.com/docs/enygma-public).

## Evidence boundary

This table compares mechanisms described in official documentation or standards. It does not prove that a named bank, regulator, or live production deployment uses the configuration shown. Rayls auditor decryption remains untested in this research.
