# constructor

## Description

The `ZPassSDK` provides an interface for interacting with the ZPass, including program management, account handling, and network communication. It leverages WebAssembly and supports integration with Aleo's ecosystem.

### Parameters

* **`privateKey` (string)**: The private key for the Aleo account. Must start with `APrivateKey1`.
* **`host` (string, optional)**: The API host for the network client. Defaults to `https://api.explorer.provable.com/v1` if not provided.

### Example

```javascript
const sdk = new ZPassSDK({
    privateKey: 'APrivateKey1...',
    host: 'http://localhost:3030'
});
```
