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

# What is Off-Chain?

The off-chain flow refers to the operations that occur outside the Aleo blockchain. These operations, can either be initiated and completed off-chain or even have their beginnings outside the Aleo ecosystem altogether.

### **Origin of Credentials: Beyond the Aleo Ecosystem**

While zPass provides the tools to generate and manage credentials on the Aleo blockchain, a credential might have an off-chain origin, like a government-issued passport or a university degree. These documents, although produced outside of Aleo's specific programs, can still play a role in zPass.

For instance, consider a passport. Issued by national authorities, passports aren't native to the Aleo or any blockchain system, yet their native signatures allow them to integrate into zPass. Here's how:

1. **Credential Creation (Off-Chain):** A trusted entity, like a government agency, issues a passport with a native signature. This passport serves as a credential.
2. **Credential Integration:** The Holder, who possesses the credential, can introduce this credential into the zPass system. Attributes within the passport, like date of birth or nationality, can be converted into a digital format suitable for Aleo's programs.
3. **Credential Verification:** Once integrated, the Aleo program can execute and verify the credential's authenticity. This execution yields an output (often a boolean value) that confirms if the verification was successful coupled with a ZKP.
