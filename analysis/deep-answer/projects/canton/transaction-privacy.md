# Canton Network — transaction privacy

Status: official documentation downloaded and relevant text inspected in the user's Codespace.

## Findings

Canton's documented model is sub-transaction privacy. A transaction is decomposed into views based on stakeholder relationships. Each view is encrypted for its entitled recipients and delivered to the relevant participants. Each participant validates the view it is entitled to see.

The inspected privacy-model text explains that:

- Parties see actions in which they have a stake.
- Signatories see the contract and its events.
- Observers see a contract by explicit declaration.
- Controllers see choices they can exercise.
- A party that sees an action also sees its consequences.
- The Synchronizer sees encrypted messages and confirmation results, not the transaction views' plaintext content.

Canton also documents divulgence: a party involved in a transaction may learn about a contract through transaction execution even if it was not originally an observer. This can cause unintended disclosure if application design does not account for it.

## Evidence

1. [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model)
   - Codespace retrieval: HTTP 200; 339,780 bytes.
   - SHA-256: 3ea9c653a2289a8b6b06b37fab46356f4c9a70f5ef20ce4e6a7234ff5e80af4e.
   - Local snapshot: /tmp/deep-answer-transaction-privacy/canton_privacy.html
   - Extracted content includes transaction decomposition, encryption, distribution, stakeholder visibility, and divulgence.

2. [Privacy Model Explained — raw MDX source](https://raw.githubusercontent.com/canton-network/cf-docs/main/docs-main/overview/learn/privacy-model.mdx)
   - SHA-256: 6835dc9452f97f273fa33d39b449976401c09ee0b3b7c8dca04a5d3519bc72f1.
   - Local snapshot: /tmp/deep-answer-auditor/canton_privacy.mdx.
   - Lines 140–148 document selective disclosure via observers for compliance, audit, or information purposes.
   - Lines 172–179 describe auditability best practices.

3. [Participant Node Architecture](https://docs.canton.network/overview/reference/participant-overview)
   - Participant stores data for Daml contracts whose signatories and observers are hosted on that participant.
   - Terminal SHA-256: fd4a3a50fda68df83e22eca3a8d26dae768794dd808621135f04ac419ad1c47c.

## Classification

- Official documentation claim: sub-transaction views are divided and encrypted for entitled recipients.
- Official documentation claim: participant visibility is stakeholder/contract-scoped.
- Official documentation claim: divulgence can make contract information visible to transaction participants beyond originally declared observers.

## Limitations

- Documentation establishes the design and stated guarantees, not a test of a named production Canton deployment.
- Current HTML and raw MDX are snapshots; hashes identify the downloaded files.
- Detailed text behind some MDX component placeholders was not recovered. Claims above rely only on explicit extracted text.

## Open questions

- Inspect the precise protocol-level behavior of encrypted views and the Synchronizer using the Canton protocol specification.
- Determine how much metadata remains visible to Synchronizer infrastructure and other network components.