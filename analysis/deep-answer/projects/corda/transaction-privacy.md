# R3 Corda — transaction privacy

Status: official Corda 5.2 documentation reviewed in browser. The user's Codespace returned HTTP 403 for the selected R3 pages; no local snapshot is claimed.

## Findings

Corda 5.2 documents more than one notary/verification design. Privacy properties depend on which protocol is used.

### Non-validating notary protocol

The notary performs uniqueness and time-window checks while revealing only selected transaction components:

| Transaction component | Visibility to non-validating notary |
|---|---|
| Input states | References only |
| Output states | Number of states only |
| Commands and signer identities | Hidden |
| Time window | Fully visible |
| Notary identity | Fully visible |
| Signatures | Hidden |
| Transaction metadata | Fully visible |

Participants must resolve the transaction backchain to verify provenance. R3 notes this can require nodes to fetch transactions they were not directly involved in and can expose a token's history to those nodes.

### Transaction Privacy Enhancements / contract-verifying notary

Corda 5.2 describes a privacy-enhanced mode in which every virtual node no longer needs to see and verify all predecessors. In exchange, transaction-content visibility must be given to the notary, which verifies the applicable contracts.

Filtered transactions use Merkle proofs to reveal only relevant transaction components, including the output states used as inputs and relevant notary metadata/signature.

R3 lists the trade-off:
- Participants see only transactions they are party to and the filtered input information required for verification.
- Greater trust is placed in the contract-verifying notary operator.
- The notary receives transaction content and contract-verification responsibility.

## Evidence

1. [Transaction Privacy Enhancements — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/enhanced-ledger-privacy.html)
2. [Non-Validating Notary Protocol — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/non-validating-notary.html)
3. [Notary Protocols — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/notary-protocols.html)
4. [Notaries — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries.html)

## Classification

- Official documentation claim: non-validating notary receives limited transaction components.
- Official documentation claim: transaction privacy enhancements shift contract verification and transaction-content visibility to the notary.
- Official documentation claim: filtered transactions use Merkle proofs to disclose only relevant components.
- Interpretation: Corda's privacy model involves a configurable trust and disclosure trade-off, not a single fixed notary-visibility rule.

## Limitations

- These findings are specifically about Corda 5.2 documentation.
- They must not be silently generalized to Corda Enterprise 4.10 or 4.14.
- The user's terminal requests to R3 returned HTTP 403. Browser-accessible official documentation was used instead; no local Corda source snapshot or SHA-256 is available.
- No Corda network or CorDapp was run for this research.