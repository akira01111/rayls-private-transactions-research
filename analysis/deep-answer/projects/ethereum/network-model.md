# Ethereum — network model

Status: evidence reviewed for Ethereum's base network model. The distinction between Mainnet, public testnets, private networks, and application or Layer 2 environments must be preserved in the final comparison.

## Supported observations

### Public networks and Mainnet

- Ethereum documentation describes networks as groups of connected computers that communicate using the Ethereum protocol.
- There is one Ethereum Mainnet. Other independent networks can follow the same protocol rules for testing or development without sharing balances or transaction history with Mainnet.
- Public networks are accessible to anyone with an internet connection. The documentation states that anyone can read or create transactions and validate transactions on a public blockchain.
- Ethereum Mainnet is described as the primary public production blockchain, where transactions involving assets of actual value are recorded.

### Testnets are not identical to Mainnet

- Ethereum has public testnets for protocol and smart contract testing before deployment to Mainnet.
- The documentation identifies Sepolia as the recommended default testnet for application development. It specifically says Sepolia uses a permissioned validator set controlled by client and testing teams.
- Hoodi is identified as a testnet for protocol developers to test network upgrades and for stakers to test validator operation.
- Therefore, the existence of public testnets does not mean every Ethereum network uses the same validator admission model as Mainnet.

### Private and consortium networks

- The Ethereum Networks documentation defines a private network in this context as one whose nodes are not connected to a public network such as Mainnet or a testnet.
- It explicitly cautions that “private” in this context means reserved or isolated, not necessarily protected or secure.
- The documentation describes consortium networks as networks where consensus is controlled by a predefined set of trusted nodes.
- These descriptions concern separate network configurations. They must not be used to reclassify Ethereum Mainnet as a permissioned network.

### Proof of Stake and validator participation

- Ethereum's consensus mechanism is Proof of Stake. The official documentation says Ethereum switched to Proof of Stake in 2022.
- Validators stake ETH and are responsible for checking proposed blocks. They may also be selected to propose blocks.
- To participate directly as a validator, a user must deposit 32 ETH into the deposit contract and operate an execution client, a consensus client, and a validator client.
- The 32 ETH requirement applies to direct validator participation. It is not a requirement for ordinary users to submit transactions.
- The documentation describes 12-second slots and 32-slot epochs. Validators attest to blocks, and finality is based on supermajority agreement over checkpoints.

## Evidence snapshots

### 1. Ethereum Networks

Official source: [Ethereum Networks](https://ethereum.org/developers/docs/networks/)

- Retrieval method: user-run Bash `curl` in GitHub Codespaces.
- Retrieval date: 2026-11-28.
- HTTP status: 200.
- Downloaded size: 444,383 bytes.
- SHA-256: `835711ee4021bcac282813c361cb45cf980ef0112c4e4bfc28d4f9157e38c6b8`.
- Page-reported last update: 2026-09-23.
- Extracted from the page's `article#main-content` element.

### 2. Ethereum Proof of Stake

Official source: [Proof of Stake](https://ethereum.org/developers/docs/consensus-mechanisms/pos/)

- Retrieval method: user-run Bash `curl` in GitHub Codespaces.
- Retrieval date: 2026-11-28.
- HTTP status: 200.
- Downloaded size: 413,995 bytes.
- SHA-256: `295eeabd5f951cce8e09f42ce23170eaa13167dbc18dfa2fb8d7df5d3e5082ef`.
- Page-reported last update: 2026-10-07.
- Extracted from the page's `article#main-content` element.

## Evidence classification

- **Official documentation claim:** public network access, Mainnet production status, public testnet purpose, Sepolia's permissioned validator set, private and consortium network definitions, Proof of Stake, validator responsibilities, and the 32 ETH direct-validator deposit requirement.
- **Direct retrieval observation:** both official pages returned HTTP 200 and were saved as local HTML snapshots. The recorded SHA-256 values identify the retrieved snapshots.
- **Not independently tested:** this research did not independently join an Ethereum validator set, inspect live validator admission, or test Sepolia/Mainnet transactions as part of this network-model review.

## Scope and interpretation limits

- Do not say that every Ethereum network is permissionless. The documentation itself describes Sepolia as having a permissioned validator set.
- Do not say that ordinary Ethereum users need 32 ETH to transact. That amount is the documented direct-validator deposit requirement.
- Do not conflate Ethereum Mainnet with Sepolia, Hoodi, local development networks, consortium networks, or Layer 2 systems.
- A network being public and its applications being permissionless are different questions. The present snapshots do not establish the permissioning model of every application or Layer 2 network in the Ethereum ecosystem.

## Still to verify

- How institutional permissioning and privacy applications are deployed above Ethereum Mainnet, and whether specific examples are relevant to the quest.
- Whether the final comparison should focus strictly on Ethereum Mainnet or separately describe other Ethereum ecosystem environments.
- Any specific Layer 2 or institutional deployment claim must be supported by its own primary source and version/deployment boundary.
