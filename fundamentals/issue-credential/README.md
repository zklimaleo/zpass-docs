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

# Issue Credential

<details>

<summary>Step 1: Generate Account </summary>

```rust
/// Generates a private key using a provided random number generator (RNG).
///
/// # Parameters
/// - `rng`: A mutable reference to a random number generator (TestRng) used for cryptographic randomness.
///
/// # Returns
/// Returns a `Result` containing a generated private key of type `PrivateKey<Testnet3>` if successful,
/// or an error message otherwise.
fn generate_private_key(rng: &mut TestRng) -> Result<PrivateKey<Testnet3>, String> {
    
    // Attempt to create a new private key using the provided RNG.
    // Utilize the `new` method from `PrivateKey<Testnet3>` to handle this.
    PrivateKey::<Testnet3>::new(rng)
        // If the operation fails, map the error to a string message.
        .map_err(|_| String::from("Failed to create private key"))
}
```

</details>

<details>

<summary>Step 2: Create Credential</summary>

```rust
/// Creates a credential combining blockchain addresses and other fields based on the given credential payload.
///
/// # Parameters
/// - `payload`: A `Credential` object containing fields like issuer, subject, and date of birth (dob).
///
/// # Returns
/// Returns a `Result` containing a `Value<Testnet3>` if successful, or an error message otherwise.
fn create_credential_with_addresses_and_fields(payload: Credential) -> Result<Value<Testnet3>, String> {
    
    // Initialize an IndexMap with a capacity of 3 to store key-value pairs.
    let mut map = IndexMap::with_capacity(3);
    
    // Inner function to insert key-value pairs into the IndexMap.
    fn insert_to_map(
        map: &mut IndexMap<Identifier<Testnet3>, Plaintext<Testnet3>>, 
        key: &str, 
        value: Plaintext<Testnet3>
    ) -> Result<(), String> {
        
        // Convert the key from a string to an Identifier.
        let id = Identifier::from_str(key)
            .map_err(|_| format!("Can't convert {} to Identifier", key))?;
        
        // Insert the Identifier and associated Plaintext into the map.
        map.insert(id, value);
        
        Ok(())
    }
    
    // Insert the issuer's address into the map.
    insert_to_map(&mut map, "issuer", Plaintext::from(Literal::Address(payload.issuer)))?;
    
    // Insert the subject's address into the map.
    insert_to_map(&mut map, "subject", Plaintext::from(Literal::Address(payload.subject)))?;
    
    // Insert the date of birth (dob) into the map.
    insert_to_map(&mut map, "dob", Plaintext::from(Literal::Field(payload.dob)))?;
    
    // Return the populated IndexMap wrapped in a Plaintext structure as a successful result.
    Ok(Value::Plaintext(Plaintext::Struct(map, Default::default())))
}
```

</details>

<details>

<summary>Step 3: Hash Credential</summary>

```rust
/// Creates a hash based on the input message and the specified hash algorithm.
///
/// # Parameters
/// - `message`: The message to be hashed, represented as an array slice of `Field<Testnet3>` objects.
/// - `algorithm`: The hash algorithm to use for hashing. Currently supports only POSEIDON2.
///
/// # Returns
/// Returns a `Result` containing the hash as `Field<Testnet3>` if successful, or an error message otherwise.
fn create_hash(message: &[Field<Testnet3>], algorithm: HashAlgorithm) -> Result<Field<Testnet3>, String> {
    
    // Initialize variable 'hash' to store the resulting hash value
    let hash = match algorithm  {
        
        // If the chosen algorithm is POSEIDON2
        HashAlgorithm::POSEIDON2 => {
            
            // Execute hash_psd2 method from Testnet3 to generate hash
            // Map any errors to their string representation
            Testnet3::hash_psd2(message).map_err(|e| e.to_string())?
        }
    };
    
    // Return the hash as a successful result
    Ok(hash)
}
```

</details>

<details>

<summary>Step 4: Sign Credential</summary>

```rust
/// Signs a message using a private key and a random number generator (RNG).
///
/// # Parameters
/// - `private_key`: Reference to the private key of type `PrivateKey<Testnet3>` used for signing the message.
/// - `message`: The message to be signed, represented as an array slice of `Field<Testnet3>` objects.
/// - `rng`: A mutable reference to a random number generator (TestRng) for cryptographic operations.
///
/// # Returns
/// Returns a `Result` containing a tuple with the generated signature of type `Signature<Testnet3>`
/// and a nonce of type `Scalar<Testnet3>` if successful, or an error message otherwise.
fn sign_message_with_private_key(
    private_key: &PrivateKey<Testnet3>, 
    message: &[Field<Testnet3>], 
    rng: &mut TestRng
) -> Result<(Signature<Testnet3>, Scalar<Testnet3>), String> {

    // Attempt to sign the message using the provided private key and RNG.
    match Signature::<Testnet3>::sign(private_key, message, rng) {
        
        // If signature is successfully created
        Ok(signature) => {
            
            // Generate a random nonce using the RNG
            let nonce = Scalar::rand(rng);
            
            // Return the signature and the nonce as a successful result
            Ok((signature, nonce))
        },
        
        // If signature creation fails
        Err(_) => {
            
            // Return an error message indicating the failure
            Err(String::from("Failed to create signature"))
        },
    }
}

```

</details>
