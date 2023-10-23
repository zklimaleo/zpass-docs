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

# Sign Credential

### Overview

This provides an explanation of how to use the `sign_message_with_private_key` function to sign a message using a private key and a random number generator in a Rust environment. The function returns either a generated signature and nonce or an error message.

### Function Signature

Here's the function definition:

```rust
sign_message_with_private_key(
    private_key: &PrivateKey<Testnet3>, 
    message: &[Field<Testnet3>], 
    rng: &mut TestRng
) -> Result<(Signature<Testnet3>, Scalar<Testnet3>), String>;
```

#### Parameters:

* **private\_key**: A reference to the private key used for signing. It's of type `PrivateKey<Testnet3>`.
* **message**: An array slice of message elements, each being of type `Field<Testnet3>`.
* **rng**: A mutable reference to a random number generator (`TestRng`) for cryptographic operations.

#### Returns:

A `Result` containing either:

* A tuple of the generated signature (`Signature<Testnet3>`) and a nonce (`Scalar<Testnet3>`), or
* An error message (`String`) indicating the failure.

<details>

<summary>Sign Credential</summary>

<pre class="language-rust" data-overflow="wrap"><code class="lang-rust">/// Signs a message using a private key and a random number generator (RNG).
///
/// # Parameters
/// - `private_key`: Reference to the private key of type 
/// `PrivateKey&#x3C;Testnet3>` used for signing the message.
///
/// - `message`: The message to be signed, represented as an array slice of 
/// `Field&#x3C;Testnet3>` objects.
///
<strong>/// - `rng`: A mutable reference to a random number generator (TestRng) for 
</strong><strong>/// cryptographic operations.
</strong>///
/// # Returns
/// Returns a `Result` containing a tuple with the generated signature of 
/// type `Signature&#x3C;Testnet3>` and a nonce of type `Scalar&#x3C;Testnet3>` if 
/// successful, or an error message otherwise.
fn sign_message_with_private_key(
    private_key: &#x26;PrivateKey&#x3C;Testnet3>, 
    message: &#x26;[Field&#x3C;Testnet3>], 
    rng: &#x26;mut TestRng
) -> Result&#x3C;(Signature&#x3C;Testnet3>, Scalar&#x3C;Testnet3>), String> {

    // Attempt to sign the message using the provided private key and RNG.
    match Signature::&#x3C;Testnet3>::sign(private_key, message, rng) {
        
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

</code></pre>

</details>
