# zPass issuance program

````
```leo
// The 'zpass_issuance' program.
program zpass_issuance.aleo {
    // The ZPass record
    record ZPass {
        owner: address,
        issuer: address,
        dob: u32,
        nationality: field,
        expiry: u32,
        salt: scalar
    }

    // The private credentials struct
    struct PrivateCredentials {
        issuer: address,
        subject: address,
        dob: u32,
        nationality: field,
        expiry: u32
    }

    // The public credentials struct
    // This is the public information that is shared publicly onchain
    struct PublicCredentials {
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
        private pri: PrivateCredentials,
        public pub: PublicCredentials,
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
            issuer: pri.issuer,
            dob: pri.dob,
            nationality: pri.nationality,
            expiry: pri.expiry,
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
}

```
````

The program above demonstrates an example implementation of a zPass issuance program. This program issues a private `zPass` record to a user, which can be utilized in various scenarios, such as third-party applications that support this specific zPass program. The `zPass` record is highly flexible and can contain any value type supported by Aleo, tailored to the needs of the integrating applications.

The `Credentials` object is divided into private and public components, allowing the program to selectively disclose certain information publicly while keeping sensitive data private. This design provides flexibility, enabling verifiers to access publicly disclosed information without compromising the privacy of the user.

Additionally, the program introduces two extra mappings to enhance functionality and security. These mappings are used to track the issuance count and prevent the double issuance of the same zPass record.

Similar to the [verify-offchain-program.md](verify-offchain-program.md "mention"), the `issue` transition reconstructs the full credentials and verifies them against the issuer's signature to ensure authenticity. Once the verification is successful, the program issues a zPass record to the caller and stores the commitment of the credentials on-chain. To enhance security, **salt** is used to add randomness to the commitment, ensuring uniqueness and making it resistant to preimage attacks. This commitment serves as a safeguard to prevent double issuance, ensuring the integrity of the zPass issuance process.
