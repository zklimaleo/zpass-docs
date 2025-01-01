# Background

In the Aleo ecosystem, programs are inherently static and predefined, which introduces challenges in supporting dynamic program imports. This limitation makes deploying a universal zPass program—capable of accommodating all possible credentials and use cases—difficult. As a result, developers interested in using zPass have two primary options: either import an existing zPass program that aligns with their needs or deploy a customized version tailored to their specific use case. Creating a zPass program from scratch requires developers to handle the issuance process themselves and carefully constrain values in supported credentials during zPass issuance.

Over time, as more zPass programs are developed and the range of supported credentials grows, the ecosystem will become increasingly comprehensive. This progression is expected to reduce the need for future applications to deploy new zPass programs from scratch, as a library of reusable zPass programs will be available.

This section provides an overview of the structure of a zPass program and explains how it can be integrated into applications to address diverse use cases.

## zPass Program Examples

Explore various zPass program implementations:

* [verify-offchain-program.md](verify-offchain-program.md "mention"): Demonstrates verifying user credentials offchain using digital signatures to ensure authenticity and privacy.
* [zpass-issuance-program.md](zpass-issuance-program.md "mention"): Explains how to issue private zPass records containing user credentials with support for flexible value types.
* [zpass-hiding-program.md](zpass-hiding-program.md "mention"): Showcases the use of randomized commitments to protect user credentials while maintaining privacy.
* [zpass-invalidate-program.md](zpass-invalidate-program.md "mention"): Introduces logic to invalidate compromised zPass records and support reissuance for enhanced security.
* [zpass-invalidate-hiding-program.md](zpass-invalidate-hiding-program.md "mention"): Combines invalidation and hiding functionalities for robust security and privacy in zPass management.

Click on the links to explore each program and learn about their specific functionalities and use cases.
