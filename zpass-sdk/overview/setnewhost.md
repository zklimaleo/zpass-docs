# setNewHost

## Description

The `setNewHost` method allows you to update the host URL for the `ProgramManager`. This is useful if the API endpoint for your Aleo network changes or if you need to switch between different environments (e.g., staging, production).

### Parameters

* **`host` (string)**: The new host URL to be set for the `ProgramManager`. It must be a valid URL.

### Example&#x20;

```javascript
zpassSdk.setNewHost('http://localhost:3030');
```
