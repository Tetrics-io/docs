# Order Flow

TETRICS workflow is built on the principle that users should simply declare their desired outcomes and leave the intricate transaction orchestration to the system. In technical terms, the protocol translates high-level signed intents into an optimized, atomic on‑chain transaction. This section details the end‑to‑end flow of the system and the technical benefits of this declarative approach.

### Detailed End‑to‑End Flow

1. _**Intent Submission**_\
   Users specify their desired operation by signing a message (e.g., “buy 100 tokens if the price is ≤ $1”), adhering to EIP-7521 for structured, secure, and interoperable intents.
2. _**Batch Aggregation**_
   * **Standardization:** Intents are standardized to ensure security and interoperability.
   * **Grouping:** Intents are collected until a predefined batch size is reached, enhancing privacy and liquidity through aggregation.
3. _**Solver Optimization**_
   * **Intra‑Batch Matching:** Intelligent solvers find optimal matches within the batch to minimize gas fees and latency.
   * **External Liquidity Integration:** If no match is found, solvers dynamically query on-chain and off-chain liquidity sources.
4. _**Adapter Framework Integration**_
   * **Algorithmic Processing:** Custom algorithms ensure efficient matching and optimization with minimal computational overhead.
   * **Protocol Bridging:** The framework integrates diverse DeFi/CeFi protocols, using standardized APIs to normalize data and incorporate market insights.
5. _**Execution Engine Assembly**_
   * **Atomic Transaction Construction:** Optimized plans are compiled into a single atomic transaction, ensuring all operations execute seamlessly or revert together.
   * **Gas Optimization Techniques:** Engine consolidates actions to reduce gas usage and transaction fees.
6. _**On‑Chain Transaction Execution**_
   * **Submission:** The engine executes consolidated actions on-chain into one atomic transaction to minimize gas usage and transaction fees, finalizing the process efficiently.
   * **Verification & Confirmation:** Engine consolidates actions to reduce gas usage and transaction fees.

### Benefits of the Declarative Approach

{% hint style="success" %}
1. **Simplicity**\
   Users specify their desires (e.g., "buy tokens at $1") without dealing with the complexities of smart contract interactions.
2. **Efficiency & Optimization**\
   Batching intents with intelligent solvers optimizes execution paths, lowering gas costs and reducing latency.
3. **Security & Atomicity**\
   The atomic execution model processes transactions entirely, reducing partial failures and minimizing exposure to front-running attacks.
4. **Scalability**\
   Users specify their desires (e.g., "buy tokens at $1") without dealing with the complexities of smart contract interactions.By batching multiple intents and integrating diverse liquidity sources, the protocol efficiently handles high transaction volumes without performance loss.
5. **Interoperability**\
   The use of standardized formats (EIP-7521) and a modular adapter framework ensures seamless integration across various protocols and platforms.
{% endhint %}
