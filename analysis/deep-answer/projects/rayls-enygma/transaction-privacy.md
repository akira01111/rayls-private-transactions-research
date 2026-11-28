# Rayls Enygma Public — transaction privacy

Status: current official documentation downloaded from Rayls and its visibility matrix inspected in the user's Codespace.

## Visibility matrix

| Party | Can see | Cannot see |
|---|---|---|
| Anyone / explorer | Registered account address, public keys, username; shield/unshield address, token and amount; occurrence of shielded payment, relayer, gas fee, nullifiers, commitments and encrypted notes | Sender, recipient, amount and spent notes for shielded payment; token moved in shared vault |
| Recipient | Amount and token of each payment received | Sender identity from the note |
| Sender | Its own payments | Other accounts' balances and payments |
| Relayer | Publicly visible information, token used for its pricing, gas fee paid to it | Sender, recipient and amount of a shielded payment |
| Auditor | Every shielded transaction decrypted: sender, recipient, amount, token; invites/claims and Foundation fees | Spend keys; cannot spend or move users' funds |

## Important boundary

Shielding, unshielding and registering are public activities. When public tokens move into or out of a vault, the address, token and amount are visible on-chain. A shielded payment is different: its sensitive payment details are hidden from public observers, while encrypted note data and commitments remain visible.

## Evidence

1. [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what)
   - Codespace retrieval: HTTP 200; 196,863 bytes.
   - SHA-256: 17704cffaf946d917d32ec35d77b6b2c00acf2aa368b835903ca6aff9e04c0d2.
   - Local snapshots: /tmp/deep-answer-auditor/rayls.html and /tmp/deep-answer-transaction-privacy/rayls_who_sees_what.html.
   - Terminal extraction includes the full “What each party can see” table and details on public shielding/unshielding.

2. [How Enygma Public works](https://docs.rayls.com/docs/how-enygma-public-works)

## Classification

- Official documentation claim: public observers can see ciphertext/commitment/nullifier-related data, but not the private parties and values of a shielded payment.
- Official documentation claim: recipients see amount/token for their payments, but notes do not carry sender identity.
- Official documentation claim: relayer cannot see sender, recipient, or amount of shielded payment.

## Limitations

- Documentation claims are not the same as an independent decryption test.
- The file does not prove the exact visibility configuration of the historical November 21 transaction investigated in the Rayls forensic work.
- Do not infer that every on-chain action is private: shield, unshield, and registration are explicitly public.