# proveOffChain

## Description

The `proveOffChain` method generates an off-chain proof for a ZPass credential, executing the program locally without submitting to the blockchain. The program can be both deployed on-chain or a local program that is not deployed on-chain but is provided and agreed upon by all the involved parties (issuer, user, verifier).

### Parameters

* **`options` (ProveOffChainOptions)**: An object containing:
  * **`localProgram` (string)**: The Aleo program source code
  * **`functionName` (string)**: Name of the function to execute
  * **`inputs` (string\[])**: Array of input parameters for the function
  * **`offlineQuery` (OfflineQuery, optional)**: An optional offline query object used to insert the global state root and state paths needed to create a valid inclusion proof offline.

### Returns

Returns a Promise that resolves to an object containing:

* **`outputs` (string\[])**: Array of function outputs
* **`execution` (string)**: The execution trace
* **`verifyingKey` (string)**: The verifying key for the proof

### Example

```javascript
const { outputs, execution, verifyingKey } = await zpass.proveOffChain({
    localProgram: programSource,
    functionName: functionName,
    inputs: [signature, `{
      issuer: ${issuer},
      subject: ${subject},
      dob: ${dob},
      nationality: ${nationality},
      expiry: ${expiry}
    }`,
      `{ salt: ${salt} }`,
    ],
});
```
