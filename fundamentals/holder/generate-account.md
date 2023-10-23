# Generate Account

<details>

<summary>Generate Account </summary>

{% code overflow="wrap" %}
```rust
/// Generates a private key using a provided random number generator (RNG).
///
/// # Parameters
/// - `rng`: A reference to a random number generator (TestRng).
///
/// # Returns
/// Returns a `Result` containing a generated private key of type 
/// `PrivateKey<Testnet3>` if successful, or an error message otherwise.
fn generate_private_key(rng: &mut TestRng) -> Result<PrivateKey<Testnet3>, String> {
    // Attempt to create a new private key using the provided RNG.
    // Utilize the `new` method from `PrivateKey<Testnet3>` to handle this.
    PrivateKey::<Testnet3>::new(rng)
        // If the operation fails, map the error to a string message.
        .map_err(|_| String::from("Failed to create private key"))
}
```
{% endcode %}

</details>
