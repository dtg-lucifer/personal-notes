### **1. How Storage Works in a Blockchain**

Think of a blockchain as a library where:

- Each **block** is like a shelf containing books (transactions).
- The library keeps growing as new shelves (blocks) are added.
- The librarians (nodes) don't need to store all the shelves forever—they can manage their storage while ensuring the library stays functional.

---

### **2. Managing Unlimited Growth**

#### **A. Pruning**

Some nodes are "pruned," meaning:

1. **Full Validation**: The node reads all shelves (blocks) to confirm they belong to the library.
2. **Discarding Old Shelves**: After validation, the node keeps only the **catalog** (block headers) and a summary of active books (UTXO set for Bitcoin or account states for Ethereum).
    - Example: A Bitcoin pruned node only keeps recent blocks and the list of "unspent funds." If someone asks about a specific transaction, the node directs them to an archival node.

#### **B. Light Nodes (SPV Nodes)**

1. Light nodes store only the **catalog of shelves** (block headers), not the books themselves.
2. If a user asks, "Show me my transaction," the light node:
    - Requests the specific shelf and book from a full node.
    - Uses a **Merkle proof** to ensure the book belongs to the shelf without storing the entire book.

#### **C. Archival Nodes**

1. These are like librarians who keep every shelf and book forever.
2. They are essential for explorers (like Etherscan) but aren’t required for most users.

---

### **3. Scaling Solutions**

#### **A. Offloading to Layer 2**

- Imagine there’s a **second library branch** (Layer 2, like Lightning Network or zkRollups):
    - Most books are stored there for regular use.
    - Occasionally, summaries of what happened in the second branch are sent to the main library.

**Example**:

- Bitcoin's Lightning Network:
    1. Alice and Bob open a "channel" on Bitcoin's blockchain.
    2. They exchange transactions privately in the channel without adding books to the main library.
    3. When the channel closes, a summary is sent to the main library.

#### **B. Sharding (Ethereum 2.0)**

- Instead of one giant library, imagine **many smaller libraries (shards)**, each with its own set of shelves.
- Librarians specialize in managing specific shards, reducing their workload.

**Example**:

1. One shard stores transactions for accounts starting with "A–M."
2. Another shard stores "N–Z."
3. If someone needs data across shards, they can access a **coordinator shard** that tracks where everything is.

---

### **4. Data Retrieval**

When you ask for all your transactions, the system works like this:

#### **A. Bitcoin (UTXO Model)**

1. Your wallet checks the blockchain for transactions where your address is listed as the recipient.
2. The node scans the **UTXO set** (like a list of active checks).
    - Example: "Alice sent 1 BTC to you in block 500, and Bob sent 0.5 BTC in block 520."
3. Your wallet sums the UTXOs to display your balance.

#### **B. Ethereum (Account Model)**

1. Your wallet queries the blockchain's **state database**.
    - The state database stores the balance and transaction history of every account.
2. The node scans for all transactions involving your account.
    - Example: "You sent 1 ETH to Bob in block 200, and received 0.5 ETH in block 220."
3. Results are aggregated and displayed.

#### **How Nodes Find Data Efficiently**

- **Merkle Trees**: Like a table of contents in each block, pointing to transactions.
    - Nodes quickly verify specific transactions without reading the entire block.
- **Indexes**: Full nodes pre-build indexes to make searching faster.

---

### **5. Practical Example: Fetching Transactions**

Let’s visualize how your wallet fetches data:

1. **You Request All Transactions for Your Wallet**:
    
    - Your wallet contacts a node (full node or light node).
2. **Step 1: Querying the Blockchain**:
    
    - Bitcoin: The node scans the UTXO set and past transactions to find relevant ones.
    - Ethereum: The node queries the state database and transaction history.
3. **Step 2: Verifying Results**:
    
    - The node uses Merkle proofs or checks signatures to confirm the data's integrity.
4. **Step 3: Returning Data**:
    
    - The node aggregates and sends the data back to your wallet.
    - Your wallet organizes it into a readable format.

---

### **6. Why This Process Works Despite Growing Data**

- **Not All Nodes Store Everything**: Many nodes prune older data.
- **Specialized Roles**: Some nodes store full history, while others handle current activity.
- **Efficient Structures**: Merkle trees, state roots, and UTXO sets allow nodes to validate data without storing everything.