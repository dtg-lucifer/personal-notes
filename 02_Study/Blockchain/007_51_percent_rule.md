# What is that rule ? 

The "51% rule" in blockchain refers to the threshold of control a malicious actor needs to alter the blockchain's history or manipulate transactions. This specific percentage arises from the way most consensus mechanisms (like **Proof of Work** or **Proof of Stake**) are designed to achieve decentralized agreement. Here's the reasoning behind it:

---

### **Understanding the 51% Attack**

1. **Majority Rule in Consensus:**
    - In decentralized systems, the longest or most "work-done" chain (in PoW) or the chain with the highest "stake weight" (in PoS) is considered the valid blockchain.
    - Decisions about which block to append next or which chain is valid depend on a majority of participants (nodes or mining power).
2. **Why 51% Specifically?**
    - To control the majority, you need more than 50% of the network's power (hashrate in PoW, stake in PoS).
    - If an attacker controls 51% or more, they can:
        - Create a fraudulent chain faster than the rest of the network.
        - Overwrite recent transaction history by building an alternate chain (a process known as "chain reorganization").
        - Double-spend coins by invalidating transactions after they were confirmed.
3. **What Happens Below 51%?**
    - With less than 51%, the honest majority of the network will always outpace the malicious actor.
    - Even if an attacker tries to rewrite history or introduce fraudulent blocks, the rest of the network will reject their chain since it won't be the "longest" or most valid chain.

---

### **The Math Behind It**

1. **Probability in PoW:**
    
    - In Proof of Work, miners solve cryptographic puzzles to add blocks. The likelihood of any participant solving the puzzle depends on their share of the total hashrate.
    - If an attacker has less than 50% of the hashrate, their chance of solving the puzzle and catching up to or overtaking the honest chain decreases exponentially over time. This is because:
        - Honest miners will collectively produce blocks faster than the attacker.
        - The attacker's chain would eventually lag behind and be discarded by the network.
    
    Mathematically:
    
    - If the attacker's hashrate is pp and the honest network's hashrate is qq, where p+q=1p + q = 1 and p<qp < q:
        - The probability of the attack succeeding diminishes as the number of blocks to be rewritten increases, following a geometric progression.
2. **Why Not 60%, 70%, or Another Threshold?**
    
    - The minimum threshold for majority control is **50% + 1 node** (or 50% + 1 unit of power/stake). At exactly 50%, there's still ambiguity because both chains would grow at the same rate. By surpassing this threshold, the attacker can consistently outpace the honest network.
    - Any threshold higher than 50% is redundant because control is already guaranteed beyond that.

---

### **Implications of the 51% Attack**

1. **Practical Challenges:**
    
    - Acquiring 51% of a large network's computational power (PoW) or staking assets (PoS) is often prohibitively expensive.
    - For PoW, the attacker would need to acquire or control more than half of the global mining power.
    - For PoS, the attacker would need to buy or control more than half of the total staked tokens, driving up token prices and increasing costs.
2. **Network Size Matters:**
    
    - Smaller networks are more vulnerable to 51% attacks because their mining/staking resources are limited and easier to acquire.
    - Larger networks like Bitcoin and Ethereum are highly secure due to their vast mining/staking ecosystems.

---

### **Summary**

The "51%" threshold ensures that any attacker attempting to manipulate the blockchain must overcome the collective resources of the majority. This is a foundational principle in blockchain security, leveraging decentralized decision-making to protect the network from single points of failure or malicious actors. The number could theoretically be different (e.g., 60%) in systems with alternative consensus rules, but in most cases, **50% + 1** is sufficient to guarantee dominance.