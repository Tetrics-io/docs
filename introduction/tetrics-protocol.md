# TETRICS protocol

### **What is** TETRICS **protcol ?**

TETRICS protocol is an intent‑centric framework that streamlines complex workflows by translating user-specified transaction intents into efficient, batched on‑chain operations. Leveraging the [EIP‑7521](https://eips.ethereum.org/EIPS/eip-7521) standard & anoma's architecture, users can submit signed intents for activities like trading, staking, yield farming, and more across liquidity fragmentation. These intents are then aggregated and optimized through a specialized network of solvers, ensuring that transactions are executed in a secure, cost‑efficient manner.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>TETRICS Protocol Architecture</p></figcaption></figure>

### **How It Works**

{% stepper %}
{% step %}
_**Intent Submission**_

Users create and sign transaction intents that encapsulate high‑level actions without worrying about the underlying blockchain intricacies.
{% endstep %}

{% step %}
_**Batching & Aggregation**_

Once received, intents are grouped into batches. This allows solvers to analyze a set of intents collectively, increasing the opportunity to match and optimize execution paths.
{% endstep %}

{% step %}
_**Solver Optimization**_

Solvers act as intelligent agents that scan each batch to find the most efficient execution route. They prioritize intra‑batch matches and, if necessary, expand their search to external on‑chain and off‑chain liquidity sources to ensure optimal execution with reduced gas costs and enhanced security.

TETRICS combines modern, intent‑based design with robust transaction orchestration and automation. By enabling users to simply declare their desired outcomes, it abstracts away the underlying operations complexities across liquidity fragmentation, offering a powerful and scalable solution for next‑generation on-chain strategy workflows.

For further details on each component and technical deep-dives, please refer to our dedicated sections on the EIP‑7521 Intent Framework, Solver Communication Strategies, and the Open‑Source Adapter Marketplace.
{% endstep %}
{% endstepper %}
