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

# Generate Credential

### Overview

The tutorial aims to guide you through the use of the `generate_message_with_addresses_and_fields` function. This function takes a `Credential` payload and returns a `Value<Testnet3>` wrapped in Rust's `Result` type.

### Function Signature

Here's the function definition:

```rust
pub(crate) fn generate_message_with_addresses_and_fields(payload: Credential) -> Result<Value<Testnet3>, anyhow::Error>;
```

#### Parameters:

* **payload**: An instance of a `Credential` struct containing various fields like issuer, subject, date of birth (dob), nationality, and expiry.

#### Returns:

A `Result` containing:

* A `Value<Testnet3>` object, or
* An error of type `anyhow::Error` if the operation fails.

### Under the Hood: Insertion to Map

The function employs an `IndexMap` with an initial capacity of 3 to store key-value pairs. The function `insert_to_map` is called multiple times to insert:

* `issuer` and `subject` as addresses.
* `dob`, `nationality`, and `expiry` as fields.

These are all inserted as `Plaintext` types, and they are derived from the `Credential` payload.

### Attributes

<table><thead><tr><th width="190">Attribute</th><th width="550">Definition</th></tr></thead><tbody><tr><td>Issuer</td><td>Issuing authority public address<br><em>ex. Aleo Address of the credential Issuer.</em></td></tr><tr><td>Subject</td><td><p>Holder public address</p><p><em>ex. Aleo Address of the credential Holder.</em></p></td></tr><tr><td>Date of Birth</td><td>Attribute value represented as a field.</td></tr><tr><td>Nationality</td><td>Attribute value encoded from a string and represented as a field.</td></tr><tr><td>Expiration</td><td>Attribute value represented as a field.</td></tr></tbody></table>

<details>

<summary>Generate Credential</summary>

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
