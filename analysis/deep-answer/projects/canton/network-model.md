# Canton Network — network model

Status: network-layer and application-layer distinctions reviewed against current Canton Network, Canton Foundation, and Global Synchronizer documentation.

## Network model

### Public network, configurable applications
- Canton describes itself as a public network. Its FAQ says anyone can request a validator node, although sponsorship is currently required; a validator participates in consensus related to transactions in which it is a party.
- Permissioning is defined per application. An application provider can make an application permissioned or permissionless while it operates over the broader Canton network.
- This is not equivalent to saying that every party, contract, application, or validator has unrestricted access to all network data.

### Network of networks and synchronization
- Parties are hosted on Participant Nodes. Participants maintain the data and contract views to which their parties are entitled.
- Synchronizers coordinate transaction sequencing and confirmation. The Global Synchronizer is documented as a decentralized interoperability service.
- The Global Synchronizer documentation describes a 2/3-majority Byzantine Fault Tolerant consensus protocol for message ordering and confirmation, with Super Validators operating the decentralized infrastructure and participating in governance.
- Applications may use a shared decentralized synchronizer or a different synchronizer arrangement according to their own trust, scalability, and metadata-disclosure requirements.

## Evidence
1. [Canton Network FAQ](https://www.canton.network/faq) — retrieved 2026-11-28; public-network positioning, sponsorship for validators, and application-level permissioning.
2. [Global Synchronizer overview](https://docs.global.canton.network.sync.global/overview/overview.html) — decentralized synchronizer, Super Validator operating model, and 2/3 BFT consensus.
3. [Canton Foundation — SV Network Status](https://canton.foundation/sv-network-status-2/) — separate DevNet, TestNet, and MainNet status areas and MainNet Super Validator information.
4. [Canton Foundation — Validators](https://canton.foundation/validators/) — validator onboarding and approved Node-as-a-Service options.

## Classification and limits
- **Official documentation claims:** public-network positioning; sponsored validator onboarding; application-level permissioning; participant/synchronizer roles; Global Synchronizer BFT operation.
- **Current operational evidence:** the Canton Foundation publishes a MainNet status and Super Validator node information page. Dynamic fields may change.
- **Interpretation:** Canton is best described as a public network of interoperable applications with configurable, often permissioned application access—not as a fully permissionless application environment.
- Do not conflate Daml contract observers with Participant Node Observation permission; they are distinct access mechanisms documented in [auditor access](auditor-access.md).
- Do not infer that a public network means every application is permissionless or every participant sees the same transaction data.

## Institutional relevance
Canton separates shared synchronization/interoperability from application-specific control over parties and data. This is relevant to institutions seeking interoperability without making every application's transaction data public. See [deployment status](deployment-status.md).

## Evidence snapshot metadata retained from Codespaces retrieval

### Topology
- Retrieval: user-run Bash `curl` in GitHub Codespaces; 2026-11-28; HTTP 200; 344,748 bytes.
- SHA-256: `751d0d31a8be00aa92105c759eeae0f5b0d18f5d1eca4f7ac72a3effc556b86e`.
- Local snapshot: `/tmp/deep-answer-auditor/canton_topology_v2.html`.

### Participant Node Architecture
- Retrieval: user-run Bash `curl` in GitHub Codespaces; 2026-11-28; HTTP 200; 215,117 bytes.
- SHA-256: `fd4a3a50fda68df83e22eca3a8d26dae768794dd808621135f04ac419ad1c47c`.
