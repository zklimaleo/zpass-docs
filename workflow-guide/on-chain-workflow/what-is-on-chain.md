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

# What is On-Chain?

When an Aleo program is executed an execution proof and program outputs, which for zPass is a record containing verified credential attributes.&#x20;

A **record** is a fundamental data structure for encoding user assets and application state.\
Each account record contains information that specifies the record owner, its stored value, and its application state.&#x20;

A record that has a `visibility` of `private` is verifiably encrypted in the transition and stored on the ledger. This enables users to securely and privately transfer record data and values between one another over the public network. Only the sender and receiver with their corresponding account view keys are able to decrypt these records.

The output record and execution proof are wrapped in a transaction, and delivered to the Aleo Blockchain.
