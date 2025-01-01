# issueZPass

## Description

The `issueZPass` method allows you to issue a new ZPass credential on-chain. This method handles the on-chain interaction for creating a new ZPass credential.

### Parameters

* **`options` (OnChainOptions)**: An object containing the necessary parameters for on-chain interaction:
  * **`programName` (string)**: The Aleo program name
  * **`functionName` (string)**: Name of the function to execute
  * **`inputs` (string\[])**: Array of input parameters for the function
  * **`fee` (number)**: Transaction fee in microcredits
  * **`privateFee` (boolean)**: Whether to use private fee
  * **`feeRecord` (string, optional)**: Record for private fee payment if private fee is used

### Returns

Returns a Promise that resolves to a string containing the transaction ID of the issued ZPass.

* **`transactionId` (string)**: The transaction ID of the issued ZPass

### Example

```javascript
const transactionId = await zpass.issueZPass({
    programName,
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
    fee: 300000,
    privateFee: false,
  });
```
