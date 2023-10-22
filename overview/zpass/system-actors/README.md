---
cover: ../../../.gitbook/assets/System Actors.png
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

## Issuer

The function of a credential is to provide verifiable evidence supporting your claims. The information on a credential is important, but it only truly counts when it's backed up by a trusted authority, also known as the Issuer.

#### `Claim → Credential → Issuer`

`Your age → Your driver’s license → Your local government`

`Your education → Your diploma → Your school`

`Your credit score → Your credit report → Your financial bureau`

`Your citizenship → Your passport → Your country`

## Holder

The Holder is the subject of the credentials, the person whose identity, or other claims, are being verified. The ability to independently validate these credentials directly correlates with greater autonomy in controlling access to this information.

**`Credential → Attribute → Holder`**

`Driver's License`` `**`→`**` ``Age`` `**`→`**` ``You`

`Education`` `**`→`**` ``Diploma`` `**`→`**` ``You`

`Financial history`` `**`→`**` ``Credit Report`` `**`→`**` ``You`

`Citizenship`` `**`→`**` ``Passport`` `**`→`**` ``You`

## Verifier

The Verifier is the party offering a service that necessitates credential verification from the Holder. The focus is on authenticating the Holder's identity or claims to decide on service access.

**`Verifier → Required Attribute → Validation Method`**

`Service → Age Requirement → Driver's License Check`

`Service → Educational Qualification → Diploma Verification`

`Service → Financial Standing → Credit Report Review`

`Service → Citizenship Status → Passport Scan`
