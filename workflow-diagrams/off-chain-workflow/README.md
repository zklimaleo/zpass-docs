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

# Off-chain Workflow

<figure><img src="../../.gitbook/assets/offchain.png" alt="" width="563"><figcaption></figcaption></figure>

## zPass **Off-Chain Flow**

Let's break it down into two main sections:

1. **Credential Generation (Off-chain)**
2. **Holder Presentation and Aleo Verifier Process**

The off-chain flow offers a path to ensure privacy and trust without depending on the blockchain.

1. **User Requests a Credential**: An entity (or user) approaches a recognized issuer for a credential.
2. **Credential Generation by the Issuer**: The issuer, after due verification, creates a digital credential for the user, we refer to this as a zPass, though, this step can happen entirely outside the Aleo ecosystem.
3. **Credential Integration with Aleo**: The user presents their credential (like a passport) to an Aleo program. The program doesn't record the credential details but processes it. For instance, it can hash the attributes using methods such as psd2, keccak, sha, or bhp in order to verify a signature.
4. **Program Execution and Output Generation**: Once processed, the program runs and produces an output. Crucially, this output, coupled with an execution proof, does not reveal the credential's data. Yet, it acts as a verifiable testament that the program ran with the said credentials.
5. **Local Execution with WebAssembly (Wasm)**: To further the cause of privacy, Aleo leverages Wasm, allowing users (holders of credentials) to run the program locally. This local execution ensures the user never reveals private inputs or trusts a third party implicitly.
