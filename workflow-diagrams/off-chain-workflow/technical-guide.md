# Technical Guide

#### Getting Started with Aleo

Before diving into the code, initialize the Aleo SDK:

```jsx
import * as aleo from "@aleohq/sdk";
await aleo.initializeWasm();
```

This allows you to work with Aleo's functions in your application.

#### Establishing Connection to Aleo VM

For our demo, we'll connect to Aleo's VM (Virtual Machine):

```jsx
const defaultHost = "<https://vm.aleo.org/api>";
const keyProvider = new aleo.AleoKeyProvider();
const programManager = new aleo.ProgramManager(
  defaultHost,
  keyProvider,
  undefined,
);
```

#### Creating Credentials

Our demo will involve generating a credential off-chain:

#### Structure of the Credential:

```
struct Message:
    issuer (the Issuer's address)
    subject (the Holder's address)
    dob (Date of Birth)
    nationality
    expiry (Expiration date of the credential)
```

In real-world scenarios, a Holder might receive a credential like a passport from an Issuer. This passport could be verified through its native signature, proving its authenticity.

#### Verifying Credentials

The Verifier checks the credentials using Aleo programs. Here are example Aleo programs that hash credentials using different algorithms:

* Keccak: `offchain_verifier1.aleo`
* SHA-3: `offchain_verifier2.aleo`
* BHP: `offchain_verifier3.aleo`
* Poseidon: `offchain_verifier4.aleo`

These programs take the credential as input, hash it, and then use the hash to verify the signature.

#### Execution & Verification using WebAssembly (Wasm)

Aleo leverages WebAssembly (Wasm) for executing programs in a local environment:

```jsx
await initializeWasm();
```

The benefits:

* **Privacy**: Holders can execute the program locally, ensuring their private inputs remain confidential.
* **No Third-Party Trust**: Holders don't need to trust a third party to verify their credentials.

#### Verifying Execution

Finally, the Verifier uses the execution proof to ensure the program ran correctly. This doesn't reveal any credential data but verifies the proper functioning of the Aleo program.

```jsx
export function verify(executionString, verifyingKeyString, program, functionName) {...}
```

