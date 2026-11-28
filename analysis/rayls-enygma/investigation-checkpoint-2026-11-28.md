# Rayls Enygma Investigation Checkpoint — 2026-11-28

## Purpose

Handoff checkpoint for continuing the investigation of transaction `0x09edab2bb8914aea3c905608ea9fcd09c056a470a5e150df03e0b324eff525bb`, block `24825928`, timestamp `2026-11-21T09:40:42Z`, destination proxy `0x9c5ad5e5ea5b5910e7fd1e1cc7b70ce0e4bf06c2`.

**Critical caution:** do not treat the implementation verified on 2026-11-27 as proof of the implementation active on 2026-11-21.

## 1. Proxy timeline

| Block | UTC time | Event / implementation | Evidence status |
|---:|---|---|---|
| 21,568,375 | 2026-10-30 00:04:35 | Proxy creation; creation tx log emitted `Upgraded(address)` with implementation `0x0a3a9f0e41937d330a8734c3276557f1ec9ad62f` | Explorer transaction-specific log; block cross-checked with RPC |
| 24,825,928 | 2026-11-21 09:40:42 | Historical `transferV2` target transaction, tx index 0 | Transaction verified; active implementation unknown |
| 25,699,353 | 2026-11-26 22:08:28 | `Upgraded(address)` points to `0x9644667cc096964bafb6a533d57873544fbfb956` | RPC log observed |
| 25,714,062 | 2026-11-27 00:22:17 | `Upgraded(address)` points to `0x937471b6acdad0c77d6874d0546d6009e09cd3f0` | RPC log observed |
| Latest, checked 2026-11-28 | — | ERC-1967 implementation slot contains `0x937471b6acdad0c77d6874d0546d6009e09cd3f0` | Direct current-state RPC observation |

The later upgrade events do not establish the implementation active on 2026-11-21. The initial creation event does not prove the initial implementation remained active until then.

## 2. Deployment evidence

Creation transaction:
`0xa626fb912862868ebe94747d6d2256e18e3ed7cdd2cf4d2da0ccdf31c7f4c3a7`

Explorer reported:
- transaction type: `contract_creation`
- success
- timestamp: `2026-10-30T00:04:35Z`
- created address: SharedVaultProxy `0x9c5ad5e5ea5b5910e7fd1e1cc7b70ce0e4bf06c2`
- proxy type: `eip1967`
- creation log 0 is `Upgraded(address)`, with implementation `0x0a3a9f0e41937d330a8734c3276557f1ec9ad62f`.

RPC `eth_getTransactionByHash` returned block `0x1491b77` = **21,568,375**. Explorer transaction metadata independently returned `block_number: 21568375`.

RPC `eth_getTransactionReceipt` returned `result: null`, although Explorer has transaction details and logs. Do not interpret null RPC receipt as evidence deployment did not happen.

## 3. RPC / Explorer log-index discrepancy

Attempted RPC `eth_getLogs` scan:
- address: proxy above
- topic0: `0xbc7cd75a20ee27fd9adebab32041f755214dbc6bffa90cc0225b39da2e5c2d3b` (`Upgraded(address)`)
- range: 21,568,375–24,825,928
- 66 chunks of 50,000 blocks; scan completed without RPC errors
- returned zero events.

Exact-block controls:
- creation block 21,568,375, with topic filter: 0 logs
- creation block 21,568,375, proxy only without topic: 0 logs
- block 25,699,353: 1 upgrade log
- block 25,714,062: 1 upgrade log

Explorer alternative attempts:
- Legacy logs API range query returned `status: 0`, `No logs found`.
- v2 address logs endpoint returned `items: []`, `next_page_params: null`.
- However, Explorer transaction-specific endpoint for the creation transaction returned the creation `Upgraded(address)` event.

Assessment: the address/range log endpoints tested do not expose the creation event. The reason is unknown. These zero-event results are not a complete, reconcilable history and cannot establish that no upgrades occurred before 2026-11-21.

## 4. Latest-state proxy getters (read-only RPC, 2026-11-28)

| Getter | Result | Interpretation boundary |
|---|---|---|
| `getVaultId()` | `2` | Current vault/tree ID, not token ID |
| `getAssetContractAddress()` | `0x0000000000000000000000000000000000000000` | Stored base asset address is zero; not proof the vault is empty |
| `getNumberOfAssetIdentifiers()` | `1` | Current stored value; does not classify a token |

Current Explorer-verified SharedVault source describes one shared Merkle tree for ERC-20 assets. An ERC-20 token ID is the token contract address; `_tokenOf(tokenId)` rejects zero and values above `uint160`, then casts to address. ERC-721/ERC-1155 use NftCustody with asset IDs above 160 bits.

Therefore `vaultId` and `tokenId` are different. `vaultId = 2` does not mean ERC-1155. Zero `assetContractAddress` is consistent with a dynamic shared-token design. The specific token used in the historical transaction remains unknown.

These are current source observations from implementation `0x937471...`, verified by Explorer on 2026-11-27; historical attribution remains unresolved.

## 5. Historical receipt vs current source

Historical target transaction:
- method: `transferV2`
- inputs: 1
- outputs: 3
- statement length: 10
- statement[7] converts to the proxy address.

Current verified `SharedVault.sol` routes receipt shape `m == 3 && n == 1 && len == 10` to `VK_ID_ERC20_JOINSPLIT_RELAYER`; current `Erc20CoinVault.sol` defines that key constant as slot **3**. Current `checkReceiptConditions()` checks vault address at statement index 7 and ciphertext hash at the last index.

Classification:
- Exact shape match to current verified source: yes.
- Historical verifier slot 3 use on 2026-11-21: not established.
- Historical semantic assignment of statement[8] as fee: not established.
- Third output note ownership: unknown.
- Token denomination and decimals for statement[8]: unknown.

The transaction called `transferV2`, not `partialWithdrawWithRelayerFee`. Do not transfer comments about the latter function to this transaction.

## 6. Existing evidence records in the repository

Repository: `akira01111/rayls-private-transactions-research`

1. [Historical transferV2 / relayer-fee transaction review](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-public-transfer-v2-relayer-fee-2026-11-27.json)
2. [Official Enygma Public fee and relayer documentation review](https://github.com/akira01111/rayls-private-transactions-research/blob/main/sources/official-docs/enygma-public-fee-and-relayer-flow-2026-11-27.json)
3. [SharedVault ID and receipt circuit source mapping](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-shared-vault-id-and-receipt-circuit-2026-11-28.json)
4. [SharedVault post-transaction upgrade events](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-shared-vault-proxy-upgrades-2026-11-28.json)
5. [SharedVault proxy creation and initial implementation](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-shared-vault-proxy-creation-2026-11-28.json)
6. [Pre-transaction upgrade scan and RPC/Explorer discrepancy](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-shared-vault-pretransaction-upgrade-scan-2026-11-28.json)
7. [Multisig-executed SharedVault upgrade actions](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-shared-vault-multisig-upgrade-actions-2026-11-28.json)
8. [OwnerMultisig proposal structure and execution logs](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-structure-2026-11-28.json)
9. [Proposal 10 execution chronology](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-10-execution-chronology-2026-11-28.json)

The raw transaction archive and source repository have not been modified during this investigation.

## 7. Immediate next action — pending user output

The last command provided to the user queries the Explorer address transaction index:

```bash
P=0x9c5ad5e5ea5b5910e7fd1e1cc7b70ce0e4bf06c2

curl -fsS \
  "https://testnet-explorer.rayls.com/api/v2/addresses/$P/transactions" \
  -o /tmp/proxy-transactions-page1.json

python3 - <<'PY'
import json
with open("/tmp/proxy-transactions-page1.json") as f:
    d = json.load(f)
items = d.get("items", [])
print("TOTAL ITEMS:", len(items))
print("NEXT PAGE PARAMS:", d.get("next_page_params"))
for tx in items[:5]:
    print({
        "block": tx.get("block_number"),
        "hash": tx.get("hash"),
        "method": tx.get("method"),
        "from": (tx.get("from") or {}).get("hash"),
        "to": (tx.get("to") or {}).get("hash")
    })
if items:
    print("OLDEST BLOCK IN PAGE:", items[-1].get("block_number"))
PY
```

The user has **not yet returned the output** of this endpoint query. Continue from that result; do not repeat it unless necessary.

If address transactions are indexed:
- inspect `items` and `next_page_params`
- use exact returned pagination cursor fields; do not invent cursor values
- inspect proxy interactions from creation through target block
- identify possible UUPS upgrade calls/selectors and obtain transaction-specific logs for candidates
- test whether the address transaction index contains the known creation transaction before trusting completeness.

If that endpoint is empty or omits old records, stop relying on this Explorer address index and try block transaction listing, an independent archive RPC/indexer, or deployer/admin transaction history. Do not conclude no upgrade occurred.

## 8. Explorer v2 address transaction index — page 1

Endpoint:
`/api/v2/addresses/0x9c5ad5e5ea5b5910e7fd1e1cc7b70ce0e4bf06c2/transactions`

Observed response:
- items: 50
- newest block in page: 25,683,008
- oldest block in page: 24,560,687
- target transaction `0x09edab2b...25bb` appears at block 24,825,928, item index 32.
- creation transaction is not present in page 1.
- the returned `next_page_params` cursor is:
  - `index: 0`
  - `value: "0"`
  - `hash: 0xfa4ee432b2718f1f555d8c49ed0fcdfe3b930c0f93e5c39cb2171abb35013fa6`
  - `inserted_at: 2026-11-19T17:22:13.207381Z`
  - `block_number: 24560687`
  - `fee: 61384656000000000`

Important completeness warning:
- The page contains ordinary proxy calls labelled `transferV2` and one `depositV2`.
- The page's newest block (25,683,008) is earlier than known Upgraded event blocks 25,699,353 and 25,714,062.
- The two upgrade transaction hashes already observed in RPC logs were not present on this page.
- This suggests the endpoint's transaction index may omit some proxy-emitted upgrade transactions, or its indexing/order differs. Do not treat the address transaction list as a complete upgrade history until tested.
- The target transaction appearing on page 1 does prove this endpoint can return that transaction.

Immediate next action:
- Follow the exact returned cursor parameters to fetch page 2.
- Check whether pages move backward in block height and whether known upgrade transaction hashes ever appear.
- Continue toward creation block only if pagination is stable. If it omits known upgrade transactions, use it only as supplementary evidence and seek block transaction lists or an independent indexer.

## 9. Two later upgrades executed through OwnerMultisig

Explorer transaction metadata for both upgrade transactions shows the outer call destination is `0xbf099175a241194c38e977735d59ccb22596d775`, not the SharedVaultProxy. Both outer transactions are successful calls to `execute(uint256 id)`, selector `0xfe0d94c1`.

| Date UTC | Block | Outer tx | Action ID | Proxy event implementation |
|---|---:|---|---:|---|
| 2026-11-26 22:08:28 | 25,699,353 | `0xc2a566d29af6e96a8de6a9c002e20508f901e28f32c0f074f8c18c9072e13567` | 13 | `0x9644667cc096964bafb6a533d57873544fbfb956` |
| 2026-11-27 00:22:17 | 25,714,062 | `0xa8d762f12efaf8decc32918b4f32fe90db5bf8db377c156693c959ff3497250c` | 16 | `0x937471b6acdad0c77d6874d0546d6009e09cd3f0` |

The proxy-emitted `Upgraded(address)` event hash/block correlates with each outer `execute(id)` transaction. This strongly indicates multisig-mediated upgrades. Internal call traces have not yet been retrieved.

The address transaction index's first page returned 50 items, with newest block 25,683,008 and oldest block 24,560,687. It includes the target transaction at block 24,825,928 (item index 32). Its next-page cursor was:
- `index: 0`
- `value: "0"`
- `hash: 0xfa4ee432b2718f1f555d8c49ed0fcdfe3b930c0f93e5c39cb2171abb35013fa6`
- `inserted_at: 2026-11-19T17:22:13.207381Z`
- `block_number: 24560687`
- `fee: 61384656000000000`

The first page does not include the known upgrade transactions at blocks 25,699,353 and 25,714,062. The endpoint may omit multisig-executed proxy calls, so do not treat this address transaction index as a complete upgrade timeline.

**Next action:** fetch internal calls and raw traces for both multisig execution transactions, then inspect multisig metadata/source and determine whether its action history can reveal upgrades before the target transaction.

## 10. OwnerMultisig proposal structure and execution logs

Explorer metadata identifies `0xbf099175a241194c38e977735d59ccb22596d775` as verified `OwnerMultisig`, compiler `v0.8.28+commit.7893614a`, verified at `2026-11-11T11:15:18.672196Z`.

Verified ABI exposes:
- `proposalCount() -> uint256`
- `proposals(uint256 id) -> (address target, bool executed, uint256 value, bytes data)`
- `propose(address target,uint256 value,bytes data)`
- `confirm(uint256 id)`
- `execute(uint256 id)`
- events `Proposed(id, proposer, target, value, data)`, `Confirmed(id, owner)`, `Revoked(id, owner)`, `Executed(id, executor)`.

Current verified source comments say proposal IDs count upward from 0 and `proposalCount` is the next ID. Proposal struct holds target, executed flag, native value, and calldata. Source comments state proposal submission counts as the proposer's confirmation; any owner may execute after the current threshold is met. Owner set and threshold change only through multisig proposals targeting itself.

The two upgrade transaction logs include multisig `Executed(uint256,address)` with matching proposal/action IDs and executor:
- 2026-11-26 tx `0xc2a566...`: action ID 13, executor `0x71af09966cbed4434cca97c40fa38b8083548b95`.
- 2026-11-27 tx `0xa8d762...`: action ID 16, executor `0x3bffb10f6f17f15164fbc0416f1bc42c56b2c191`.

Both outer transactions call `execute(uint256 id)` on the OwnerMultisig. Both transaction-specific log endpoints also show the corresponding SharedVaultProxy `Upgraded(address)` event. Internal-transactions API returned zero items for both, so internal call traces remain unavailable.

**High-value next action:** use read-only `eth_call` on `proposalCount()` and `proposals(id)` for IDs 13 and 16, then enumerate IDs 0 through current proposalCount-1. Identify proposals whose target equals SharedVaultProxy (or an intermediary), decode proposal calldata, and find historical upgrade proposals executed before target block 24,825,928.

## 11. Historical implementation candidates from OwnerMultisig proposals

A latest-state read-only call to `proposalCount()` returned **24**. The public getter `proposals(id)` was read for IDs 0–23. Important direct SharedVaultProxy targets:

| Proposal ID | Executed (latest state) | Inner selector | Implementation argument | Execution block/time |
|---:|---|---|---|---|
| 5 | true | `0x4f1ef286` (`upgradeToAndCall(address,bytes)`) | `0x3a3f95cf53d4a0bd99d9afb3c785cd969cefdf39` | Unknown |
| 10 | true | `0x3659cfe6` (`upgradeTo(address)`) | `0xad9667049f14d1757d147f652c41dc241c57091c` | Unknown |
| 13 | true | `0x4f1ef286` | `0x9644667cc096964bafb6a533d57873544fbfb956` | Block 25,699,353; 26 Nov 2026 22:08:28 UTC |
| 16 | true | `0x4f1ef286` | `0x937471b6acdad0c77d6874d0546d6009e09cd3f0` | Block 25,714,062; 27 Nov 2026 00:22:17 UTC |

The implementation address in proposal 10 matches the address recorded in the earlier audit as the prior associated implementation (`0xad966704...`). This is an important candidate, but the `executed=true` getter is current state and does not reveal when proposal 5 or proposal 10 executed.

The currently verified OwnerMultisig source says IDs increment from zero and `proposalCount` is the next ID. Therefore IDs 5 and 10 were proposed earlier than ID 13, but **proposal creation order is not execution order**. Their execution block/time must be obtained from `Executed(id)` events or corresponding `execute(id)` transactions before concluding which implementation was active at target block 24,825,928.

New evidence record:
[OwnerMultisig historical vault upgrade candidates](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-historical-vault-upgrade-candidates-2026-11-28.json)

**Next action:** query OwnerMultisig's transaction index and paginate for outer `execute(5)` and `execute(10)`. Check index completeness against known `execute(13)` and `execute(16)` controls. Then retrieve transaction-specific logs to match `Executed(id)` and `Upgraded(address)` events.

## 12. Proposal 10 execution chronology — implementation 0xad966...

The first page of OwnerMultisig transaction history (50 items) contains:
- `propose(SharedVaultProxy, 0, upgradeTo(0xad9667049f14d1757d147f652c41dc241c57091c))` at block **23,399,866**, `2026-11-11T21:23:54Z`.
- `confirm(10)` at block **23,399,960**, `2026-11-11T21:24:51Z`.
- `execute(10)` at block **23,399,976**, `2026-11-11T21:25:01Z`, tx `0xc841126f7cf05d937967743f7db5cb80d04cf32ed1dca929aac23d952e97f3c4`.

The latest-state `proposals(10)` getter independently returned:
- target = SharedVaultProxy
- executed = true
- calldata selector `0x3659cfe6` = `upgradeTo(address)`
- implementation argument = `0xad9667049f14d1757d147f652c41dc241c57091c`.

This execution is conclusively before the target transaction (block 24,825,928; 2026-11-21 09:40:42 UTC). It establishes that `0xad966...` was installed on 2026-11-11. It does **not yet establish** that it remained active on 2026-11-21 because proposal 5 is another executed direct SharedVaultProxy upgrade:
- proposal ID 5 target = SharedVaultProxy
- selector `0x4f1ef286` = `upgradeToAndCall(address,bytes)`
- implementation argument = `0x3a3f95cf53d4a0bd99d9afb3c785cd969cefdf39`
- execution transaction/block/time still unknown.

Proposal IDs represent creation order per current verified source, not execution order. The `executed=true` getter is current state only.

New record:
[Proposal 10 execution chronology](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-10-execution-chronology-2026-11-28.json)

**Next action:** follow the exact multisig address transaction pagination cursor from page 1 (block 22,489,567; hash `0xa0d8d9fffe0c7d8a9d0d8e74974c90a715666651c58fc38716cea3a2c1583ec0`) to page 2 and locate `execute(5)`. Then check every OwnerMultisig execute transaction between block 23,399,976 and target block 24,825,928 for any direct SharedVaultProxy upgrade proposal.

## 8. Evidence discipline

Label conclusions as direct observation / verified fact, current verified source observation, official claim, inference, or unknown.

Never assert historical implementation, token identity, verifier key slot, fee denomination, or output note ownership without specific evidence.

All RPC operations described so far were read-only. No transaction has been signed or sent.


## 13. Proposal 5 execution chronology — page 2 resolved the ordering question

The OwnerMultisig transaction-index page 2 returned 19 items and no further pagination cursor. Among its decoded execute(uint256 id) entries:

- Proposal/action ID **5**: tx `0xa9409e70a24ac6898cc0213b1f1e0f0617923f47e3be3781e08c01c143fdd959`, block **22,380,723**, timestamp **2026-11-04T17:03:01Z**.
- Proposal/action ID **10**: tx `0xc841126f7cf05d937967743f7db5cb80d04cf32ed1dca929aac23d952e97f3c4`, block **23,399,976**, timestamp **2026-11-11T21:25:01Z**.
- Historical target transaction: block **24,825,928**, timestamp **2026-11-21T09:40:42Z**.

Latest-state proposals(5) getter:
- target = SharedVaultProxy
- executed = true
- selector = `0x4f1ef286` (upgradeToAndCall(address,bytes))
- implementation argument = `0x3a3f95cf53d4a0bd99d9afb3c785cd969cefdf39`.

Latest-state proposals(10) getter:
- target = SharedVaultProxy
- executed = true
- selector = `0x3659cfe6` (upgradeTo(address))
- implementation argument = `0xad9667049f14d1757d147f652c41dc241c57091c`.

**Updated chronology assessment:** the observed execute transaction order is ID 5 first, then ID 10, then the target transaction. This resolves the previous uncertainty about which proposal was executed first. If these two actions emitted their expected proxy upgrade events, ID 10's implementation `0xad966...` superseded ID 5's `0x3a3f95...` seven days before the target transaction. It is now the leading candidate for the active implementation at block 24,825,928.

**Still pending before historical attribution is final:**
1. Inspect execute(5) transaction-specific logs for OwnerMultisig Executed(id=5) and proxy Upgraded(address) with `0x3a3f95...`.
2. Inspect execute(10) transaction-specific logs for the matching proxy Upgraded(address) with `0xad966...`.
3. Check the enumerated proposal set (IDs 0–23) for any other direct or indirect upgrade path affecting SharedVaultProxy before block 24,825,928.

New record:
[Proposal 5 execution chronology](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-5-execution-chronology-2026-11-28.json)

This section supersedes the previous checkpoint statements that proposal 5's execution block/time was unknown and the previous instruction to locate execute(5).


## 14. Proposal 5 execution logs — installation confirmed

Transaction-specific Explorer logs for proposal 5 execution transaction:
`0xa9409e70a24ac6898cc0213b1f1e0f0617923f47e3be3781e08c01c143fdd959`

Endpoint: `https://testnet-explorer.rayls.com/api/v2/transactions/0xa9409e70a24ac6898cc0213b1f1e0f0617923f47e3be3781e08c01c143fdd959/logs`

Three logs were returned:

1. Log index 0, emitted by SharedVaultProxy: topic0 `0xbc7cd75a20ee27fd9adebab32041f755214dbc6bffa90cc0225b39da2e5c2d3b` (`Upgraded(address)`); indexed implementation is `0x3a3f95cf53d4a0bd99d9afb3c785cd969cefdf39`.
2. Log index 1, emitted by SharedVaultProxy: topic0 `0x7f26b83ff96e1f2b6a682f133852f6798a09c465da95921460cefb3847402498`, data encodes value 2. Its semantic label is not needed for the implementation chronology.
3. Log index 2, emitted by OwnerMultisig: topic0 `0x7271f8b3d48d26ccc839c0f424fe9e12fe4e058108b58c096c078659c7fbadf6` (`Executed(uint256,address)`); indexed action ID = 5, executor = `0x3bffb10f6f17f15164fbc0416f1bc42c56b2c191`.

**Conclusion now supported by transaction-specific logs:** proposal/action ID 5 was successfully executed and SharedVaultProxy emitted `Upgraded(address)` pointing to `0x3a3f95cf53d4a0bd99d9afb3c785cd969cefdf39` at block 22,380,723 on 2026-11-04 17:03:01 UTC. This confirms installation of the implementation encoded in proposal 5.

**Historical target status:** proposal 10 executed later on 2026-11-11 and its current proposal getter encodes `upgradeTo(0xad966...)`. Its transaction-specific proxy `Upgraded(address)` log still needs confirmation. Until that check is complete, do not yet state the target-date implementation as final.

Updated records:
- [Proposal 5 execution chronology](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-5-execution-chronology-2026-11-28.json)
- [Proposal 10 execution chronology](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-10-execution-chronology-2026-11-28.json)

Next action: inspect logs for proposal 10 execution transaction `0xc841126f7cf05d937967743f7db5cb80d04cf32ed1dca929aac23d952e97f3c4`.


## 15. Proposal 10 execution logs — second installation confirmed

Transaction-specific Explorer logs for proposal 10 execute transaction:
`0xc841126f7cf05d937967743f7db5cb80d04cf32ed1dca929aac23d952e97f3c4`

Endpoint: `https://testnet-explorer.rayls.com/api/v2/transactions/0xc841126f7cf05d937967743f7db5cb80d04cf32ed1dca929aac23d952e97f3c4/logs`

Two logs were returned:

1. Log index 0, emitted by SharedVaultProxy: topic0 `0xbc7cd75a20ee27fd9adebab32041f755214dbc6bffa90cc0225b39da2e5c2d3b` (`Upgraded(address)`); indexed implementation = `0xad9667049f14d1757d147f652c41dc241c57091c`.
2. Log index 1, emitted by OwnerMultisig: topic0 `0x7271f8b3d48d26ccc839c0f424fe9e12fe4e058108b58c096c078659c7fbadf6` (`Executed(uint256,address)`); indexed action ID = 10; executor = `0x3bffb10f6f17f15164fbc0416f1bc42c56b2c191`.

**Confirmed chronology:**
- 2026-11-04 17:03:01 UTC, block 22,380,723: Proposal 5 installed `0x3a3f95cf53d4a0bd99d9afb3c785cd969cefdf39`.
- 2026-11-11 21:25:01 UTC, block 23,399,976: Proposal 10 installed `0xad9667049f14d1757d147f652c41dc241c57091c`.
- 2026-11-21 09:40:42 UTC, block 24,825,928: historical target transaction occurred.

Among the enumerated direct SharedVaultProxy upgrade proposals (IDs 5, 10, 13, 16), IDs 13 and 16 are after the target transaction (blocks 25,699,353 and 25,714,062). Therefore `0xad966...` is the best-supported implementation at the target date based on confirmed upgrade execution chronology.

**Remaining independent check:** request the EIP-1967 implementation storage slot at historical block 24,825,928. If historical state is available, the result should match `0xad966...`. The earlier range-log index inconsistencies remain a limitation; do not claim that the absence of other events in those indexes proves no other upgrade path existed.

Updated records:
- [Proposal 10 execution chronology](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-10-execution-chronology-2026-11-28.json)
- [Historical vault upgrade candidates](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-historical-vault-upgrade-candidates-2026-11-28.json)

Next action: query historical EIP-1967 implementation storage at block 24825928.


## 16. Proposal 10 logs confirmed; historical slot read unavailable

Transaction-specific Explorer logs for execute(10) transaction:
`0xc841126f7cf05d937967743f7db5cb80d04cf32ed1dca929aac23d952e97f3c4`

Endpoint: `https://testnet-explorer.rayls.com/api/v2/transactions/0xc841126f7cf05d937967743f7db5cb80d04cf32ed1dca929aac23d952e97f3c4/logs`

Two logs were returned:
- Log index 0, emitted by SharedVaultProxy: `Upgraded(address)`; indexed implementation = `0xad9667049f14d1757d147f652c41dc241c57091c`.
- Log index 1, emitted by OwnerMultisig: `Executed(uint256,address)`; indexed action ID = 10; executor = `0x3bffb10f6f17f15164fbc0416f1bc42c56b2c191`.

This independently confirms Proposal 10 installed `0xad966...` at block 23,399,976 (2026-11-11 21:25:01 UTC). Proposal 5 was already confirmed by its own transaction-specific logs to install `0x3a3f95...` at block 22,380,723 (2026-11-04 17:03:01 UTC).

The historical target transaction is block 24,825,928 (2026-11-21 09:40:42 UTC). Enumerated direct SharedVaultProxy upgrade proposals 13 and 16 installed later implementations at blocks 25,699,353 and 25,714,062, both after the target. Therefore `0xad966...` is currently the best-supported implementation at target time based on the confirmed upgrade chronology.

### Historical EIP-1967 slot attempt

Attempted read:
- method: `eth_getStorageAt`
- proxy: `0x9c5ad5e5ea5b5910e7fd1e1cc7b70ce0e4bf06c2`
- slot: `0x360894a13ba1a3210667c828492db98dca3e2076cc3735a920a3ca505d382bbc` (EIP-1967 implementation slot)
- requested block: 24,825,927 (block immediately preceding target transaction)
- endpoint: `https://testnet-rpc.rayls.com`
- response: JSON-RPC error code `-32603`, message `state at block #24825928 is pruned`.

Classification: direct observation of an RPC historical-state availability failure. No storage value was returned. Do not interpret this as a zero slot or as evidence of another implementation.

### Remaining authorization-path check

The enumerated OwnerMultisig proposal set also contains proposals targeting SharedVaultProxy with `grantRole(bytes32,address)`: IDs 3, 4, 14, 17, 21, and 22. The grantRole selector alone does not identify the role or grantee. Before finalizing the implementation reconstruction, decode these calls and determine whether any role granted before target block 24,825,928 could authorize an independent upgrade path. IDs 14, 17, 21, and 22 must also be timestamped/ordered against the target; do not assume their IDs imply execution order.

New record:
[Historical implementation slot pruned result](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-shared-vault-historical-implementation-slot-pruned-2026-11-28.json)

Updated records:
- [Proposal 10 execution chronology](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-proposal-10-execution-chronology-2026-11-28.json)
- [Historical vault upgrade candidates](https://github.com/akira01111/rayls-private-transactions-research/blob/main/analysis/rayls-enygma/enygma-owner-multisig-historical-vault-upgrade-candidates-2026-11-28.json)

Next action: decode proposal calldata for proxy-targeted grantRole actions and compare the granted roles with the implementation's upgrade authorization logic.
