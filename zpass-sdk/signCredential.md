# signCredential

## Description

The `signCredential` method allows you to hash credential data and sign it with a private key. This is useful for the issuer to create digital signatures that can verify the authenticity and integrity of data.

### Parameters

* **`options` (SignCredentialOptions)**: An object containing:
  * **`data` (object)**: The data to be signed, can be any properties and values type that are supported by Leo program
  * **`hashType` (HashAlgorithm)**: The hashing algorithm to use, type can be imported from `zpass-sdk`
  * **`privateKey` (string, optional)**: Optional private key to use for signing. If not provided, uses the SDK instance's private key

### Returns

Returns a Promise that resolves to an object containing:
* **`signature` (string)**: The generated signature
* **`hash` (string)**: The hash of the data

### Example

```javascript
const { signature, hash } = await zpass.signCredential({
    data: {
      issuer: issuer,
      subject: subject,
      dob: dob,
      nationality: nationality,
      expiry: expiry,
      salt: salt,
    },
    hashType: HashAlgorithm.POSEIDON2,
  });
```