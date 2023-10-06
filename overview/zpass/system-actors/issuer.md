# Issuer

### **Issuer**

**Definition**

The Issuer is the entity accountable for generating, hashing, and signing digital credentials.

**Role and Responsibilities**

_Credential Generation_: Creates a digital credential with required attributes like issuer address, subject address, date of birth (DOB), expiration date, etc.

_Hashing_: Applies cryptographic hash functions to the credential for data integrity.

_Signing_: Uses its private key to sign the hashed credential, ensuring its authenticity.

**Issuer-Aleo Integration**

1. Sign credentials and provide them as inputs to the Aleo program.
2. Create an encrypted, tamper-proof record of identity on-chain.
