# HOW CAN FINANCIAL INSTITUTIONS MAKE PRIVATE TRANSACTIONS ON A PUBLIC BLOCKCHAIN?

Status: working article draft. Stage 3 self-verification is still pending, so this is not yet the final quest submission.

## THE APPARENT CONTRADICTION

A public blockchain is designed to make activity verifiable. Financial institutions, however, cannot expose every counterparty, amount, position, or commercial relationship to every observer.

The apparent contradiction disappears when public verification is separated from public disclosure. A transaction can leave verifiable evidence on a shared ledger without making all of its business content public. The design question is not simply whether a blockchain is public or private. It is who can see which part of a transaction, under what authority, and with what proof that the transaction was valid.

## WHY USE PUBLIC OR SHARED INFRASTRUCTURE?

Institutions may look to tokenized ledger infrastructure for programmable settlement, a shared source of transaction state, atomic delivery-versus-payment, and connectivity between applications and asset networks. The IMF describes programmability, shared ledgers, and atomic settlement as key features of tokenized finance. These features can reduce reconciliation and automate financial workflows, although they are not exclusive to permissionless public chains.

There are also trade-offs. The BIS notes that open permissionless networks can create accountability and legal-responsibility questions, while closed private networks can fragment interoperability. A public-permissioned or application-permissioned model may offer a middle ground, depending on the use case.

Institutional activity is real but should be described precisely. Visa's 2021 announcement covered a USDC pilot over Ethereum for part of Crypto.com's Visa card-program settlement obligations; it was not a statement that consumer purchases were settled directly on Ethereum. Visa's later multi-chain settlement pilot includes Ethereum among supported chains, while a separate 2025 U.S. bank USDC settlement launch initially used Solana. These examples show experimentation with blockchain settlement, not one universal deployment model.

## WHAT SHOULD REMAIN PRIVATE?

The fields that require protection depend on the transaction and its legal context. For a financial institution, sensitive information may include:
- which customer or institution is paying which counterparty;
- the amount, asset, and resulting balance or position;
- the timing and pattern of payments that could reveal a business relationship or trading strategy;
- contract, invoice, or settlement instructions; and
- the ownership and spendable value represented by private notes.

This is a design checklist, not a claim that every protocol hides every field. Some metadata must remain available for transaction ordering, fees, proof verification, or audit. A privacy system should identify the permitted audience for each field rather than promise that the entire transaction disappears.

## FOUR DIFFERENT PRIVACY MODELS

Ethereum illustrates the transparent baseline. Ethereum Mainnet exposes ordinary on-chain activity to public inspection, while privacy is added by applications and protocols. ERC-5564 stealth addresses can reduce the link between a recipient's identity and a one-time receiving address. But a stealth address is not a fully confidential payment: the public transfer and the ERC's recommended token/amount announcement metadata remain visible. Zero-knowledge proofs and privacy pools can support other forms of selective disclosure, but their guarantees depend on the specific application.

Canton takes a different approach. It decomposes a transaction into stakeholder-specific views, encrypts them for entitled recipients, and distributes only the relevant views. Signatories, observers, and controllers have different roles. The Synchronizer coordinates processing and, according to the documented privacy model, sees encrypted messages and confirmation results rather than plaintext transaction views. Divulgence can still reveal related contract information, so application design matters.

Corda 5.2 uses permissioned application networks and peer-to-peer flows. Its privacy properties depend on the notary protocol. A non-validating notary sees selected components such as input references, output count, time window, notary identity, and metadata, while commands and signer identities are hidden. A contract-verifying notary receives transaction content to verify contracts. Filtered transactions and Merkle proofs allow participants to receive relevant components without every participant seeing every predecessor. This shifts trust toward the notary.

Rayls Enygma Public is the main public-chain privacy case in this research. Rayls documents shielded notes, encrypted notes, commitments, and nullifiers. The documentation says public observers can see that a shielded payment occurred and inspect cryptographic artifacts and relayer/gas metadata, but cannot see the sender, recipient, amount, or spent notes. Public operations such as registration, shielding, and unshielding still reveal specified information. The privacy model preserves a public transaction trace without exposing the shielded payment content to ordinary observers.

## AUDITORS NEED A DIFFERENT ACCESS PATH

Privacy cannot mean that legitimate reviewers are permanently excluded. But auditor access should be scoped and governed rather than treated as unrestricted administrative power.

On Ethereum, public data is visible to everyone. For private application data, users can selectively share viewing keys or provide cryptographic compliance proofs. ERC-5564 distinguishes viewing and spending keys; an auditor's viewing access is not automatically spending authority.

Canton documents two different patterns. A Daml contract observer can be added to selected contracts for audit or compliance visibility. An Observing Participant Node with Observation permission can read transactions involving the party it hosts, but Observation alone does not allow it to submit or confirm transactions. These mechanisms are not a universal network-wide auditor.

Corda's Enterprise 4.10 observer-node tutorial shows application-integrated reporting: a CorDapp sends signed transaction information to a regulator node through explicit flows. The application determines what is sent. This is not automatic reporting for every Corda application, and the example must not be conflated with Corda 5.2.

Rayls documents a deployment-level auditor key. When an account registers, a copy of its view key is encrypted to the deployment auditor key using ML-KEM-768 and stored in the registry. The view key allows reading shielded transaction details; spending still requires the account's spend key. This is an official product claim, not an independently tested result in this research.

## CONTROL DOES NOT DISAPPEAR

A privacy layer does not by itself satisfy institutional governance or regulatory obligations. Institutions still need identity and eligibility controls, secure key custody, auditor authorization, logging, upgrade governance, incident handling, and legal processes.

The four architectures distribute those responsibilities differently. Canton combines public-network interoperability with sponsorship and application-level permissioning. Corda 5.2 uses MGM membership for application networks. Rayls documents a validator onboarding model for its Public Chain and an owner multisig for relevant contract upgrades. Ethereum Mainnet permits broad public participation, so institutions must govern their application layer and privacy infrastructure.

Deployment status is equally important. Ethereum Mainnet is a production public network. Canton MainNet is its documented production environment. Corda 5.2 documents production-capable dynamic application networks, but this evidence pack does not verify a named live Corda 5.2 deployment. Rayls Public Chain Mainnet launched in 2026, but Enygma Public itself remains a testnet pilot. Enygma Sovereign is a separate institutional product and must not be used to claim that Enygma Public is in production.

## WHAT THE NOVEMBER 21 ENYGMA TRANSACTION SHOWS

A historical Enygma Public Testnet transaction examined for this research was a successful transferV2 call at block 24,825,928 on November 21, 2026. Its decoded receipt had one input, three outputs, and a ten-element statement. The public transaction evidence included one Nullifier event, three Commitment events, and three EncryptedNote events.

That public surface is useful: it shows that a shielded payment still produces verifiable on-chain artifacts. It does not, on its own, reveal the private payment content or establish the meaning of every statement value. In particular, the integer 4,416,000,000,000,000,000 is directly present in the statement, but its denomination and semantic meaning are not independently established here.

A review of the OwnerMultisig's 24 current proposals found the direct SharedVaultProxy upgrade actions and six role grants. The best-supported implementation reconstruction for the November 21 transaction is 0xad966..., based on confirmed upgrade chronology and role authorization review. This is not a direct historical storage read: the RPC reported that the relevant historical EIP-1967 state had been pruned, and indirect or non-multisig paths were not ruled out.

The November 21 transaction is a historical case study. It is not the researcher's own required self-verification payment.

## THE DESIGN PRINCIPLE

Financial institutions can make private transactions on public or shared blockchain infrastructure by separating the information needed for public verification from the information that should remain private. They then add a controlled disclosure path for counterparties, auditors, or regulators, and govern who can change the keys, contracts, participants, and reporting rules.

There is no single universal privacy model. Ethereum shows application-level privacy over a transparent base layer; Canton shows encrypted stakeholder views; Corda shows permissioned transaction distribution and notary trade-offs; Rayls Enygma Public documents shielded payments and a deployment auditor path on a public-chain testnet.

The evidence supports the architecture principle. It does not yet establish production readiness for Enygma Public or independently prove auditor decryption. Stage 3 self-verification — one private payment submitted by the researcher on Enygma Public Testnet and inspected in the public explorer — remains necessary before this draft is treated as the final quest submission.

## SOURCES

- IMF, [Tokenized Finance and Money](https://www.imf.org/en/news/articles/2026/05/11/sp051126-tokenized-finance-and-money).
- BIS, [Tokenisation in financial services: pathways to scale](https://www.bis.org/speeches/20241104-tokenisation-financial-services-pathways-scale).
- Visa, [USDC settlement over Ethereum pilot](https://usa.visa.com/about-visa/newsroom/press-releases.releaseld.17821.html).
- Visa, [Multi-chain stablecoin settlement expansion](https://corporate.visa.com/en/sites/visa-perspectives/newsroom/visa-expands-stablecoin-settlement-adds-five-blockchains.html).
- Ethereum, [Privacy on Ethereum](https://ethereum.org/privacy/ethereum/); [ERC-5564: Stealth Addresses](https://eips.ethereum.org/EIPS/eip-5564).
- Canton, [Privacy Model Explained](https://docs.canton.network/overview/learn/privacy-model).
- R3, [Corda 5.2 Transaction Privacy Enhancements](https://docs.r3.com/en/platform/corda/5.2/developing-applications/ledger/enhanced-ledger-privacy.html); [Corda Enterprise 4.10 observer nodes](https://docs.r3.com/en/platform/corda/4.10/enterprise/get-started/tutorials/supplementary-tutorials/tutorial-observer-nodes.html).
- Rayls, [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what); [Enygma Public testnet guide](https://docs.rayls.com/docs/try-enygma-public-on-testnet).
