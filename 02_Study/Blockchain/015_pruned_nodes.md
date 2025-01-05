### **1. Pruned Nodes and Your Transactions**

- A **pruned node** doesn’t store the full blockchain history, but it still:
    - Validates every transaction during initial synchronization.
    - Keeps the latest state of the blockchain (like the UTXO set for Bitcoin or the current state for Ethereum).
- Older transactions are removed **after validation**, but their effects (like UTXOs or account balances) are included in the current state.

---

### **2. What Happens if You Need an Old Transaction?**

If the transaction is part of **pruned data**:

1. Your wallet queries a full node or an archival node.
    - Archival nodes store the complete blockchain history and can provide older transactions.
    - Most blockchain explorers (e.g., Etherscan for Ethereum) use archival nodes to display transaction histories.
2. The pruned node can still verify:
    - The transaction's effect is consistent with the current state (e.g., your balance is correct based on your transaction history).

---

### **3. Example: Bitcoin**

Let’s say:

- You want to see a transaction `Tx123` from block 100, but your pruned node has discarded blocks older than 500.

**Process**:

1. **UTXO Verification**:
    - If `Tx123` created a UTXO (e.g., 0.5 BTC sent to you), the pruned node still has that UTXO in its database.
    - It confirms that `Tx123` exists indirectly because the UTXO exists.
2. **Querying an Archival Node**:
    - Your wallet can connect to an archival node to fetch the full details of `Tx123` if needed.

---

### **4. Example: Ethereum**

In Ethereum, where transactions are tied to accounts:

- If a pruned node doesn’t store `Tx123`, it still has the **latest state** of your account (e.g., balance, contract storage).
- To retrieve the full history:
    - Your wallet queries an archival node or a blockchain explorer like Etherscan.
    - These services use pre-indexed data to retrieve old transactions quickly.

---

### **5. Why It’s Safe and Reliable**

- **Redundancy**:
    - Thousands of full nodes and archival nodes exist globally. Even if some nodes prune old data, others retain it.
- **Merkle Roots**:
    - Every block header contains a **Merkle root**, which summarizes all transactions in the block.
    - Even a pruned node can verify old transactions using a **Merkle proof** provided by another node.

---

### **6. Practical Scenario**

Imagine your wallet requests the details of `Tx123`:

1. **Query**:
    - Your wallet first asks the connected pruned node.
    - The pruned node replies: "I don’t have this transaction, but I can verify its effect on the current state."
2. **Fetch Full Data**:
    - Your wallet then queries a full node or an explorer for the complete transaction details.

---

### **7. Why Pruned Nodes Are Useful**

- Pruned nodes reduce storage costs for most participants.
- They ensure the blockchain remains decentralized by allowing individuals with limited resources to participate.