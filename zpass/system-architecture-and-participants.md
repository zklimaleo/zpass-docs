---
cover: ../.gitbook/assets/System Actors.png
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

# System Architecture & Participants



<figure><img src="../.gitbook/assets/Chart2.png" alt=""><figcaption></figcaption></figure>

## Issuer

The Issuer is the trusted entity that issues credentials to substantiate identity claims. The information on a credential is important, but it only truly counts when it's backed up by a trusted authority.

#### `Issuer → Credential → Claim`

`Local government`` `**`→`**` ``Driver’s license`` `**`→`**` ``Age`

`School`` `**`→`**` ``Diploma`` `**`→`**` ``Academic Degree`

`Financial bureau`` `**`→`**` ``Credit report`` `**`→`**` ``Credit score`&#x20;

`Country`` `**`→`**` ``Passport`` `**`→`**` ``Nationality`

## Holder

The Holder is the subject of the claims, represented by attributes that exist within credentials. The ability to independently validate these credentials directly correlates with greater autonomy in controlling access to this information.

#### **`Attribute → Credential → Holder`**

`Age`` `**`→`**` ``Driver's License`` `**`→`**`  ``You`

`Academic Degree`` `**`→`**` ``Diploma`` `**`→`**` ``You`

`Credit score`` `**`→`**` ``Credit Report`` `**`→`**` ``You`

`Nationality`` `**`→`**` ``Passport`` `**`→`**` ``You`

## Verifier

The Verifier offers a service and mandates that the user meets specific attribute requirements through credential verification. The focus is on authenticating user identity or claims to decide on service access.

#### **`Required Attribute → Verification Method → Verifier Service`**

`Age`` `**`→`**` ``Driver's License Check`` `**`→`**` ``Verifier Service`

`Academic Degree`` `**`→`**` ``Diploma Verification`` `**`→`**` ``Verifier Service`

`Credit score`` `**`→`**` ``Credit Report Review`` `**`→`**` ``Verifier Service`

`Nationality`` `**`→`**` ``Passport Scan`` `**`→`**` ``Verifier Service`
