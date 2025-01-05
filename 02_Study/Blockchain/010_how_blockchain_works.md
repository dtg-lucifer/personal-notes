## **1. What Blockchains Store and Where**

### **Structure of Blockchain Data**

- A blockchain is a sequence of blocks, where each block contains:
    - A **block header** (metadata like timestamp, previous block hash, etc.).
    - A **Merkle tree root**: Efficiently summarizes all transactions in the block.
    - The **list of transactions** themselves.

### **Data Storage by Nodes**

- **Full Nodes**:
    - Store the entire blockchain history (all blocks and their data).
    - These nodes validate and propagate new transactions and blocks.
- **Pruned Nodes**:
    - Store only a portion of the blockchain. After validating older blocks, they delete them, retaining just enough to ensure security (e.g., headers and recent transactions).
- **Lightweight Nodes** (SPV Nodes):
    - Store only block headers. They rely on full nodes for detailed data, using Merkle proofs to verify transactions.

### **Storage Limitations**

- Nodes do not have unlimited storage. To mitigate this:
    - Nodes prune older, unnecessary data while maintaining security.
    - Many blockchain designs limit block sizes or implement mechanisms like state rent (Ethereum proposals) to cap storage requirements.

---

## **2. How Data is Distributed in the P2P Network**

- Blockchains use a peer-to-peer (P2P) protocol to ensure decentralized operation:
    - Nodes are connected in a decentralized manner, sharing and validating blocks and transactions.
    - Data is redundantly stored across many nodes to ensure reliability and fault tolerance.
    - A distributed hash table (DHT) or other data structures may be used to locate specific data.

---

## **3. Retrieving Data: Viewing All Transactions**

When you want to view all your transactions, here's what happens:

### **Step 1: Locating Relevant Transactions**

- Your **wallet address** (public key) or an associated identifier is used to query the blockchain.
- Transactions are not stored in a single place or block. Instead:
    - A **full node** or blockchain explorer indexes the blockchain to locate all transactions involving your address.

### **Step 2: Fetching Data**

- A node or service (like a blockchain explorer) performs a scan of:
    - The **UTXO set** (Unspent Transaction Outputs) in blockchains like Bitcoin.
    - The **account state** in account-based blockchains like Ethereum.
- Transactions involving your address are fetched and aggregated.

### **Step 3: Displaying Data**

- Once located, transactions are formatted and displayed by:
    - A blockchain explorer (e.g., Etherscan for Ethereum, Blockchair for Bitcoin).
    - Your wallet software, which connects to nodes or APIs to fetch this data.

---

## **4. Challenges and Optimizations**

### **Scaling and Storage**

- As blockchain usage grows, data requirements increase. Some solutions include:
    - **Sharding**: Dividing the blockchain into smaller pieces for distributed storage.
    - **Layer 2 solutions**: Offloading transactions to secondary networks (e.g., Lightning Network for Bitcoin, Optimistic Rollups for Ethereum).
    - **Compression techniques**: Using efficient data structures (e.g., Merkle trees) to reduce storage overhead.

### **Efficient Data Retrieval**

- **Indexing**: Nodes or explorers build indexes for faster querying.
- **Caching**: Frequently accessed data (like account balances) is cached by nodes or APIs.

---

## **Example Scenario: Fetching Transactions**

- **You request all your Bitcoin transactions**:
    
    - Your wallet software connects to a node.
    - The node scans all blocks to find transactions where your address is involved.
    - It uses the UTXO database to confirm your current balance.
    - Results are returned to your wallet software for display.
- **You request all Ethereum transactions**:
    
    - Your wallet queries an Ethereum node or API.
    - The node checks the transaction history and account state using its database.
    - Data is returned to the wallet for display.

---

# Follow along with 
- [[011_current_state]]
- [[012_how_storage_works]]
- [[013_efficient_data_lookup]]
- [[014_merkle_tree_utxo_sets]]
- [[015_pruned_nodes]]
- [[016_flow_of_query_data]]