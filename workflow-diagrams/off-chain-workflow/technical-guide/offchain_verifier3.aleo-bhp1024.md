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

# offchain\_verifier3.aleo (BHP)

```rust
export const SIGVERIFY_PROGRAM_BHP1024 = `
program offchain_verifier.aleo;

struct Message:
    issuer as address;
    subject as address;
    dob as field;


closure get_msg_hash:
    input r0 as Message;
    hash.bhp1024 r0 into r1 as field;
    output r1 as field;


closure signature_verification:
    input r0 as field;
    input r1 as signature;
    input r2 as address;
    sign.verify r1 r2 r0 into r3;
    output r3 as boolean;


function verify:
    input r0 as signature.public;
    input r1 as address.public;
    input r2 as Message.public;
    call get_msg_hash r2 into r3;
    call signature_verification r3 r0 r1 into r4;
    output r4 as boolean.private;
`;
```
