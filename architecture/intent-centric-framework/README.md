# Intent-Centric framework

[Relayer-Based Orchestration](../relayer-based-orchestration/) will upgrades to signed intents under EIP-7521 and Anoma's architecture.

* Solvers compete to find optimal execution paths, prioritizing privacy, capital efficiency, and cross-venue risk netting.
* Batch auctions and sealed-bid mechanisms mitigate MEV and information leakage.

### **Intent-Centric Framework**

Streamlines complex flows by translating user-specified transaction intents into efficient, batched on‑chain operations. Leveraging the [EIP‑7521](https://eips.ethereum.org/EIPS/eip-7521) standard & anoma's architecture, users can submit signed intents for multiple transaction flows across chains. These intents are then aggregated and optimized through a specialized network of solvers, ensuring that transactions are executed in a secure, cost‑efficient manner.

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>TETRICS Intent Centric Framework</p></figcaption></figure>

<mark style="color:$success;">Recreate this image? well hmm. Here is more should focus on cross chain complex work flows to make it great. Not mention about shield , automate is okey but</mark>&#x20;



1. _**Intent Submission**_\
   Users create and sign transaction intents that encapsulate high‑level complex actions without worrying about the underlying blockchain intricacies.
2. _**Batching & Aggregation**_\
   Once received, intents are grouped into batches. This allows solvers to analyze a set of intents collectively, increasing the opportunity to match and optimize execution paths.
3. _**Solver Optimization**_\
   Solvers act as intelligent agents that scan each batch to find the most efficient execution route. They prioritize intra‑batch matches and, if necessary, expand their search to external on‑chain and off‑chain liquidity sources to ensure optimal execution with reduced gas costs and enhanced security.\
   TETRICS combines modern, intent‑based design with robust transaction orchestration. By enabling builders to simply declare their desired outcomes, it abstracts away the underlying operations complexities across liquidity fragmentation, offering a powerful and scalable solution for next‑generation cross-chain multi-step flows.\
   For further details on each component and technical deep-dives, please refer to our dedicated sections on the [EIP‑7521 Intent Framework](https://eips.ethereum.org/EIPS/eip-7521), [Solver Communication](solvers/), and the [Adapter Framework](../../adapter-framework.md).
