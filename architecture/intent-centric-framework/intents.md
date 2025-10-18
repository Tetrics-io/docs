# Intents

Imagine Alice wants to buy some tokens and Bob wants to stake theirs, but neither of them wants to deal with all the technical details of how these operations happen on the blockchain. Instead of manually managing every transaction detail, they simply declare what they want to do. This high-level instruction is what we call a blockchain intent.

### **What Are Blockchain Intents?**

Blockchain intents are like clear, human-friendly instructions that tell a system what you want to achieve without requiring you to specify every underlying step. Think of it as telling your smart assistant, “I want to buy tokens,” rather than programming every action needed to make that happen.

### **How Do They Work?**

1. _**Intent Declaration**_\
   When Alice submits her intent to trade tokens, she signs a message that outlines her goal—buying tokens at a specific price or under certain conditions. Similarly, Bob could declare an intent to stake his tokens for rewards. These declarations are structured following standards like EIP‑7521 and EIP‑7683, ensuring they’re secure and interoperable across various blockchain systems.
2. _**Abstraction of Complexity**_\
   The beauty of intents is that they abstract away the nitty-gritty of blockchain operations. Users like Alice and Bob don’t need to worry about gas fees, smart contract interactions, or even the specific sequence of events needed to execute their orders. Instead, they rely on the protocol to interpret their high-level instructions.
3. _**Automated Processing**_\
   Once intents are submitted, specialized components (solvers) collect and group these intents into batches. The system then figures out the best way to process them—optimizing for cost and efficiency—without requiring further input from Alice or Bob.

### **Example:**

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

* Alice signs an intent that reads, “Buy 100 tokens if the price drops to $1.” She doesn’t need to specify which smart contract to use or how the transaction will be executed.
* Bob signs a similar intent saying, “Stake 50 tokens to earn rewards,” again leaving the technical details to the protocol.

The protocol then takes these intents, aggregates them, and uses its built-in solvers to determine the optimal way to execute both transactions. It finds the best route for Alice’s purchase and Bob’s staking, ensuring that everything happens securely, efficiently, and with minimal fees.
