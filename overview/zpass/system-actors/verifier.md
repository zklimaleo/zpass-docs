# Verifier

The Verifier offers a service and mandates that the user meets specific attribute requirements through credential verification. The focus is on authenticating user identity or claims to decide on service access.

**`Required Attribute → Verification Method → Verifier Service`**

`Age`` `**`→`**` ``Driver's License Check`` `**`→`**` ``Verifier Service`

`Academic Degree`` `**`→`**` ``Diploma Verification`` `**`→`**` ``Verifier Service`

`Credit score`` `**`→`**` ``Credit Report Review`` `**`→`**` ``Verifier Service`

`Nationality`` `**`→`**` ``Passport Scan`` `**`→`**` ``Verifier Service`



**Role and responsibilities**

Claim validation: Requests and verifies ZKP to confirm the Holder’s identity or specific claims.

**Request for proof**

Initiates a query to the Holder, requesting a ZKP for a specific identity claim.

**Verification workflow**

1. Receives the ZKP from the Holder.
2. Validates it using corresponding Aleo network protocols.
