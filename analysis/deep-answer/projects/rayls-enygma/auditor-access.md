# Rayls Enygma Public — auditor access

Status: official product documentation inspected and local terminal snapshot retrieved. No independent decryption test was performed.

## Documented mechanism

- Each deployment has an auditor key.
- When an account registers, the wallet encrypts a copy of its view key to the deployment auditor key using ML-KEM-768 and stores it in the registry.
- The deployment auditor can use the corresponding mechanism to open account view keys and display shielded transactions.
- The view key provides read/decrypt capability, not spend authority. Spending requires the account spend key.
- The documentation says the Rayls team is the auditor on testnet.
- The documentation also states that owner multisig upgrades can change registry or shared-vault rules.

## Evidence

1. [Who sees what in Enygma Public](https://docs.rayls.com/docs/enygma-public-who-sees-what)
   - Codespace retrieval: HTTP 200; 196,863 bytes.
   - SHA-256: 17704cffaf946d917d32ec35d77b6b2c00acf2aa368b835903ca6aff9e04c0d2.
   - Relevant terminal-extracted text: deployment auditor, ML-KEM-768 view-key encryption, every shielded transaction visibility, and read-not-spend separation.

2. [Enygma Public](https://docs.rayls.com/docs/enygma-public)
3. [How Enygma Public works](https://docs.rayls.com/docs/how-enygma-public-works)

## Classification

- Official product documentation claim: deployment-level auditor visibility.
- Official product documentation claim: view-key read capability is separate from spend authority.
- Not independently verified: successful decryption by the current testnet auditor of a specific account/transaction.
- Not immutable: relevant contract rules are upgradeable through the owner multisig.

## Open questions

- Compare the current testnet registry/auditor configuration against the documentation using read-only RPC.
- Do not request, expose, or use private auditor credentials. No decryption should be attempted without explicit authorization.