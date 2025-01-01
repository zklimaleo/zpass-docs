# verifyOffChain

### Description

The `verifyOffChain` static method verifies an off-chain ZPass proof locally without accessing the blockchain.

### Parameters

* **`options` (VerifyOffChainOptions)**: An object containing:
  * **`execution` (string)**: The execution trace to verify, output of `proveOffChain`
  * **`program` (string)**: The Aleo program source code
  * **`functionName` (string)**: Name of the function that was executed
  * **`inputs` (string\[], optional)**: Array of input parameters used, must be provided if `verifyingKey` is not provided
  * **`verifyingKey` (string, optional)**: The verifying key for the proof, must be provided if `inputs` is not provided
  * **`url` (string, optional)**: Custom API endpoint URL, for keys synthesizing purpose

### Returns

Returns a Promise that resolves to a boolean indicating whether the proof is valid.

### Example

```javascript
const isValid = await ZPass.verifyOffChain({
    execution: executionTrace,
    program: programSource,
    functionName: "verify_credential",
    verifyingKey: verifyingKey,
});
```

### Notes

Either `inputs` or `verifyingKey` must be provided. If both are provided, `verifyingKey` takes precedence.

If `verifyingKey` is not provided, the SDK will synthesize the verifying key from the inputs and the program.

Synthesizing the verifying key is a computationally expensive operation, so it is recommended to provide the verifying key if possible.
