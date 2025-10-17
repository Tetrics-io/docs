# Role of Searchers & Resolvers

### Searchers

Searchers act as real-time data acquisition agents within the solver ecosystem. They continuously monitor both on‑chain and off‑chain data sources, gathering critical market conditions, liquidity statistics, and external event signals.

* **Function**: By feeding the latest data into the solver module, searchers ensure that optimization algorithms have up-to-date information, which is crucial for making accurate matching and execution decisions.
* **Impact**: This proactive monitoring helps TETRICS adapt quickly to market fluctuations, ensuring that the execution plan remains optimal even in volatile conditions.

### Resolvers

Once the solvers generate an optimized execution plan, resolvers take charge of finalizing the plan for on‑chain execution.

* &#x20;**Function**: Resolvers reconcile the planned transactions with the current state of the blockchain and external protocols, resolving any conflicts or discrepancies that may arise due to timing or network changes.
* **Impact**: This final arbitration ensures atomic execution, meaning that either all components of the plan are successfully executed or the transaction is fully reverted, thereby preserving user funds and maintaining system integrity.
