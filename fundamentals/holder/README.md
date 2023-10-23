---
layout:
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

# Holder

### Roles and responsibilities

**Identity proofing:** Utilizes the signed credential to assert identity or specific claims.

**Record of credential**

The Holder receives an issued credential, for on-chain flow, the credential is provided on the Aleo network as an encrypted record.

**ZKP generation**

* Authorize a credential to use for verification.
* Privately input the credential into an Aleo program.
  * Execute program using wasm on local device.
  * Generate program output and an execution proof.
