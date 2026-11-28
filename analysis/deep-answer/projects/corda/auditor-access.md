# R3 Corda — auditor access

Status: official R3 Corda Enterprise 4.10 observer-node tutorial reviewed through browser. Terminal retrieval returned HTTP 403; no local HTML snapshot is claimed.

## Application-integrated observer nodes

R3 documents observer nodes as a pattern for financial networks where regulators need reporting on actions taken. A regulator can operate its own node and receive digitally signed, deduplicated reports.

The documented TradeAndReport example:
- Distributes a signed transaction to the buyer and a state regulator through FinalityFlow.
- Separately reports the transaction to a national regulator through an application flow.
- Sends the signed transaction to the regulator responder.
- Records transaction states using **ALL_VISIBLE**.

R3 also warns that default vault queries do not distinguish states recorded as participant/owner from states recorded as observer. Custom queries are needed when an application should return only participant/owner states.

## What the example demonstrates

The observer-node example is an application-level reporting pattern. The CorDapp decides which transactions to send and which states to record. It is not evidence of a network-wide auditor role or automatic regulator access to every transaction in every Corda application.

## Evidence

1. [Posting transactions to observer nodes — Corda Enterprise 4.10](https://docs.r3.com/en/platform/corda/4.10/enterprise/get-started/tutorials/supplementary-tutorials/tutorial-observer-nodes.html)
   - Official R3 documentation and Kotlin/Java sample flow.
   - Relevant browser-inspected lines: 401–409, 414–459, and 543–547.
   - Codespace curl status: HTTP 403. The downloaded response was an error page, not documentation.

## Classification and limits

- **Official documentation/code example claim:** regulator observer nodes can receive application-distributed signed transaction reports.
- **Interpretation:** audit access is integrated into application flows and depends on the CorDapp's reporting logic.
- **Not established:** every Corda deployment or CorDapp automatically reports every transaction to a regulator.
- **Not established:** a universal network-wide auditor role.
- This example is specifically Corda Enterprise 4.10 and must not be presented as an independently tested Corda 5.2 feature.

## Institutional relevance

Corda demonstrates that regulator reporting can be built into a permissioned application flow, with explicit control over which transactions/states are distributed. The institution still needs to govern the reporting flow and the regulator node's data handling.
