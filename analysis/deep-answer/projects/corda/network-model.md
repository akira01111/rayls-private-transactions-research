# R3 Corda — network model

Status: reviewed for Corda 5.2 application-network architecture. Corda Enterprise 4.10 is retained only for the separately documented observer-node example; the versions are not merged.

## Network model

### Permissioned application networks
- Corda 5.2 describes application networks as membership groups in which members register before transacting.
- The Membership Group Manager (MGM) acts as the central registrar for a dynamic application network. Network operators decide which identities can join; the required due diligence can vary and may include KYC.
- Corda 5.2 documentation explicitly classifies Corda as a permissioned network in its application-network planning guidance.

### Static and dynamic networks
- Static networks are intended for local testing with predetermined virtual nodes or members and no MGM distributing member data across clusters.
- Dynamic networks have a running MGM and are documented as being used for production networks as well as multi-cluster testing.
- Participant communication is peer-to-peer through Corda flows. A notary provides uniqueness consensus to prevent double-spends; notary privacy depends on the selected protocol.

## Evidence
1. [Planning Application Networks — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/application-networks/plan.html) — explicitly describes Corda as permissioned and assigns membership decisions to the Network Operator.
2. [Creating Application Networks — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/application-networks/creating.html) — MGM and member onboarding.
3. [Developing Applications — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications.html) — static networks for local testing; dynamic networks for production and multi-cluster testing.
4. [Notary Protocols — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/notary-protocols.html) — non-validating and contract-verifying notary protocols.

## Classification and limits
- **Official documentation claims:** permissioned membership, MGM registration, static/dynamic network purposes, peer-to-peer flows, and notary roles.
- **Interpretation:** Corda 5.2 application networks are permissioned environments, not open public ledgers.
- Production-capable architecture does not, by itself, prove that a particular named Corda 5.2 network is currently live.
- Corda Enterprise 4.10 and Corda 5.2 are separate version/edition scopes. The regulator observer-node example in the auditor-access file refers to Enterprise 4.10 and must not be described as a Corda 5.2 deployment.
- Do not imply that all admitted members can read every network transaction. Visibility depends on transaction participation and application flows.

## Institutional relevance
Corda is a comparator for a permissioned, membership-governed DLT model. It demonstrates how institutions can control participation and use peer-to-peer transaction distribution, with corresponding interoperability and network-boundary trade-offs. See [deployment status](deployment-status.md).
