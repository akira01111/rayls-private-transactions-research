# Canton Network — network model

Status: preliminary; complete classification remains open.

## Current evidence

- Current Canton documentation describes Canton as a public Layer 1 network.
- Parties are hosted on Participant Nodes.
- Party-to-participant hosting relationships carry distinct permissions: Observation, Confirmation, and Submission.
- Synchronizers coordinate transaction processing, while participants maintain party-specific/private contract views.

## Evidence

1. [What is Canton Network?](https://docs.canton.network/overview/understand/what-is-canton)
2. [Topology](https://docs.canton.network/overview/reference/topology)
   - Codespace retrieval: HTTP 200; 344,748 bytes.
   - SHA-256: 751d0d31a8be00aa92105c759eeae0f5b0d18f5d1eca4f7ac72a3effc556b86e.
   - Local snapshot: /tmp/deep-answer-auditor/canton_topology_v2.html
3. [Participant Node Architecture](https://docs.canton.network/overview/reference/participant-overview)
   - Codespace retrieval: HTTP 200; 215,117 bytes.
   - SHA-256: fd4a3a50fda68df83e22eca3a8d26dae768794dd808621135f04ac419ad1c47c.

## Classification

- Official documentation claim: public Layer 1 positioning.
- Official documentation claim: party-specific hosting and permissions are managed through topology.
- Interpretation still pending: how best to characterize network-wide access versus application-level permissioning in the comparison table.

## Still to verify

- Do not mechanically call the whole Canton network “public permissioned” without explaining the distinction between the public network layer and application/party-level permissions.
- Determine which precise network-layer claims are appropriate for this quest's comparison criteria.