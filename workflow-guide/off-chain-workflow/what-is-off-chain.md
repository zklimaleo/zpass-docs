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

# What is the Off-Chain Flow?

The off-chain flow refers to the operations that occur outside the Aleo blockchain. These operations, can either be initiated and completed off-chain or even have their beginnings outside the Aleo ecosystem altogether.

### **Origin of Credentials: Beyond the Aleo Ecosystem**

While Aleo provides the tools to generate and manage credentials within its ecosystem, in reality, a credential might have an off-chain origin, like a government-issued passport or a university degree. These documents, although produced outside of Aleo's specific programs, can play a vital role in the system.

For instance, consider a passport. Issued by national authorities, passports aren't native to the Aleo or any blockchain system, yet their native signatures can fit smoothly into Aleo's ecosystem. These native signatures allow external credentials to integrate into zPass. Here's how:

1. **Credential Creation (Off-Chain):** A trusted entity, like a government agency, issues a passport with a native signature. This passport serves as a credential.
2. **Credential Integration:** The Holder, who possesses the credential, can introduce this credential into the zPass system. Attributes within the passport, like date of birth or nationality, can be converted into a digital format suitable for Aleo's programs.
3. **Credential Verification:** Once integrated, the Aleo program can execute and verify the credential's authenticity. This execution yields an output (often a boolean value) that confirms if the verification was successful.