# Rayls Enygma Public — auditor access

Status: official product documentation inspected and local terminal snapshot retrieved. No independent auditor decryption test was performed.

## Documented mechanism

- Each Enygma Public deployment has an auditor key.
- When an account registers, the wallet encrypts a copy of its view key to the deployment auditor key using ML-KEM-768 and stores it in the registry.
- The deployment auditor can use the corresponding mechanism to open account view keys and display shielded transactions.
- The view key provides read/decrypt capability, not spend authority. Spending requires the account's spend key.
- The documentation says Rayls is the auditor on the Enygma Public testnet.
- The documentation also says owner-multisig upgrades can change registry or shared-vault rules.

## Scope and control boundary

This is a deployment-scoped auditor model: the documented auditor can read shielded transaction details made available through registered view keys for that deployment. It is not the same as making transaction contents public. At the same time, auditor key custody, access procedures, and the successful decryption path are material trust assumptions.

The view-key/spend-key separation is a capability boundary, not by itself proof that no other administrative or governance mechanism can change system rules. The forensic investigation of the OwnerMultisig and SharedVault upgrade path is recorded separately.

## Evidence

1. [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what)
   - Codespace retrieval: HTTP 200; 196,863 bytes.
   - SHA-256: 17704cffaf946d917d32ec35d77b6b2c00acf2aa368b835903ca6aff9e04c0d2.
   - Relevant terminal-extracted text: deployment auditor, ML-KEM-768 view-key encryption, shielded transaction visibility, and read-not-spend separation.
2. [Enygma Public](https://docs.rayls.com/docs/enygma-public)
3. [How Enygma Public works](https://docs.rayls.com/docs/how-enygma-public-works)
4. [Try Enygma Public on testnet](https://docs.rayls.com/docs/try-enygma-public-on-testnet)

## Classification and limits

- **Official product documentation claim:** deployment-level auditor visibility through view keys encrypted to an auditor public key.
- **Official product documentation claim:** view-key read capability is separate from spend authority.
- **Not independently verified:** successful decryption by the current testnet auditor for a specific account/transaction.
- **Not immutable:** relevant contract rules are upgradeable through the owner multisig.
- The current visibility documentation does not prove the exact configuration used by the historical November 21 transaction.

## Institutional relevance

Rayls documents an explicit deployment auditor key and a read-only account-view capability. This is a more centralized, deployment-scoped audit model than Canton contract observers or Corda application reporting flows. Its practical assurance depends on key custody, registry correctness, governance, and a successful independent decryption test.
