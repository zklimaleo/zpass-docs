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

# Privacy and Security with WASM

WebAssembly (WASM) is integral to zPass, designed to maximize user security and data control. By using WASM for client-side data processing, zPass eliminates unnecessary data transfers, reducing exposure risks.

**Localized Data Processing**

Utilizing WASM, zPass can execute pre-compiled programs directly on the user's device, thus retaining sensitive information within a local environment. This localized approach mitigates the risk of data exposure through network interceptions or server vulnerabilities, ensuring that user data never leaves the client-side unless explicitly intended.

**Trustless Ecosystem**

The architecture creates a trustless computing ecosystem. It minimizes dependency on third-party servers or intermediaries for data processing, thereby conferring users greater control and assurance over their data. This is especially important for maintaining data integrity and confidentiality.

**Security Advantages**

WebAssembly is engineered to enforce the same-origin and permissions security policies of the browser, which makes it an apt choice for secure, controlled execution of code. zPass leverages these inherent security features to establish a secure execution environment for user-specific applications.
