# Deep Answer — transaction privacy comparison

Status: preliminary comparison based on official documentation and user-terminal snapshots for Ethereum, Canton, and Rayls; Corda 5.2 is browser-verified because terminal requests returned HTTP 403.

| Project | Main mechanism | What is hidden / restricted | What remains visible or trusted |
|---|---|---|---|
| Ethereum | Privacy tools and application-layer mechanisms (ZK proofs, stealth addresses, privacy pools, selective disclosure) | Depends on the selected application; ZK proofs can prove facts without exposing underlying data | Ethereum base-layer on-chain actions remain publicly visible; privacy is not automatically supplied by using a ZK rollup |
| Canton | Sub-transaction views, stakeholder-based distribution, encryption | Participants receive only views they are entitled to see | Divulgence can reveal related contracts; Synchronizer sees encrypted messages and confirmation results according to the documentation |
| R3 Corda 5.2 | Non-validating or contract-verifying notary; filtered transactions with Merkle proofs | Depending on protocol, commands/signers or full backchains may be hidden; participants can see only transaction portions required for verification | Non-validating notary still sees time window, notary identity, and metadata; enhanced privacy gives transaction content to the contract-verifying notary |
| Rayls Enygma Public | Shielded notes, encrypted notes, nullifiers and commitments | Public cannot see sender, recipient, amount, spent notes, or shared-vault token identity for shielded payment | Public can see that a shielded payment occurred, relayer/gas data, nullifiers, commitments and encrypted notes; shield/unshield/registration remain public |

## Key interpretive points

1. Ethereum must not be described as having no privacy tools. Its base layer is transparent, while privacy is implemented by tools and applications with different disclosure properties.
2. Canton restricts the distribution of transaction views by stakeholder relationships. Divulgence is an explicit privacy consideration.
3. Corda has protocol-dependent trust and disclosure trade-offs. The non-validating notary and transaction privacy enhancements are not the same privacy configuration.
4. Rayls hides payment details from the public while preserving visible cryptographic artifacts and public shield/unshield activity.

## Evidence sources

- Ethereum: [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/), [Privacy roadmap](https://ethereum.org/roadmap/privacy/)
- Canton: [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model), [Participant Node Architecture](https://docs.canton.network/overview/reference/participant-overview)
- Corda: [Transaction Privacy Enhancements — 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/enhanced-ledger-privacy.html), [Non-Validating Notary — 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/non-validating-notary.html)
- Rayls: [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what)

## Not yet final

The comparison must be revisited after the network-model criterion is completed and the Corda version scope is aligned with the quest's intended product comparison.