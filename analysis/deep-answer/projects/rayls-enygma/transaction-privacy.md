# Rayls Enygma Public — transaction privacy

Status: official documentation downloaded and its visibility matrix inspected in the user's Codespace. The visibility matrix is an official product claim; it is not an independent decryption test.

## Documented visibility matrix

| Party | Can see | Cannot see |
|---|---|---|
| Anyone / explorer | Registered account address, public keys, username; public shield/unshield address, token and amount; occurrence of a shielded payment, relayer/gas data, nullifiers, commitments, and encrypted notes | Sender, recipient, amount and spent notes for the shielded payment; token moved within the shared vault |
| Recipient | Amount and token of each payment received | Sender identity from the note |
| Sender | Its own payments | Other accounts' balances and payments |
| Relayer | Publicly visible information, token used for pricing, gas fee paid to it | Sender, recipient and amount of a shielded payment |
| Auditor | Documented access to shielded transaction details including sender, recipient, amount and token | Spend keys; view access does not grant authority to spend or move users' funds |

## What is and is not shielded

Shielding, unshielding, and account registration are public activities. When tokens move into or out of a vault, the address, token, and amount are visible on-chain. A shielded payment is different: its sensitive payment details are hidden from public observers while cryptographic artifacts and encrypted note data remain visible.

This is not invisibility of the transaction itself. An observer can see that a shielded payment occurred and can inspect the public commitments, nullifiers, ciphertext-related data, relayer, and gas metadata. The documented privacy property is about hiding payment content and linkage, not eliminating all public traces.

## Evidence

1. [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what)
   - Codespace retrieval: HTTP 200; 196,863 bytes.
   - SHA-256: 17704cffaf946d917d32ec35d77b6b2c00acf2aa368b835903ca6aff9e04c0d2.
   - Local snapshots: /tmp/deep-answer-auditor/rayls.html and /tmp/deep-answer-transaction-privacy/rayls_who_sees_what.html.
2. [How Enygma Public works](https://docs.rayls.com/docs/how-enygma-public-works)
3. [Try Enygma Public on testnet](https://docs.rayls.com/docs/try-enygma-public-on-testnet)

## Evidence classification and limits

- **Official documentation claim:** public observers cannot see the sender, recipient, amount, or spent notes of a shielded payment.
- **Official documentation claim:** recipients see the amount/token received but not sender identity from the note; relayers cannot see the shielded payment parties or amount.
- **Not independently verified:** successful auditor decryption of a specific account/transaction.
- **Not historically attributed:** this visibility matrix does not prove the exact configuration or implementation used by the separate 2026-11-21 historical transaction.
- Do not infer that every on-chain Enygma operation is private: shield, unshield, and registration are explicitly public.

## Institutional relevance

Enygma Public is the clearest main-case example in this research of a shielded-payment application on a public-chain testnet that retains public cryptographic evidence and documents an auditor-access path. Its testnet status and untested auditor decryption remain material limitations.
