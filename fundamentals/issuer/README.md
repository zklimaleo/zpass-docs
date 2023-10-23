---
cover: ../../.gitbook/assets/Issuer.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: false
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Issuer

## Role and responsibilities

**Credential generation**: Creates a digital credential with required attributes like issuer address, subject address, date of birth (DOB), and expiration date.

**Hashing**: Applies cryptographic hash functions to the credential for data integrity.

**Signing**: Uses private key to sign the hashed credential, ensuring its authenticity and source of issuance.

**Issuer–Aleo integration**

* Sign credentials and provide them to the user.
* Sign credentials and provide them as inputs to an Aleo program&#x20;
  * Create an encrypted tamper-proof record of the credential on-chain.
