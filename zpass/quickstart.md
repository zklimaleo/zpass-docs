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

# Quickstart

### Getting Started with zPass

Install zPass-SDK using

```bash
npm install zpass-sdk
```

As zPass-SDK is using wasm for its core functionality, remember to install wasm supporting packages in your project such as `vite-plugin-wasm` to make sure wasm can be run properly.

It is recommended to setup worker thread in your project to run the `zpass-sdk` properly.

A helper function called `createAleoWorker` is provided in `zpass-sdk` to initialize the worker thread. `worker.js` is the file that will be used to run the worker thread.

```javascript
import { createAleoWorker } from "zpass-sdk";

const AleoWorker = () => {
    return createAleoWorker({
        url: "worker.js",
        baseUrl: import.meta.url,
    });
};

export { AleoWorker };
```

Import `ZPassSDK` from `zpass-sdk` in your `worker.js` file to start using the SDK. An optional `initThreadPool` function is provided to enable multi-threading and improve performance.

```javascript
import { ZPassSDK, initThreadPool } from "zpass-sdk";

await initThreadPool();
```

### ZPass SDK Methods References

Please refer to [overview](../zpass-sdk/overview/ "mention") for the methods references of `zpass-sdk`.

### Example Usage

For example on how to use `zpass-sdk`, please refer to [step-by-step-guide.md](../example-usage/step-by-step-guide.md "mention").
