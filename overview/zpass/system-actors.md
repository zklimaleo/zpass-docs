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

**Role and Responsibilities:**

Credential Generation: Creates a digital credential with required attributes like issuer address, subject address, date of birth (DOB), expiration date, etc.

Hashing: Applies cryptographic hash functions to the credential for data integrity.

Signing: Uses a private key to sign the hashed credential, ensuring its authenticity and source of issuance.

**Issuer-Aleo Integration**

* Sign credentials and provide them as inputs to the Aleo program.
* Create a tamper-proof record of identity on-chain.

#### Holder

**Definition**

The entity in possession of the signed digital credential, aiming to prove specific identity claims.

**Role and Responsibilities**

Identity Proofing: Utilizes the signed credential to assert identity or specific claims.

**Record of Credential**

The Holder receives and safely stores the issued credential on the Aleo network as an encrypted record.

**ZK-Proof Generation**

1. Selects the credential to use for verification.
2. Privately inputs the credential into a Leo program, on their local device, which generates a proof when executed.

**Verifier**

**Definition**

Entity requiring verified proof for a specific claim from the Holder.

**Role and Responsibilities**

Claim Validation: Requests and verifies ZK proofs to confirm the Holder's identity or specific claims.

**Request for Proof**

Initiates a query to the Holder, requesting a ZK proof for a specific identity claim.

**Verification Workflow**

1. Receives the ZK-proof from the Holder.
2. Validates it using corresponding Aleo network protocols.
