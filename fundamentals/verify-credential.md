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

# Verify Credential

The execution proof and outputs can be verified without sacrificing the confidential information used to produce the proof.

```javascript
// Import required modules from Aleo SDK.
import { 
    verifyFunctionExecution, 
    initializeWasm, 
    VerifyingKey, 
    AleoKeyProvider, 
    ProgramManager 
} from "@aleohq/sdk";
import { Execution } from "@aleohq/wasm";

// Initialize Aleo's WASM environment.
await initializeWasm();

// Define the default host for the Aleo Virtual Machine.
const defaultHost = "https://vm.aleo.org/api";

// Initialize Aleo's key provider.
const keyProvider = new AleoKeyProvider();

// Initialize the program manager with the default host, key provider, and undefined options.
const programManager = new ProgramManager(
    defaultHost,
    keyProvider,
    undefined
);

// Enable caching for the key provider.
keyProvider.useCache(true);

// Function to verify the execution of a specified function within an Aleo program.
export function verify(executionString, verifyingKeyString, program, functionName) {

    // Convert the verifying key string to a VerifyingKey object.
    const verifyingKey = VerifyingKey.fromString(verifyingKeyString);

    // Perform the function execution verification.
    const isCorrect = verifyFunctionExecution(
        Execution.fromString(executionString),
        verifyingKey,
        programManager.createProgramFromSource(program),
        functionName
    );

    // Log the verification result.
    console.log("Execution verified successfully: " + isCorrect);

    // Return the verification status.
    return isCorrect;
}
```
