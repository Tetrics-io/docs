# Solvers

Solvers are the smart agents behind TETRICS protocol that take user-submitted intents and figure out the most efficient way to execute them. They work like a matchmaker in a busy marketplace—analyzing and optimizing transactions so that everything runs smoothly onchain.

### **What Are Solvers?**

Solvers are specialized components that scan batches of blockchain intents to find the best execution paths. They aim to match intents from different users, optimizing for lower fees, speed, and overall security. By leveraging real‑time data and various liquidity sources, solvers ensure that every transaction is processed in the most effective manner possible.

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### **How Do Solvers Work?**

**1. Batch Analysis:**

When multiple intents are submitted (like Alice’s and Bob’s), solvers group them into batches. This collective view allows them to see opportunities where intents might complement each other.

**2. Finding Matches:**

Consider Alice’s intent to buy 100 tokens if the price drops to $1 and Bob’s intent to stake tokens. A solver reviews the batch to see if Alice’s buying condition can be paired with a seller’s intent or another complementary action.&#x20;

**3. Optimization:**

If a direct match isn’t found within the batch, solvers extend their search. They look into additional onchain or offchain liquidity sources and data streams to secure the best possible execution path. This process helps minimize gas fees and improve overall transaction efficiency.
