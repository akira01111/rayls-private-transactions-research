# R3 Corda — transaction privacy

Status: official Corda 5.2 documentation reviewed in browser. The user's Codespace returned HTTP 403 for selected R3 pages; no local documentation snapshot is claimed.

## Privacy depends on the notary protocol

Corda 5.2 documents more than one notary/verification design. The visibility and trust boundary depend on which protocol is selected.

### Non-validating notary

The non-validating notary performs uniqueness and time-window checks while receiving selected transaction components:

| Transaction component | Visibility to non-validating notary |
|---|---|
| Input states | References only |
| Output states | Number of states only |
| Commands and signer identities | Hidden |
| Time window | Fully visible |
| Notary identity | Fully visible |
| Signatures | Hidden |
| Transaction metadata | Fully visible |

Participants must resolve the transaction backchain to verify provenance. R3 warns that this may require nodes to fetch transactions they were not directly involved in, potentially exposing a token's history to those nodes.

### Transaction Privacy Enhancements / contract-verifying notary

Corda 5.2 also documents a privacy-enhanced mode in which every virtual node no longer needs to see and verify all predecessors. In exchange, the contract-verifying notary receives transaction content so it can perform contract verification.

Filtered transactions use Merkle proofs to disclose only relevant transaction components, including output states used as inputs and relevant notary metadata/signature. The result is a different trust distribution:
- Participants see transactions they are party to and filtered input information needed for verification.
- The contract-verifying notary receives content and takes on contract-verification responsibility.
- The application chooses a protocol; neither notary mode should be presented as the only Corda privacy model.

## Evidence

1. [Transaction Privacy Enhancements — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/enhanced-ledger-privacy.html)
2. [Non-Validating Notary Protocol — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/non-validating-notary.html)
3. [Notary Protocols — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/notary-protocols.html)
4. [Notaries — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries.html)

## Evidence classification and limits

- **Official documentation claim:** non-validating notary receives limited transaction components.
- **Official documentation claim:** privacy enhancements shift transaction-content visibility and contract verification to a contract-verifying notary.
- **Official documentation claim:** filtered transactions use Merkle proofs to reveal relevant components.
- **Interpretation:** Corda's privacy model involves a configurable trust and disclosure trade-off, not one fixed notary-visibility rule.
- These findings are specifically about Corda 5.2 and must not be silently generalized to Corda Enterprise 4.10 or 4.14.
- Terminal requests to R3 returned HTTP 403. Browser-accessible official documentation was used; the 403 response is not source content.
- No Corda network or CorDapp was run for this research.

## Institutional relevance

Corda demonstrates controlled peer-to-peer data distribution and a choice of notary trust models. It is a strong permissioned-DLT comparator, but not a public blockchain privacy layer. Its value in this comparison is to make the privacy/control trade-off explicit.
