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

# onchain\_issuer.aleo (Poseidon)

```
// Aleo program named 'onchain_issuer'
program onchain_issuer.aleo {

    // Define a struct called 'Credentials' to hold issuer, subject, and date of birth (dob)
    struct Credentials {
        issuer: address,
        subject: address,
        dob: field,
    }

    // Define a record called 'SignedCredential' to hold an ownership address, a Credentials object, and a signature
    record SignedCredential {
        owner: address,
        credential: Credentials,
        sig: signature
    }

    // Function to verify that the hash of 'msg' equals 'msg_hash'
    function verify_hash(msg_hash: field, msg: Credentials) -> bool {
        return msg_hash.eq(Poseidon2::hash_to_field(msg));
    }

    // Function to verify a signature against the issuer and message hash
    function signature_verification(msg_hash: field, sig: signature, issuer: address) -> bool {
        return signature::verify(sig, issuer, msg_hash);
    }

    // Transition function to verify a credential's hash and signature
    transition verify(
        public sig: signature, 
        public addr: address, 
        public msg_hash: field,
        public msg: Credentials
    ) -> (SignedCredential, bool) {

        // Assert that the message hash is correct
        assert(verify_hash(msg_hash, msg));

        // Verify the signature against the message hash and issuer
        let sig_is_verified: bool = signature_verification(
            msg_hash,
            sig,
            msg.issuer
        );

        // Create a signed record containing the credential and signature
        let signed_record: SignedCredential = SignedCredential {
            owner: msg.subject,
            credential: msg,
            sig
        };

        // Return the signed record and whether the signature was successfully verified
        return (signed_record, sig_is_verified);
    }
}
```
