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

### Overview

The `create_hash` function generates a cryptographic hash using one of the supported algorithms. It returns a `Result` containing either the generated hash as a `String` or an error using the `anyhow` library for extended error handling.

### Function Definition

```rust
pub(crate) fn create_hash(value: Value<Testnet3>, algorithm: HashAlgorithm) -> Result<String, anyhow::Error>;
```

#### Parameters:

* **value**: The value you want to hash, of type `Value<Testnet3>`.
* **algorithm**: An enum representing the hashing algorithm to be used (`HashAlgorithm`).

#### Returns:

* `Result<String, anyhow::Error>`: A `Result` that will either contain the generated hash as a `String` or an error.

### Hash Calculation Steps

* **Conversion**: The `value` is first converted into either fields or bits based on the algorithm selected.
* **Hashing**: The `Testnet3` object exposes static methods to generate hashes based on the selected algorithm. These methods return a `Result` and can fail, leading to error propagation.
* **Final Conversion**: For some algorithms, additional steps like converting to a group and then back to a field are performed.

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

<details>

<summary>Hash Credential</summary>

{% code overflow="wrap" %}
```rust
// This function creates a cryptographic hash of a given value, using the specified hash algorithm.
// It returns a string representation of the hash or an error.
pub(crate) fn create_hash(value: Value<Testnet3>, algorithm: HashAlgorithm) -> Result<String, anyhow::Error> {
    
    // Generate the hash based on the selected algorithm
    let hash = match algorithm {
        
        // POSEIDON2 algorithm
        HashAlgorithm::POSEIDON2 => {
            // Convert the value to a fields object
            let message = value.to_fields()
                .map_err(|e| anyhow!("Failed value to Fields conversion: {}", e))?;
            
            // Perform the POSEIDON2 hash conversion
            let hash = Testnet3::hash_psd2(message.as_slice())
                .map_err(|e| anyhow!("Failed hash_psd2 conversion: {}", e))?;
            
            // Convert the hash to a string representation
            hash.to_string()
        },
        
        // BHP1024 algorithm
        HashAlgorithm::BHP1024 => {
            // Convert the value to bits in little-endian
            let message = value.to_bits_le();
            
            // Perform the BHP1024 hash conversion
            let hash = Testnet3::hash_bhp1024(message.as_slice())
                .map_err(|e| anyhow!("Failed hash_bhp1024 conversion: {}", e))?;
            
            // Convert the hash to a string representation
            hash.to_string()
        },
        
        // SHA3_256 algorithm
        HashAlgorithm::SHA3_256 => {
            // Convert the value to bits in little-endian
            let message = value.to_bits_le();
            
            // Generate SHA3-256 hash from the message bits
            let sha_bit_vec = Testnet3::hash_sha3_256(message.as_slice())
                .map_err(|e| anyhow!("Failed hash_sha3_256 conversion: {}", e))?;
            
            // Convert SHA3-256 hash to a group using BHP256
            let bhp_group = Testnet3::hash_to_group_bhp256(sha_bit_vec.as_slice())
                .map_err(|e| anyhow!("Failed hash_to_group_bhp256 conversion: {}", e))?;
            
            // Convert the group to a literal
            let literal_group_from_bhp = Literal::Group(bhp_group);
            
            // Cast the group literal to a field
            let casted_to_field = literal_group_from_bhp
                .cast_lossy(snarkvm::prelude::LiteralType::Field)
                .map_err(|e| anyhow!("Failed cast_lossy conversion: {}", e))?;
            
            // Convert the hash to a string representation
            casted_to_field.to_string()
        },
        
        // KECCAK256 algorithm
        HashAlgorithm::KECCAK256 => {
            // Convert the value to bits in little-endian
            let message = value.to_bits_le();
            
            // Generate Keccak-256 hash from the message bits
            let keccak_bit_vec = Testnet3::hash_keccak256(message.as_slice())
                .map_err(|e| anyhow!("Failed hash_keccak256 conversion: {}", e))?;
            
            // Convert Keccak-256 hash to a group using BHP256
            let bhp_group = Testnet3::hash_to_group_bhp256(keccak_bit_vec.as_slice())
                .map_err(|e| anyhow!("Failed hash_to_group_bhp256 conversion: {}", e))?;
            
            // Convert the group to a literal
            let literal_group_from_bhp = Literal::Group(bhp_group);
            
            // Cast the group literal to a field
            let casted_to_field = literal_group_from_bhp
                .cast_lossy(snarkvm::prelude::LiteralType::Field)
                .map_err(|e| anyhow!("Failed cast_lossy conversion: {}", e))?;
            
            // Convert the hash to a string representation
            casted_to_field.to_string()
        }
    };
    
    // Return the generated hash
    Ok(hash)
}

```
{% endcode %}

</details>
