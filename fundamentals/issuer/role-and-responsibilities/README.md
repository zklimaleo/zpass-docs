# Role and responsibilities

**Credential generation**: Creates a digital credential with required attributes like issuer address, subject address, date of birth (DOB), and expiration date.

**Hashing**: Applies cryptographic hash functions to the credential for data integrity.

**Signing**: Uses private key to sign the hashed credential, ensuring its authenticity and source of issuance.

**Issuer–Aleo integration**

* Sign credentials and provide as inputs to the Aleo program.
* Create a tamper-proof record of identity on-chain.
