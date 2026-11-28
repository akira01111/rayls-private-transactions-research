# Stage 3 — Enygma Public self-verification checklist

Status: **pending user-submitted private payment**. Historical transaction 0x09edab2b…25bb is not a substitute for this requirement.

## Test environment

- Wallet: https://enygma-testnet.rayls.com
- Network: Rayls Public Chain Testnet
- Chain ID: 7295799
- Explorer: https://testnet-explorer.rayls.com
- Tokens: test USDr and test RLS with no real value
- Documented testnet auditor: Rayls

Sources:
- [Try Enygma Public on testnet](https://docs.rayls.com/docs/try-enygma-public-on-testnet)
- [Enygma Public](https://docs.rayls.com/docs/enygma-public)

## User-run steps

- [ ] Open the official testnet wallet and create a dedicated test account using a passkey, or connect an account intended only for testnet experimentation.
- [ ] Obtain only the test tokens supplied by the setup/faucet.
- [ ] Register the account. Registration publishes the account's public keys and username and stores an auditor-encrypted view-key copy according to the official flow.
- [ ] Register a recipient account. It must be registered to receive a shielded payment.
- [ ] Shield test RLS. The documented guide says shielded payments pay their gas from shielded RLS.
- [ ] Send a small test payment to the registered recipient. Review the wallet's preview of public, shielded, and auditor-visible information before approving.
- [ ] The user signs the transaction in their own wallet/passkey and submits it. No assistant or research agent should sign or submit on the user's behalf.
- [ ] Copy the transaction hash and open it in the testnet explorer.
- [ ] Preserve the receipt, block number/time, transaction method, public sender/relayer information, and visible event/log data.
- [ ] Compare the explorer's public view with the wallet's stated privacy preview. Do not claim independent auditor decryption unless that has separately been authorized and tested.

## Evidence to preserve

| Field | Record |
|---|---|
| Sender account label | |
| Recipient account label | |
| Test token and amount | |
| Transaction hash | |
| Block and timestamp | |
| Method / selector | |
| Public from / to | |
| Nullifier / commitment / encrypted-note events | |
| What explorer visibly reveals | |
| What explorer does not reveal | |
| Wallet preview vs observed result | |
| Any discrepancy or error | |

## Safety and evidence boundaries

- Use test tokens only; do not bridge or spend real-value assets for this exercise.
- Never share a seed phrase, passkey, spending key, viewing key, or private auditor credentials in chat or in repository evidence.
- A public explorer inspection verifies public transaction evidence, not successful auditor decryption.
- Do not label this stage complete until the user's own successful shielded payment and its transaction evidence have been inspected and saved.
