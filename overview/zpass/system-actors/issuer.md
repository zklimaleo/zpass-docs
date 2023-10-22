# Issuer

The Issuer is the trusted entity that issues credentials to substantiate identity claims. The information on a credential is important, but it only truly counts when it's backed up by a trusted authority.

#### `Issuer → Credential → Claim`

`Local government`` `**`→`**` ``Driver’s license`` `**`→`**` ``Age`

`School`` `**`→`**` ``Diploma`` `**`→`**` ``Academic Degree`

`Financial bureau`` `**`→`**` ``Credit report`` `**`→`**` ``Credit score`&#x20;

`Country`` `**`→`**` ``Passport`` `**`→`**` ``Nationality`

**Role and responsibilities**

Credential generation: Creates a digital credential with required attributes like issuer address, subject address, date of birth (DOB), and expiration date.

Hashing: Applies cryptographic hash functions to the credential for data integrity.

Signing: Uses private key to sign the hashed credential, ensuring its authenticity and source of issuance.

**Issuer–Aleo integration**

* Sign credentials and provide as inputs to the Aleo program.
* Create a tamper-proof record of identity on-chain.
