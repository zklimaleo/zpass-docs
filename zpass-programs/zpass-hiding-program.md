# zPass hiding program

````
```leo
// The 'zpass_hiding' program.
program zpass_hiding.aleo {
    // The ZPass record
    record ZPass {
        owner: address,
        issuer: group,
        dob: group,
        nationality: group,
        expiry: group,
        salt: scalar
    }

    // The private credential struct
    struct PrivateCredential {
        issuer: address,
        subject: address,
        dob: u32,
        nationality: field,
        expiry: u32
    }

    // The public credential struct
    // This is the public information that is shared publicly onchain
    struct PublicCredential {
        salt: scalar
    }

    // The full credentials struct to be hashed and verified against the signature
    struct FullCredentials {
        issuer: address,
        subject: address,
        dob: u32,
        nationality: field,
        expiry: u32,
        salt: scalar
    }

    // The mapping of issued commitments
    mapping issued: group => bool;

    // The count of issued ZPasses
    // Using key of 0field as global key
    mapping issuance_count: field => u128;

    async transition issue(
        private sig: signature,
        private pri: PrivateCredential,
        public pub: PublicCredential,
    ) -> (ZPass, Future) {
        // Construct the full credentials struct to be hashed and verified against the signature
        let credentials: FullCredentials = FullCredentials {
            issuer: pri.issuer,
            subject: self.caller, // The caller must be the subject of the ZPass
            dob: pri.dob,
            nationality: pri.nationality,
            expiry: pri.expiry,
            salt: pub.salt,
        };

        // Verify signature
        assert_eq(signature::verify(sig, pri.issuer, Poseidon2::hash_to_field(credentials)), true);

        // Compute commitment to prevent double issuance
        let commit: group = BHP256::commit_to_group(self.caller, pub.salt);

        // Return the ZPass record and pass the commitment to store in the mapping
        return (ZPass {
            owner: self.caller,
            issuer: BHP256::commit_to_group(pri.issuer, pub.salt),
            dob: BHP256::commit_to_group(pri.dob, pub.salt),
            nationality: BHP256::commit_to_group(pri.nationality, pub.salt),
            expiry: BHP256::commit_to_group(pri.expiry, pub.salt),
            salt: pub.salt
        }, issue_finalize(commit));
    }

    async function issue_finalize(
        public commit: group
    ) {
        // Ensure the commitment is not already issued
        assert_eq(issued.get_or_use(commit, false), false);

        // Store the commitment in the mapping
        issued.set(commit, true);
        // Increment the issuance count
        issuance_count.set(0field, issuance_count.get_or_use(0field, 0u128) + 1u128);
    }

    // Sample transition to check if the dob is more than certain age
    transition more_than_18(
        dob: u32,
        dob_check: u32,
        zpass: ZPass
    ) {
        // Ensure knowledge of the dob commitment
        assert_eq(zpass.dob, BHP256::commit_to_group(dob, zpass.salt));
        // Ensure the dob is more than certain age
        assert_eq(dob > dob_check, true);
    }
}

```
````

Similar to the [zpass-issuance-program.md](zpass-issuance-program.md "mention"), the values in the zPass are converted into commitments using a salt as randomness. This approach enhances the security of user-confidential information, providing additional protection against rare scenarios such as private key or view key compromise. However, this added layer of security introduces a tradeoff: users are required to remember and re-enter these private values when utilizing their zPass in applications.

The `more_than_18` transition provides an example of how a private value from the zPass can be used. In this transition, the commitment is reconstructed from the user-provided input values to verify the user's knowledge of the original values, ensuring that only the rightful user can access or utilize the zPass data.
