# Step-by-step Guide

## Setup

1. Install `zPass-SDK` using `npm install zpass-sdk.`
2. As `zPass-SDK` is using wasm for core functionality, install wasm supporting packages such as `vite-plugin-wasm` to make sure wasm can be run properly.
3. Create a worker directory in your project.
4. Create an `AleoWorker.js` file, import `createAleoWorker()` helper function to help initialize and manage workers.
5. The `createAleoWorker()` takes an argument of an object with 2 values which are `URL` and optional `baseURL`, the url here is referring to the location of `worker.js` file that we are going to define our zPass functions in later. For example, if the `worker.js` is located at the same location as the `AleoWorker.js` file, the arguments of `createAleoWorker()` will be `{“worker.js”, import.meta.url}`. The `import.meta.url` will return the absolute URL of the current module regardless of how the application is deployed or served.

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

6. Move on to create a new `worker.js` file to build zPass functions in worker using `zPass-SDK`.
7. In `worker.js` file, import and call `initThreadPool()` to initialize a thread pool of Workers. This enables multi-threading, which significantly improves performance.
8. Then proceed to create own zPass functions using `zPass-SDK`, these functions will be later exposed to the main threat using `expose()` from `comlink`. The `expose()` method takes an argument of an object with all the functions defined in `workers.js`.

## Using zPass

1. (Optional) Import `initThreadPool` to initialize a thread pool of workers to enable multi-threading and improve performance.
2. Import `ZPassSDK` into `worker.js`, initialize ZPassSDK with user `privateKey` and optional `host` url to connect to the rpc node of Aleo network.

```javascript
const sdk = new ZPassSDK({
    privateKey: privateKey,
    host: host
});
```

3. Import `expose` from `comlink` to expose functions that are created in `worker.js` later.
4. To start using zPass on-chain, a zPass program must be deployed onto the network or use any zPass program that has been deployed. Check out this [guide](../zpass/background.md) on how to write a zPass program to prove certain credentials requirements.
5. Once a zPass program is deployed on-chain, the first thing to do is to get the issuer to sign the credentials defined in the zPass program so that the users can issue themselves an on-chain zPass later.
6. For example, first create a function called `testZPass()` and in the scope of it, let’s use the `signCredential` method from ZPassSDK.
7. The `signCredential` method takes an argument as an object with fields:
   1. `data`: A credential object with properties and respective values same as defined in the deployed zPass program. Note that the name of each property must match the name of the field in the credential struct from the zPass program. The value must be in string type and appended with Aleo type suffix such as u32 in order to be able to parse correctly.
   2. `hashType`: Pick supported hash algorithm to use for hashing the data, type HashAlgorithm can be imported from zpass-sdk.
   3. `privateKey?`: An optional private key to switch using if the issuer account private key is not used during initialization of ZPassSDK.
8. `signCredential` will return an object that contains signature and hash in string type, signature will be required as one of the inputs later during proveOffChain, proveOnChain or issueZPass.

```javascript
const { signature } = await sdk.signCredential({
    data: {
      issuer: "aleo1rhgdu77hgyqd3xjj8ucu3jj9r2krwz6mnzyd80gncr5fxcwlh5rsvzp9px",
      subject: "aleo172s23z4lw3z3ruwc92dgukq8s0v3249jg28zsldq6a0adpw7c5gqfnkla2",
      dob: "19990301u32",
      nationality: "2148979field",
      expiry: "20250301u32",
      salt: "231scalar"
    },
    hashType: HashAlgorithm.POSEIDON2
  }); 
```

9. After that, we can use the `issueZPass` method from ZPassSDK. Remember to initialize ZPassSDK before using its method.
10. The `issueZPass` method takes an argument as an object with fields:
    1. `programName`: The name of the program to call in string type, which is the name of a zPass program that has been deployed on-chain with the suffix of .aleo.
    2. `functionName`: The name of the calling function in string type.
    3. `privateFee`: To spend fee from private records or not, either true or false.
    4. `inputs`: An array of strings which are the inputs to the program function.
    5. `fee`: Fee to spend in microcredit, in number type.
    6. `feeRecord?`: Optional fee records to pass for program execution if privateFee is true.
11. The `issueZPass` method will return `transactionId` once successfully.
12. In our example, by following the parameters of issue transition in `verify_poseidon2_zpass.aleo` program this will be:

```javascript
const txId = await sdk.issueZPass({
    programName: "verify_poseidon2_zpass.aleo",
    functionName: "issue",
    privateFee: false,
    inputs: [
      signature,
      `{
        issuer: aleo1rhgdu77hgyqd3xjj8ucu3jj9r2krwz6mnzyd80gncr5fxcwlh5rsvzp9px,
        subject: aleo172s23z4lw3z3ruwc92dgukq8s0v3249jg28zsldq6a0adpw7c5gqfnkla2,
        dob: 19990301u32,
        nationality: 2148979field,
        expiry: 20250301u32
      }`,
      `{
        salt: 231scalar
      }`
    ],
    fee: 3000,
}); 

```

13. Then return the `txId` back to the main application.&#x20;
14. To expose the `testZPass` function that we just created, use `expose` from `comlink` to expose it as a worker method like `expose({ testZPass })`; .

## Test running ZPass worker method

1. To try to run the `testZpass()` worker method that we just created, simply import `AleoWorker()` from `AleoWorker.js`, create an instant using `AleoWorker()` then call `testZPass()` method from that instant.
2. To test it in the local development network, check out how to set it up [here](https://developer.aleo.org/guides/leo/testing#local-testing-with-network).

```javascript
import { AleoWorker } from "./workers/AleoWorker.js";

const aleoWorker = AleoWorker();

const result = await aleoWorker.testZPass({
      privateKey: privateKey,
      host: hosturl
})
```
