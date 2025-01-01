# createAleoWorker

## Description

The `createAleoWorker` method creates a new Web Worker instance for handling Aleo computations. This is useful for offloading heavy cryptographic operations to a separate thread to avoid blocking the main thread.

### Parameters

* **`options` (CreateAleoWorkerOptions)**: An object containing:
  * **`url` (string)**: URL of the worker script file
  * **`baseUrl` (string, optional)**: Base URL to resolve the worker script URL against

### Returns

Returns a wrapped Worker instance configured for Aleo operations using Comlink.

### Example

```javascript
import { createAleoWorker } from "zpass-sdk";

const AleoWorker = () => {
    return createAleoWorker({url: "worker.js", baseUrl: import.meta.url});
};

export { AleoWorker };
```
