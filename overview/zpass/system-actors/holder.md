# Holder

The Holder is the subject of the claims, represented by attributes that exist within credentials. The ability to independently validate these credentials directly correlates with greater autonomy in controlling access to this information.



**`Attribute → Credential → Holder`**

`Age`` `**`→`**` ``Driver's License`` `**`→`**`  ``You`

`Academic Degree`` `**`→`**` ``Diploma`` `**`→`**` ``You`

`Credit score`` `**`→`**` ``Credit Report`` `**`→`**` ``You`

`Nationality`` `**`→`**` ``Passport`` `**`→`**` ``You`



**Role and responsibilities**

Identity proofing: Utilizes the signed credential to assert identity or specific claims.

**Record of credential**

The Holder receives and safely stores the issued credential on the Aleo network as an encrypted record.

**ZKP generation**

1. Selects a credential to use for verification.
2. Privately inputs the credential into a Leo program, on their local device, which generates a proof when executed.
