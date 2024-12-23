# proveOnChain

## Description

The `proveOnChain` method generates an on-chain proof for a ZPass credential.

### Parameters

* **`options` (OnChainOptions)**: An object containing:
  * **`program` (string)**: The Aleo program source code
  * **`functionName` (string)**: Name of the function to execute
  * **`inputs` (string[])**: Array of input parameters for the function
  * **`fee` (number, optional)**: Transaction fee in microcredits
  * **`password` (string, optional)**: Password for key encryption

### Returns

Returns a Promise that resolves to a string containing the transaction ID of the proof.

### Example

```javascript
const transactionId = await zpass.proveOnChain({
    program: programSource,
    functionName: "prove_credential",
    inputs: ["record1234", "2u32"],
    fee: 1000000
});
``` 