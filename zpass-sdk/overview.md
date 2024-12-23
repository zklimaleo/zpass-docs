# ZPass SDK methods overview

The ZPass SDK provides a comprehensive set of methods for interacting with ZPass credentials on the Aleo blockchain.

## Core Operations

### Credential Management
- [signCredential](./signCredential.md) - Sign credential data with a private key
- [issueZPass](./issueZPass.md) - Issue a new ZPass credential on-chain
- [getZPassRecord](./getZPassRecord.md) - Retrieve and decrypt a ZPass record from the blockchain

### Proof Operations
- [proveOnChain](./proveOnChain.md) - Generate an on-chain proof for a ZPass credential
- [proveOffChain](./proveOffChain.md) - Generate an off-chain proof locally
- [verifyOnChain](./verifyOnChain.md) - Verify an on-chain ZPass proof
- [verifyOffChain](./verifyOffChain.md) - Verify an off-chain ZPass proof locally

## Worker Management
- [createAleoWorker](./createAleoWorker.md) - Create a Web Worker for Aleo computations
- [initThreadPool](./initThreadPool.md) - Initialize a thread pool for improved performance

## Getting Started
For a quick introduction to using the SDK, check out our [Quickstart Guide](../zpass/quickstart.md).
