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

# Hash Types

<table><thead><tr><th width="129">Name</th><th width="291">Rust</th><th>Leo</th></tr></thead><tbody><tr><td>Poseidon2</td><td><pre><code>Testnet3::hash_psd2(x)
</code></pre></td><td><pre><code>Poseidon2::hash_to_field(x)
</code></pre></td></tr><tr><td>BHP</td><td><pre><code><strong>Testnet3::hash_bhp1024(x)
</strong></code></pre></td><td><pre><code>BHP1024::hash_to_field(x)
</code></pre></td></tr><tr><td>Keccak</td><td><pre><code>Testnet3::hash_keccak256(x)
</code></pre></td><td><pre><code><strong>Keccak256::hash_to_field(x)
</strong></code></pre></td></tr><tr><td>SHA3</td><td><pre><code>Testnet3::hash_sha3_256(x)
</code></pre></td><td><pre><code>SHA3_256::hash_to_field(x)
</code></pre></td></tr></tbody></table>
