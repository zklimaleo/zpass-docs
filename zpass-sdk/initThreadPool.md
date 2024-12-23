# initThreadPool

## Description

The `initThreadPool` method initializes a thread pool of Workers to enable multi-threading, which significantly improves performance.

### Returns

Returns a Promise that resolves when the thread pool has been successfully initialized.

### Example

```javascript
await initThreadPool();
```