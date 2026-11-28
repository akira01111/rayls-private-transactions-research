# Why financial institutions consider public blockchain infrastructure

Status: research note based on official institutional, central-bank, and international-organization sources retrieved by 2026-11-28. The note distinguishes design benefits from evidence that institutions have actually piloted or announced a use case.

## 1. Programmability and atomic workflows

Tokenized assets and money can be represented and controlled through programmable ledger logic. The IMF's 2026 discussion identifies three structural features of tokenization:
- Programmability: smart contracts can automate financial logic such as margin calls, coupon payments, and collateral transfers.
- Shared ledgers: a synchronized source of truth can reduce bilateral reconciliation.
- Atomic settlement: delivery-versus-payment can occur simultaneously or near real time.

These are properties of tokenized ledger architecture, not exclusive properties of public blockchains. A permissioned network can also provide them.

Source: [IMF — Tokenized Finance and Money (2026-05-22)](https://www.imf.org/en/news/articles/2026/05/11/sp051126-tokenized-finance-and-money).

## 2. Broader access, interoperability, and network effects

Public infrastructure can allow multiple applications, users, infrastructure providers, and asset ecosystems to connect without each institution creating an isolated ledger. In practice, institutions still need identity, legal, asset, and governance controls at application or network level.

The BIS describes a trade-off:
- Public permissionless networks attract broad users and applications, but governance accountability, anonymous service providers, and legal responsibility may be difficult for regulated institutions.
- Private permissioned networks can align more directly with regulatory requirements, but separate systems can create interoperability fragmentation.
- Public permissioned infrastructure is one possible middle ground: open-style connectivity with eligibility and governance safeguards.

Source: [BIS — Tokenisation in financial services: pathways to scale (2024-11-04)](https://www.bis.org/speeches/20241104-tokenisation-financial-services-pathways-scale).

## 3. Longer operating windows and treasury operations

Visa's 2025 announcement of USDC settlement for selected U.S. issuer/acquirer partners identifies faster movement over blockchains, seven-day availability, improved operational resilience over weekends and holidays, and modernized liquidity/treasury management as potential operational benefits. The initial U.S. bank participants cited in that announcement settled over Solana; this is not evidence that those particular flows used Ethereum.

In 2026, Visa described its multi-chain settlement pilot as supporting nine blockchains, including Ethereum, and framed multi-chain support as giving partners choices in accessing liquidity across ecosystems.

Sources:
- [Visa — U.S. USDC settlement launch (2025-12-16)](https://usa.visa.com/about-visa/newsroom/press-releases.releaseId.21951.html).
- [Visa — multi-chain settlement expansion (2026-04-29)](https://corporate.visa.com/en/sites/visa-perspectives/newsroom/visa-expands-stablecoin-settlement-adds-five-blockchains.html).

## 4. Asset mobility and connection to market infrastructure

DTCC and the Stellar Development Foundation announced in May 2026 a plan to connect DTC's tokenization service to the Stellar public blockchain, with tokenized assets expected in the first half of 2027. DTCC describes the objectives as faster settlement, greater asset mobility, extended trading hours, lower cost and risk, deeper liquidity, and interoperability with traditional market infrastructure.

This is a **future integration plan**, not a live deployment as of the announcement date.

Source: [DTCC — DTC tokenization service to connect with Stellar (2026-05-27)](https://www.dtcc.com/press-releases/2026/tokenization-service-to-connect-with-stellar-public-blockchain-as-dtc-advances-multi-chain-strategy).

## 5. Why privacy and institutional controls remain necessary

The same openness that makes shared public infrastructure useful can reveal commercially sensitive counterparties, amounts, timing, or positions. Institutional designs must also address:
- identity and eligibility of participants;
- data minimization and confidentiality;
- auditor/regulator access;
- asset controls and legal enforceability;
- governance, change management, and operational accountability.

The BIS specifically cautions that open permissionless networks can raise governance/accountability concerns, while closed private networks can fragment liquidity and interoperability. The appropriate answer is not automatically “put everything on a permissionless chain.” It is to select a network model and privacy/control architecture that fits the asset, participants, and legal obligations.

## Synthesis for the Deep Answer

The evidence supports a qualified argument: institutions may want public or broadly interoperable blockchain infrastructure for programmable settlement, shared state, wider connectivity, multi-chain liquidity, and extended operating windows. They do not thereby want every transaction detail to be public or every actor to have unrestricted authority. Privacy, selective disclosure, identity/eligibility, auditor access, and governance remain design requirements.

Keep separate:
- **Documented institutional benefits:** as stated by IMF, BIS, Visa, and DTCC.
- **Observed examples/pilots:** Visa's dated settlement announcements and DTCC's announced future integration plan.
- **Inference for this article:** a privacy layer can address disclosure needs while institutions access shared settlement infrastructure. This inference must be explained and supported by the Rayls/Canton/Corda/Ethereum comparison rather than presented as a claim made by one source.
