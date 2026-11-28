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

## 8. Evidence discipline

Label conclusions as direct observation / verified fact, current verified source observation, official claim, inference, or unknown.

Never assert historical implementation, token identity, verifier key slot, fee denomination, or output note ownership without specific evidence.

All RPC operations described so far were read-only. No transaction has been signed or sent.
