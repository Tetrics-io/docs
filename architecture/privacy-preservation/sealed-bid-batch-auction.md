# Sealed-Bid Batch Auction

A **sealed-bid batch auction** is an on-chain settlement process in which multiple trades or intents are collected within a fixed time window (“batch”). Each solver submits a commit (i.e., a hash of their proposed solution) off-chain or on-chain, then later reveals the full details of their bid. The system picks the best solution and settles it atomically, ensuring fair competition and minimal front-running.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

### Transaction Settlement Process

#### 1. Intent Submission & Batch Window Collection

* **Intent Submission:** Users sign and submit requests, such as trades or yield flows, within a predetermined batch window (e.g., N blocks).
* **Visibility:** Solvers can see user intents within the batch but not the specific solutions proposed by others.
* **Storage:** Intents are stored either off-chain or in a minimal on-chain structure for reference.

#### 2. Commit Phase

* **Hashing & Commitment:** Solvers compute and hash details about the routes, fees, and constraints.
* **No Copying:** Only the hash is submitted, ensuring competitors cannot see specific fees or routes.
* **Storage of Minimal Data:** Ensures reduced on-chain data usage.

#### 3. Reveal Phase

* **Disclosure:** After the commit deadline, solvers reveal the details of their solutions previously committed.
* **Comparison:** Solutions are evaluated based on fees, slippage, and yield outcomes.
* **Best Bid Selection:** Routes with the lowest fee or highest user value are chosen.

#### 4. Atomic On-Chain Execution & Settlement

* **Transaction Finalization:** The entire batch is finalized in one transaction.
* **Atomicity:** If any step fails, such as a loss of liquidity, the transaction reverts entirely.
* **Batch Settlement:** Aggregation of multiple trades reduces on-chain interactions, optimizing gas costs.

### Optimized Blockchain Operations

#### Security & Front-Running Mitigation

* **No Early Reveal:** The commit-reveal process prevents solvers from front-running or copying others' solutions, ensuring fairness.
* **Gas & Cost Efficiency:** The transaction either succeeds or reverts entirely, eliminating partial executions.

#### Fee Distribution

* **Reward for Winning Solver:** The selected solver collects a fee, and users benefit from minimized gas fees, as settlement covers multiple trades.

By adhering to these structured phases, the system ensures efficient, secure, and cost-effective transaction settlement on the blockchain.
