# Relayer-Based Orchestration

Tetrics unifies complex, multi-leg flows into a single transaction, reducing execution risk and enabling a seamless unified-margin experience on Kalshi.

1. Builders define flows via JSON/REST API\
   (e.g., "Supply wETH on Aave → Borrow USDC on Aave → Bridge USDC to destination, Kalshi)
2. A relayer sequences and executes actions atomically on the same chain or orchestrates cross-chain flows with settlement guarantees.
3. Built-in safeguards include pre-trade validation, slippage guards, health checks, and failure recovery with compensating actions.

### How it works

#### Definition

Builders compose route through our API by specifying actions, parameters, and risk constraints such as maximum slippage and minimum health factor. Each flows includes:

* Collateral sourcing (e.g., weETH on mainnet)
* Venue-specific actions (e.g., supply/borrow on Aave, open/close position on Kalshi)
* Bridging (e.g., Across: USDC from Mainnet → Kalshi)
* Risk parameters (e.g., maximum leverage, liquidation buffers)

#### Pre-Trade Validation & Risk Engine

* **Portfolio Simulation:** Computes post-trade positions, liabilities, and health across venues.
* **Guardrails:** Enforces user-configurable limits including slippage bands, minimum collateral ratios, and maximum borrow amounts.
* **Oracle Checks:** Validates prices, ensures data freshness, and rejects route that would breach health thresholds.

#### Execution Modes

* **Same-Chain Atomic:** All actions execute in a single transaction bundle with no partial failures.
* **Cross-Chain Orchestrated:** Steps sequence across domains with explicit SLAs, timeouts, and compensations for failed legs.

#### Settlement & Monitoring

* **Settlement Watchers:** Track bridge finality and gate dependent actions until funds arrive.
* **Portfolio Accounting:** Real-time position tracking, PnL, funding/borrow costs, and health alerts.
* **Failure Recovery:** Compensating actions and user-configurable retry/cancel policies.
* Portfolio-level risk checks spanning perpetuals, spot, and credit positions.
* Collateral mobility and netting under a single health factor.

#### Cross-Chain Collateral Orchestration

* Bridge selection and quote optimization (Across, deBridge, LayerZero, Axelar).
* In-flight risk management with haircuts during transfer windows.
* Settlement watchers and dependent action gating for reliable multi-hop flows.

#### Risk-Aware Flow Optimization

* Pre-execution simulation against portfolio state and market conditions.
* Failure modes with explicit recovery paths and user controls.
* Transparency through real-time flow status, gas usage, and PnL attribution.
