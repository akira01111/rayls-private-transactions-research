# Ethereum — network model

Status: reviewed against Ethereum's current official network and consensus documentation. The model below refers primarily to Ethereum Mainnet; public testnets and separately configured private/consortium networks are not interchangeable with Mainnet.

## Network model

### Ethereum Mainnet
- Ethereum Mainnet is a public production network. Official documentation says public networks are accessible to anyone with an internet connection: anyone can read the chain and create transactions, while consensus among peers determines inclusion and state.
- Mainnet uses Proof of Stake. Direct validator participation requires a 32 ETH deposit and operation of execution, consensus, and validator clients. The 32 ETH requirement applies to becoming a validator, not to ordinary users submitting transactions.
- Public access and validator operation are distinct questions: ordinary users can use the network without becoming validators.

### Testnets and separate networks
- Sepolia is the recommended default testnet for application development. Ethereum's network documentation describes its validator set as permissioned and controlled by client and testing teams.
- Hoodi is directed at protocol developers testing upgrades and stakers testing validator operation.
- Ethereum documentation also describes private networks as isolated from public networks and consortium networks as having consensus controlled by a predefined set of trusted nodes. Those are separate configurations, not descriptions of Ethereum Mainnet.

## Evidence
1. [Ethereum Networks](https://ethereum.org/developers/docs/networks/) — retrieved 2026-11-28; documents public network access, Mainnet production status, testnets, Sepolia's permissioned validator set, and private/consortium distinctions.
2. [Proof of Stake](https://ethereum.org/developers/docs/consensus-mechanisms/pos/) — documents validator responsibilities and the 32 ETH direct-validator deposit.

## Classification and limits
- **Official documentation claims:** public network access, Mainnet production status, Proof of Stake, validator requirements, and testnet characteristics.
- **Direct retrieval observation:** official Ethereum.org pages retrieved in the user's Codespace; snapshot details are recorded in the previous evidence pack.
- **Not independently tested:** this research did not run an Ethereum validator or independently test validator admission.
- Do not describe every Ethereum ecosystem environment as permissionless. In particular, Sepolia's validator set is documented as permissioned.
- Do not state that ordinary users need 32 ETH to transact.
- Do not conflate Mainnet with Sepolia, Hoodi, local networks, consortium deployments, or Layer 2 networks.

## Institutional relevance
Ethereum Mainnet provides an established public settlement environment and broad public access. Privacy for financial transactions is not supplied by the base ledger itself; it must be added through applications or protocols with their own disclosure and governance models. An institutional example and its scope are recorded in [deployment status](deployment-status.md).

## Evidence snapshot metadata retained from Codespaces retrieval

### Ethereum Networks
- Retrieval method: user-run Bash `curl` in GitHub Codespaces.
- Retrieval date: 2026-11-28; HTTP 200; downloaded size: 444,383 bytes.
- SHA-256: `835711ee4021bcac282813c361cb45cf980ef0112c4e4bfc28d4f9157e38c6b8`.
- Page-reported last update: 2026-09-23; extracted from `article#main-content`.

### Ethereum Proof of Stake
- Retrieval method: user-run Bash `curl` in GitHub Codespaces.
- Retrieval date: 2026-11-28; HTTP 200; downloaded size: 413,995 bytes.
- SHA-256: `295eeabd5f951cce8e09f42ce23170eaa13167dbc18dfa2fb8d7df5d3e5082ef`.
- Page-reported last update: 2026-10-07; extracted from `article#main-content`.
