# Canton Network — auditor access

Status: official documentation and user-terminal snapshots inspected. Canton documents selective auditor access through two distinct mechanisms; neither is an automatic network-wide auditor.

## 1. Daml contract observer

The official privacy-model source says specific parties can be added as observers when they need visibility but not control of the observed contract. It explicitly gives compliance, audit, and information purposes as use cases, including a regulator-as-observer example.

Documented patterns include:
- Add an explicit auditor party as an observer to selected contracts.
- Use non-consuming audit choices that return audit information.
- Create separate audit-trail contracts where full visibility is unnecessary.
- Use workflow patterns for time-bounded access.

Observer rights are contract-scoped. A party may have different roles on other contracts, so do not generalize “observer” into a universal statement about every right that party has in the application.

## 2. Observing Participant Node (OPN)

The OPN documentation states that a party can entrust an observing participant node to faithfully record and provide read access to transactions involving that party. A node with only Observation permission cannot submit or confirm transactions on behalf of the parties it hosts.

The topology documentation states:
- Observation permission notifies the participant only of transactions in which the hosted party is a stakeholder.
- Confirmation includes Observation.
- Submission includes Confirmation.

An OPN is therefore a party-scoped participant-node access arrangement, distinct from assigning a Daml contract observer.

## Evidence

1. [Privacy Model Explained — raw MDX source](https://raw.githubusercontent.com/canton-network/cf-docs/main/docs-main/overview/learn/privacy-model.mdx)
   - SHA-256: 6835dc9452f97f273fa33d39b449976401c09ee0b3b7c8dca04a5d3519bc72f1.
   - Lines 140–148 and 172–179 discuss observer disclosure and auditability practices.
2. [Local and external parties](https://docs.canton.network/overview/reference/external-party)
   - Codespace snapshot: HTTP 200; 297,586 bytes; SHA-256 18accaa70e6edba54de748899c9c1621dcbe6b598b671ef6e54ec92f17179020.
3. [Topology](https://docs.canton.network/overview/reference/topology)
   - Codespace snapshot: HTTP 200; 344,748 bytes; SHA-256 751d0d31a8be00aa92105c759eeae0f5b0d18f5d1eca4f7ac72a3effc556b86e.
4. [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model)

## Classification and limits

- **Official documentation claim:** Canton supports selective contract-level audit visibility by adding a regulator/auditor as an observer.
- **Official documentation claim:** OPN Observation permission is scoped to transactions involving the hosted party and does not grant submit/confirm permission by itself.
- **Not established:** an automatic network-wide auditor that sees every transaction.
- **Not established:** proof that a named financial institution deployed a specific configuration in production.
- The OPN's read scope depends on the parties it hosts and the topology permissions granted.

## Institutional relevance

Canton offers two levels of selective disclosure: contract-level observers and participant-node observation for a hosted party. Institutions can design audit access around specific contracts or parties rather than exposing every network transaction to one global auditor.
