# How it works

#### Definition

Builders compose route through our API by specifying actions, parameters, and risk constraints such as maximum slippage and minimum health factor. Each flows includes:

* Collateral sourcing (e.g., weETH on mainnet)
* Venue-specific actions (e.g., supply/borrow on Aave, open/close position on Hyperliquid)
* Bridging (e.g., Across: USDC from Mainnet → Hyperliquid)
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
