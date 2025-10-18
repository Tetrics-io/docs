# MEV (Maximal Extractable Value)

MEV represents the extra profit that can be captured by reordering, including, or excluding transactions within a block. In simpler terms, it’s the potential gain a miner or validator might extract by strategically ordering transactions. TETRICS is designed to mitigate the risks associated with MEV by aggregating intents into batches and using intelligent solvers that optimize execution order, thereby reducing opportunities for front-running or other exploitative behaviors.

### **MEV manipulation Problems**

* _Front-running_: Placing a transaction ahead of a pending transaction to profit from the price movement.
* _Sandwich Attacks_: Inserting transactions both before and after a target transaction, exploiting price changes.
* _Reordering & Insertion_: Manipulating the sequence of transactions to capture arbitrage opportunities.

### **Threat Models**

The risks posed by MEV can be classified as follows:

* _User-Level Risks_: Individual users may experience slippage or higher transaction fees as their orders are exploited by adversaries.
* _Protocol-Level Vulnerabilities_: Aggregated order flows or predictable patterns in transaction ordering can expose the protocol to systemic exploitation.
* _Network-Level Risks_: During periods of high volatility or congestion, the probability of MEV exploitation increases, as attackers are incentivized to rearrange transaction sequences for profit.

### **MEV Protection**

To safeguard user transactions, TETRICS  employs multiple layers of defense:

* _Batching & Aggregation_: By grouping multiple intents together, the protocol obscures individual transaction details, making it harder for malicious actors to target specific orders.
* &#x20;_Solver Optimization_: Solvers analyze batches holistically to determine the most efficient execution paths, further reducing the risk of MEV exploitation.
* &#x20;_Atomic Execution_: Transactions are executed atomically, ensuring that either all actions within a batch are successfully completed, or none are—this minimizes the impact of potential manipulation.

