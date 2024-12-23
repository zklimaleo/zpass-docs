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

# Off-chain flow

The off-chain flow offers a path to ensure privacy and trust without depending on the blockchain. These operations can either be initiated and completed off-chain or have their beginnings outside the Aleo ecosystem.

<figure><img src="../../.gitbook/assets/offchain.png" alt=""><figcaption></figcaption></figure>

Let's break it down into two main sections:

#### Credential Generation (Off-chain)

While zPass provides the tools to generate and manage credentials on the Aleo blockchain, a credential might have an off-chain origin, like a government-issued passport or a university degree. Although produced outside of Aleo's specific programs, these documents can still play a role in zPass.

For instance, consider a passport. Issued by national authorities, passports aren't native to Aleo or any other blockchain system, yet their native signatures allow them to integrate into zPass. Here's how it works:

1. **User Requests a Credential:** An entity (or user) approaches a recognized issuer, like a government agency, for a credential.
2. **Credential Generation by the Issuer:** The issuer, after due verification, creates a digital credential (like a passport) with a native signature for the user.

#### Holder Presentation and Aleo Verification (Off-chain)

1. **Credential Integration:** The Holder who possesses the credential can introduce this credential into the zPass system. Attributes within the passport, like date of birth or nationality, can be converted into a digital format suitable for Aleo's programs.
2. **Local Execution with WebAssembly (Wasm):** To ensure privacy, zPass leverages Wasm, allowing users to run the Aleo program locally. This ensures the user never reveals private inputs or trusts a third party implicitly.
3. **Program Execution and Output:** The program processes the credential (for example by hashing attributes) and produces an output. This output, coupled with an execution proof, does not reveal the credential's data yet acts as verifiable proof that the program ran successfully with the provided credentials.
