# getZPassRecord

## Description

The `getZPassRecord` method retrieves and decrypts a ZPass record from a transaction on the blockchain.

### Parameters

* **`transactionId` (string)**: The ID of the transaction containing the ZPass record

### Returns

Returns a Promise that resolves to a string containing the decrypted record data.

### Example

```javascript
const record = await zpass.getZPassRecord("at1xyz...");
```

### Errors

Throws `SDKError` if:
- No outputs are found in the transaction
- No record is found in the transaction outputs 