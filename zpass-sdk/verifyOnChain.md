# verifyOnChain

## Description

The `verifyOnChain` static method verifies an on-chain ZPass proof by checking the transaction on the blockchain.

### Parameters

* **`options` (VerifyOnChainOptions)**: An object containing:
  * **`transactionId` (string)**: The ID of the transaction to verify
  * **`url` (string, optional)**: Custom API endpoint URL (defaults to "https://api.explorer.provable.com/v1")

### Returns

Returns a Promise that resolves to an object containing:
* **`hasExecution` (boolean)**: Whether the transaction contains an execution, only true if the transaction has a valid execution finalized on-chain (meaning the transaction proof is valid).
* **`outputs` (Output[])**: Array of transaction outputs

### Example

```javascript
const result = await ZPass.verifyOnChain({
    transactionId: "at1xyz...",
    url: "http://localhost:3030"
});
``` 