# R3 Corda — network model

Status: preliminary; current evidence is version-specific to Corda 5.2.

## Current evidence

Corda 5.2 documentation describes application networks with a Membership Group Manager (MGM) that members register with before transacting within the group. A notary is a member/service role in the application network.

Corda documentation also describes participant-to-participant communication as peer-to-peer using flows.

## Evidence

1. [Creating Application Networks — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/application-networks/creating.html)
2. [Notary Protocols — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/notaries/notary-protocols.html)
3. [Corda 5.2 Glossary](https://docs.r3.com/en/platform/corda/5.2/reference/glossary.html)

## Classification

- Official documentation claim: application-network membership requires registration with an MGM.
- Official documentation claim: participant communication uses peer-to-peer flows.
- Preliminary interpretation: Corda application networks are permissioned membership environments.

## Still to verify

- Compare Corda 5.2 and Corda Enterprise 4.10/4.14 only where necessary; they are separate product/version scopes.
- Clarify the Corda Enterprise deployment model used for the intended comparison, rather than using “Corda” as if every release and edition were identical.
- Do not infer that all application-network data is visible to every admitted member.