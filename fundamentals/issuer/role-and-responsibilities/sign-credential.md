# Sign Credential

<details>

<summary>Sign Credential</summary>

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
