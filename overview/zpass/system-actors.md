---
cover: ../../.gitbook/assets/System Actors.png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
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

# System Actors

#### Issuer

**Definition**

The Issuer is the entity accountable for generating, hashing, and signing digital credentials.

**Role and responsibilities**

Credential generation: Creates a digital credential with required attributes like issuer address, subject address, date of birth (DOB), and expiration date.

Hashing: Applies cryptographic hash functions to the credential for data integrity.

Signing: Uses private key to sign the hashed credential, ensuring its authenticity and source of issuance.

**Issuer–Aleo integration**

* Sign credentials and provide as inputs to the Aleo program.
* Create a tamper-proof record of identity on-chain.

#### Holder

**Definition**

Entity in possession of the signed digital credential, aiming to prove specific identity claims.

**Role and responsibilities**

Identity proofing: Utilizes the signed credential to assert identity or specific claims.

**Record of credential**

The Holder receives and safely stores the issued credential on the Aleo network as an encrypted record.

**ZKP generation**

1. Selects a credential to use for verification.
2. Privately inputs the credential into a Leo program, on their local device, which generates a proof when executed.

**Verifier**

**Definition**

Entity requiring verified proof for a specific claim from the Holder.

**Role and responsibilities**

Claim validation: Requests and verifies ZKP to confirm the Holder’s identity or specific claims.

**Request for proof**

Initiates a query to the Holder, requesting a ZKP for a specific identity claim.

**Verification workflow**

1. Receives the ZKP from the Holder.
2. Validates it using corresponding Aleo network protocols.
