---
share_link: https://share.note.sx/8kxiv6h5#/KhHl7wZQgDJzqoAORfL6bWAuKbEh9zIc6AIkCN5Avk
share_updated: 2025-01-04T01:49:20+05:30
---
# What Is the Oracle Problem?

The oracle problem revolves around a very simple limitation—blockchains cannot pull in data from or push data out to any external system as built-in functionality. As such, blockchains are isolated networks, akin to a computer with no Internet connection. The isolation of a blockchain is the precise property that makes it extremely secure and reliable, as the network only needs to form consensus on a very basic set of binary (true/false) questions using data already stored inside of its ledger. These questions include: did the public key holder sign the transaction with their corresponding private key, does the public address have enough funds to cover its transaction, and is the type of transaction valid within the particular smart contract? The very narrow focus of blockchain consensus is why smart contracts are referred to as being deterministic—they execute exactly as written with a much higher degree of certainty than traditional systems.

However, for smart contracts to realize upwards of [90% of their potential use cases](https://blog.chain.link/smart-contract-use-cases/), they must connect to the outside world. For example, financial smart contracts need market information to determine settlements, insurance smart contracts need IoT and web data to make decisions on policy payouts, trade finance contracts need trade documents and digital signatures to know when to release payments, and many smart contracts want to settle in fiat currency on a traditional payment network. None of this information is inherently generated within the blockchain, nor are these traditional services directly accessible.

Bridging the connection between the blockchain (on-chain) and the outside world (off-chain) requires an additional and separate piece of infrastructure known as an oracle.

The blockchain oracle problem is one of the most important barriers to overcome if smart contracts on networks like Ethereum are to achieve mass adoption across a wide variety of markets and use cases.

[Smart contracts](https://chain.link/education/smart-contracts) running on [blockchains](https://chain.link/education-hub/blockchain) offer immense potential to redefine the way independent entities engage in contractual agreements and exchange value. Operating separately from the smart contract economy is the much larger non-blockchain digital economy, made up of all the Internet-connected devices computing online. A byproduct of digital infrastructure is an ever-expanding reservoir of [data and APIs](https://blog.chain.link/understanding-how-data-and-apis-power-next-generation-economies/), which provide insights into how the world works; e.g., Internet search results presenting popular discussion topics in society or IoT sensors showcasing common traffic patterns.

Blockchain-based smart contracts and traditional data and API economies have immense potential to combine into [hybrid smart contracts](https://blog.chain.link/hybrid-smart-contracts-explained/) and form the future architecture of data-driven automation, but the question is how do these two worlds connect? This encompasses the crux of the “oracle problem” and will be the focus of this article.

---

# What Is a Blockchain Oracle?

A [blockchain oracle](https://chain.link/education/blockchain-oracles) is a secure piece of middleware that facilitates communication between blockchains and any off-chain system, including data providers, web APIs, enterprise backends, cloud providers, IoT devices, e-signatures, payment systems, other blockchains, and more. Oracles take on several key functions:

- **Listen** – monitor the blockchain network to check for any incoming user or smart contract requests for off-chain data.
- **Extract** – fetch data from one or multiple external systems such as off-chain APIs hosted on third-party web servers.
- **Format** – format data retrieved from external APIs into a blockchain readable format (input) and/or making blockchain data compatible with an external API (output).
- **Validate** – generate a cryptographic proof attesting to the performance of an oracle service using any combination of data signing, blockchain transaction signing, TLS signatures, Trusted Execution Environment (TEE) attestations, or zero-knowledge proofs.
- **Compute** – perform some type of secure off-chain computation for the smart contract, such as calculating a median from multiple oracle submissions or generating a [verifiable random number](https://chain.link/vrf) for a gaming application.
- **Broadcast** – sign and broadcast a transaction on the blockchain in order to send data and any corresponding proof on-chain for consumption by the smart contract.
- **Output (optional)** –  send data to an external system upon the execution of a smart contract, such as relaying payment instructions to a traditional payment network or triggering actions from a cyber-physical system.

Carrying out the functions above requires that the oracle system operate both on and off the blockchain simultaneously. The on-chain component is for establishing a blockchain connection (to listen for requests), broadcasting data, sending proofs, extracting blockchain data, and potentially performing computation on the blockchain. The off-chain component is for processing requests, retrieving and formatting external data, sending blockchain data to external systems, and performing off-chain computation for greater scalability, privacy, security, and various other smart contract enhancements.

---

# How chainlink solves that ? 

![[Pasted image 20250102205325.png]]
