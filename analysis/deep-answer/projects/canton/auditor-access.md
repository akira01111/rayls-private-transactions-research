# Canton Network — auditor access

Status: official documentation and user-terminal snapshots inspected.

## Two distinct mechanisms

### 1. Daml contract observer

The official privacy-model source says specific parties can be added as observers when they need visibility but not control. It explicitly gives compliance, audit, and information purposes as use cases, with a regulator as an observer in its example.

The source also recommends:
- Explicit auditor parties as observers.
- Non-consuming audit choices that return audit information.
- Separate audit-trail contracts when full visibility is unnecessary.
- Time-bounded access through workflow patterns.

Raw MDX evidence:
- URL: https://raw.githubusercontent.com/canton-network/cf-docs/main/docs-main/overview/learn/privacy-model.mdx
- SHA-256: 6835dc9452f97f273fa33d39b449976401c09ee0b3b7c8dca04a5d3519bc72f1
- Lines 140–148 and 172–179.

### 2. Observing Participant Node (OPN)

The OPN documentation states that a party entrusts its OPNs to faithfully record and provide read access to transactions involving that party. Nodes with only Observation permission cannot submit or confirm transactions on behalf of the parties they host.

The current topology documentation states that Observation permission means the participant node is notified only of transactions in which the hosted party is a stakeholder. Confirmation includes Observation; Submission includes Confirmation.

Sources:
- [Local and external parties](https://docs.canton.network/overview/reference/external-party)
- [Topology](https://docs.canton.network/overview/reference/topology)
- [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model)

Terminal evidence:
- External party page: HTTP 200, 297,586 bytes; SHA-256 18accaa70e6edba54de748899c9c1621dcbe6b598b671ef6e54ec92f17179020.
- Topology page: HTTP 200, 344,748 bytes; SHA-256 751d0d31a8be00aa92105c759eeae0f5b0d18f5d1eca4f7ac72a3effc556b86e.
- Privacy page raw MDX: 9,347 bytes; SHA-256 6835dc9452f97f273fa33d39b449976401c09ee0b3b7c8dca04a5d3519bc72f1.

## Important distinction

Daml contract observer rights and Participant Node Observation permission are related but different:

- Contract observer: sees a particular contract instance and its information under Daml visibility rules.
- OPN: a participant node entrusted by a party to record and read transactions involving the hosted party.

## Classification and limits

- Official documentation claim: Canton supports selective audit visibility by adding a regulator/auditor as an observer.
- Official documentation claim: OPN read access is scoped to transactions involving the hosted party.
- Not established: an automatic network-wide auditor that sees every transaction.
- Not established: proof that a named financial institution has deployed this design in production.
- Caution: an example's owner party is also a controller for Transfer; do not generalize that every observer lacks all control rights.