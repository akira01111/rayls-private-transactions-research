# R3 Corda — deployment status

Status: Corda 5.2 documentation explicitly supports dynamic application networks for production use. The reviewed material does not independently establish a particular named Corda 5.2 network as currently live.

## Product and deployment scope
- Corda 5.2 documentation identifies **dynamic networks** as the model used for production networks. A running Membership Group Manager (MGM) registers members and distributes member information across clusters.
- **Static networks** are intended for local testing with predetermined members and no MGM.
- Corda Enterprise 4.10 is documented as a commercial edition of the Corda platform. The observer-node/regulator-reporting example in this research refers to Enterprise 4.10.
- Corda 5.2 and Corda Enterprise 4.10 are not one release or one deployment. Their respective network and observer capabilities must be labelled with their own version scope.

## Evidence
1. [Developing Applications — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/developing-applications.html) — dynamic networks for production; static networks for local testing.
2. [Creating Application Networks — Corda 5.2](https://docs.r3.com/en/platform/corda/5.2/application-networks/creating.html) — MGM and member onboarding.
3. [Corda Enterprise 4.10](https://docs.r3.com/en/platform/corda/4.10/enterprise.html) — commercial edition description.
4. [Posting transactions to observer nodes — Enterprise 4.10](https://docs.r3.com/en/platform/corda/4.10/enterprise/get-started/tutorials/supplementary-tutorials/tutorial-observer-nodes.html) — application-level regulator reporting pattern.

## Interpretation limits
- "Supports production networks" is a capability statement in product documentation, not proof of a named network's current live deployment.
- The observer-node tutorial demonstrates how a CorDapp can send signed transaction reports to regulator observer nodes; it does not prove that every Corda application does this automatically.
- Do not use the Enterprise 4.10 observer-node example to claim the same feature was tested in Corda 5.2.
