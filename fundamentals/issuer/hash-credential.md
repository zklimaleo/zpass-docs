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

# Hash Credential

<details>

<summary>Hash Credential</summary>

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

### Hash Types

<table><thead><tr><th width="129">Name</th><th width="291">Rust</th><th>Leo</th></tr></thead><tbody><tr><td>Poseidon2</td><td><pre><code>Testnet3::hash_psd2(x)
</code></pre></td><td><pre><code>Poseidon2::hash_to_field(x)
</code></pre></td></tr><tr><td>BHP</td><td><pre><code><strong>Testnet3::hash_bhp1024(x)
</strong></code></pre></td><td><pre><code>BHP1024::hash_to_field(x)
</code></pre></td></tr><tr><td>Keccak</td><td><pre><code>Testnet3::hash_keccak256(x)
</code></pre></td><td><pre><code><strong>Keccak256::hash_to_field(x)
</strong></code></pre></td></tr><tr><td>SHA3</td><td><pre><code>Testnet3::hash_sha3_256(x)
</code></pre></td><td><pre><code>SHA3_256::hash_to_field(x)
</code></pre></td></tr></tbody></table>
