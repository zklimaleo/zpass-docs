---
cover: ../../.gitbook/assets/Tech Foundations.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Technical Foundations

#### Core mechanics

The backbone of zPass relies on zero-knowledge proofs and, more specifically, zk-SNARKS. The shift to general-purpose zero-knowledge proofs ensures greater privacy and programmability than traditional identity verification systems. Aleo’s infrastructure is secure and scalable, providing a strong foundation for zPass.

#### Aleo and zero-knowledge proofs

zPass is powered by Aleo, a developer platform extending the capabilities of traditional blockchains using the concept of the Zero-Knowledge Execution Environment (ZEXE) model.

**Aleo’s role in privacy**

Aleo’s infrastructure ensures three critical forms of privacy in zPass: private inputs, private outputs, and user privacy.&#x20;

**Aleo’s record model**

* Enables storage and encryption of user data while keeping it private in the user’s hands
* Extends from Zcash’s UTXO model, allowing for complex privacy-preserving applications
* Supports private inputs and outputs

**Decentralized private computation**

* Control shifts from centralized databases to end users
* Combines zero-knowledge proofs with off-chain execution for verifications that do not compromise data privacy
* User identity stays private
