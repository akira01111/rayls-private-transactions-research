# Canton Network — transaction privacy

Status: official documentation and user-terminal snapshots inspected. The description below is the documented Canton privacy model, not a test of every Canton application deployment.

## Sub-transaction privacy

Canton describes a transaction as a set of stakeholder-specific views rather than a single payload that every network participant receives. Views are encrypted for entitled recipients and distributed to the relevant participants. Participants validate the views they are entitled to see.

The documented Daml visibility rules include:
- **Signatories** see the contract and its events.
- **Observers** see a contract when explicitly declared as observers.
- **Controllers** can exercise the choices assigned to them.
- A party sees actions in which it has a stake and the consequences of those actions.
- **Divulgence** can reveal related contract information to a party through transaction execution, even if it was not originally declared an observer.

The Synchronizer coordinates transaction processing. The inspected documentation says it sees encrypted messages and confirmation results rather than the plaintext transaction views. It should not be described as seeing nothing: it participates in ordering/confirmation and can process network-level metadata.

## What remains visible or trusted

Canton does not remove the need for trust in the application and network infrastructure:
- Applications define signatories, observers, controllers, and the contracts/choices in which parties participate.
- Divulgence can expand visibility beyond an initial observer list.
- Synchronizer operators coordinate the shared transaction process; the privacy model depends on the documented encryption and participant topology.

## Evidence

1. [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model)
   - Codespace retrieval: HTTP 200; 339,780 bytes.
   - SHA-256: 3ea9c653a2289a8b6b06b37fab46356f4c9a70f5ef20ce4e6a7234ff5e80af4e.
   - Local snapshot: /tmp/deep-answer-transaction-privacy/canton_privacy.html.
2. [Privacy Model Explained — raw MDX source](https://raw.githubusercontent.com/canton-network/cf-docs/main/docs-main/overview/learn/privacy-model.mdx)
   - SHA-256: 6835dc9452f97f273fa33d39b449976401c09ee0b3b7c8dca04a5d3519bc72f1.
   - Local snapshot: /tmp/deep-answer-auditor/canton_privacy.mdx.
   - Lines 140–148 discuss observer disclosure for compliance/audit; lines 172–179 describe auditability practices.
3. [Participant Node Architecture](https://docs.canton.network/overview/reference/participant-overview)
   - Codespace snapshot SHA-256: fd4a3a50fda68df83e22eca3a8d26dae768794dd808621135f04ac419ad1c47c.

## Evidence classification and limits

- **Official documentation claim:** stakeholder-specific views are encrypted and distributed to entitled participants.
- **Official documentation claim:** visibility is role/contract scoped; divulgence can reveal related contract information.
- **Not independently tested:** this research did not run a production Canton participant or validate the encryption/disclosure protocol in a live deployment.
- The raw MDX snapshot contained component placeholders; only claims present in the extracted text were used.
- The amount of metadata visible to synchronizer infrastructure must not be overstated or understated beyond the documentation inspected.

## Institutional relevance

Canton demonstrates how interoperable infrastructure can share transaction coordination while keeping contract content restricted to relevant parties. Its privacy boundary is stakeholder and application based, not a guarantee that the entire network or every synchronizer component is invisible to all metadata.
