# What is the Off-Chain?

### **Incorporating External Credentials into zPass**

The off-chain flow refers to the operations that occur outside the Aleo blockchain. These operations, can either be initiated and completed off-chain or even have their beginnings outside the Aleo ecosystem altogether.

#### **Origin of Credentials: Beyond the Aleo Ecosystem**

While we have equipped developers with the capability to generate credentials within the Aleo environment, it's essential to grasp that a credential could very well originate from an external entity. A tangible example is a passport. Issued by national authorities, passports aren't native to the Aleo or any blockchain system. However, they bear native signatures, acting as proof of authenticity.

These native signatures allow external credentials like a passport to integrate into zPass. The external credential, when presented to an Aleo program, can be processed and verified without having to record details on the blockchain.

### Journey of an Off-Chain Credential

While Aleo provides the tools to generate and manage credentials within its ecosystem, in reality, a credential might have an off-chain origin, like a government-issued passport or a university degree. These documents, although produced outside of Aleo's specific programs, can play a vital role in the system.

For instance, consider a passport. It's issued outside of any Aleo-specific program, yet its native signatures can fit smoothly into Aleo's ecosystem. Here's how:

1. **Credential Creation (Off-Chain):** A trusted entity, like a government agency, issues a passport with a native signature. This passport serves as a credential.
2. **Credential Integration:** The Holder, who possesses the passport, can introduce this credential into Aleo's system. Attributes within the passport, like date of birth or nationality, can be converted into a digital format suitable for Aleo's programs.
3. **Credential Verification:** Once integrated, the Aleo program can execute and verify the credential's authenticity. This execution yields an output (often a boolean value) that confirms if the verification was successful.
