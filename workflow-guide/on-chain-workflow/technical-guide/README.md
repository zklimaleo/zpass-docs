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

# Technical Guide

## On-Chain Workflow with zPass

**Initialize the Aleo Environment**

```jsx
jsxCopy codeimport * as aleo from "@aleohq/sdk";

await aleo.initializeWasm();

const defaultHost = "<https://vm.aleo.org/api>";
const keyProvider = new aleo.AleoKeyProvider();
const programManager = new aleo.ProgramManager(defaultHost, keyProvider, undefined);

keyProvider.useCache(true);
```

**Explanation**:

* **initializeWasm**: Initializes the WebAssembly environment, a prerequisite for leveraging Aleo's features.
* **AleoKeyProvider**: Manages cryptographic keys required for credential issuance, verification, and proof generation.
* **ProgramManager**: Orchestrates the lifecycle of the Aleo programs.

### **Off-Chain Credential Generation**

Create a credential with essential attributes:

```jsx
jsxCopy codeconst credential = {
  issuerAddress: "issuer_public_key",
  subjectAddress: "subject_public_key",
  attribute: "date_of_birth",
  signature: "issuer_signature"
};
```

### **On-Chain Verification through Issuer Program**

```jsx
jsxCopy codeconst issuerProgram = await programManager.loadProgram("path/to/issuer_program.aleo");
const issuerOutput = await issuerProgram.execute(credential);

// Create a transaction with execution proof and issuerOutput
const transaction = {
  executionProof: issuerOutput.executionProof,
  zpassRecord: issuerOutput.zpassRecord
};

await aleo.submitTransaction(transaction);
```

**Explanation**:

* **loadProgram**: Loads the Issuer Program.
* **execute**: Verifies the credential signature and generates a zPass, an Aleo record containing the verified credential data.
* **submitTransaction**: Submits the record and the execution proof to Aleo blockchain.

### **Holder Autonomy & Verifier Interaction**

At this point, the user has a verified credential (zPass) on-chain and can interact with various Verifier Programs.

```jsx
jsxCopy codeconst verifierProgram = await programManager.loadProgram("path/to/verifier_program.aleo");
const proof = await verifierProgram.execute(zpassRecord);

// Use proof as needed
```

**Explanation**:

* **loadProgram**: Loads the Verifier Program.
* **execute**: Takes the on-chain zPass record, executes the Verifier Program, and returns a new proof without exposing the credential.

***

#### Key Benefits:

* **Permissionless Identity Issuance**: Allows users to present credentials issued off-chain by any entity.
* **Verifiable Records**: zPass, the on-chain record, is a verified credential with an execution proof, enhancing trust.
* **User Autonomy**: Users retain control over their on-chain zPass records.
* **Privacy-Preserving Verification**: Users can interact with Verifier Programs without exposing their credentials, using the blockchain for permissionless private identity verification.
