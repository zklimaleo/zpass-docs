# Generate Credential



<details>

<summary>Add Attributes to Credential</summary>

{% code overflow="wrap" %}
```rust
/// Creates a credential combining blockchain addresses and other fields 
/// based on the given credential payload.
///
/// # Parameters
/// - `payload`: A `Credential` object containing fields like issuer, 
/// subject, and date of birth (dob).
///
/// # Returns
/// Returns a `Result` containing a `Value<Testnet3>` if successful, or an /// error message otherwise.
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
    insert_to_map(&mut map, "issuer",             
        Plaintext::from(Literal::Address(payload.issuer)))?;
    
    // Insert the subject's address into the map.
    insert_to_map(&mut map, "subject", 
        Plaintext::from(Literal::Address(payload.subject)))?;
    
    // Insert the date of birth (dob) into the map.
    insert_to_map(&mut map, "dob", 
        Plaintext::from(Literal::Field(payload.dob)))?;
    
    // Return the populated IndexMap wrapped in a Plaintext structure as a 
    // successful result.
    Ok(Value::Plaintext(Plaintext::Struct(map, Default::default())))
}
```
{% endcode %}

</details>

### Attributes

<table><thead><tr><th width="162">Name</th><th width="291">Rust</th><th>Leo</th></tr></thead><tbody><tr><td>Issuer</td><td></td><td></td></tr><tr><td>Subject</td><td></td><td></td></tr><tr><td>Date of Birth</td><td></td><td></td></tr><tr><td>Nationality</td><td></td><td></td></tr><tr><td>Expiration</td><td></td><td></td></tr></tbody></table>
