# R3 Corda — auditor access

Status: official R3 Corda Enterprise 4.10 observer-node tutorial reviewed through browser. Terminal retrieval returned HTTP 403.

## Findings

R3 documents observer nodes as a pattern for financial networks where regulators need reporting on actions taken. A regulator can operate its own node and receive digitally signed, deduplicated reports.

The documented TradeAndReport example:
- Distributes a signed transaction to the buyer and a state regulator through FinalityFlow.
- Separately reports the transaction to a national regulator through an application flow.
- Sends the signed transaction to the regulator responder.
- Records the transaction's states using StatesToRecord.ALL_VISIBLE.

R3 also warns that default vault queries do not distinguish states recorded as participant/owner from states recorded as observer. Custom queries should be written when an application must return only participant/owner states.

## Evidence

1. [Posting transactions to observer nodes — Corda Enterprise 4.10](https://docs.r3.com/en/platform/corda/4.10/enterprise/get-started/tutorials/supplementary-tutorials/tutorial-observer-nodes.html)
   - Official R3 documentation and Kotlin/Java sample flow.
   - Relevant browser-inspected lines: 401–409, 414–459, and 543–547.
   - Codespace curl status: HTTP 403. The downloaded response was an error page, not documentation.

## Classification

- Official documentation and code-example claim: regulator observer nodes can receive application-distributed transaction reports.
- Interpretation: audit access is application-integrated and depends on the CorDapp flow and what it sends.
- Not established: every Corda deployment or CorDapp automatically reports every transaction to a regulator.
- Not established: a universal network-wide auditor role.