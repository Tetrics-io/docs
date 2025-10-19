# Roadmap

| Feature          | Today (Live)          | Next (Intent/Solver Era)          |
| ---------------- | --------------------- | --------------------------------- |
| **Execution**    | Relayer orchestration | Anoma transport + solver auctions |
| **Privacy**      | Public mempool        | Sealed-bid batch auctions         |
| **Atomicity**    | Same-chain atomic     | Cross-chain intent bundles        |
| **Optimization** | Adapter-level routing | Portfolio-aware solver search     |
| **Venues**       | Hyperliquid + EVM L2s | + Solana + Cosmos + non-EVM       |

### Q4 2025 (Oct - Dec)

**Theme:** Foundation Hardening & Protocol Coverage\
**Objective:** Stabilize the core and integrate top exchanges.

**Key Deliverables**

* **Relayer Improvements:**
  * Finalize collateral composition ✅
  * Enhance API/authentication
  * Implement observability and rate limits
* **Protocol Expansion:**
  * Add 4–6 high-priority protocol adapters (based on partner exchange requirements)
  * Develop demo integration UI
* **Architecture & Planning:**
  * Draft solver-mode architecture
  * Shortlist auction parameters
  * Develop Anoma/Taiga integration plan
* **Security Enhancements:**
  * Complete threat model v1
  * Establish fuzzing harnesses
  * Book audit slot

**Key Performance Indicators (KPIs)**

* Total weekly tx executed
* Success rate of executions
* Coverage of adapters
* 95th percentile latency (p95 latency)

***

### Q1 2026 (Jan - Mar)

**Theme:** Solver-mode MVP & Framework v0\
**Objective:** Enhance execution through competitive solving

**Goals and Milestones:**

* **Release:** Ship Solver-mode behind a feature flag (includes quote/intent APIs, simulation, and scoring).
* **Prototyping:** Develop Taiga sealed-bid prototype on testnet; initiate Anoma integration scaffolding.
* **Framework Development:** Establish Adapter framework v0, including a private registry, SDK, and guide.
* **Compliance Preparation:** Lay compliance foundations with KYC for professional solvers and implement log retention policies.
* **Security Measures:** Conduct an internal security review, execute static and dynamic analysis, and begin Audit #1.

**Key Performance Indicators (KPIs):**

* Solver fill rate percentage
* Average clearing time
* Number of external adapter contributions

***

### Q2 2026 (Apr - Jun)

**Theme:** Solver Beta & Interest-Free Margin R\&D\
**Objective:** Enhance fill rates and investigate capital efficiency.

**Deliverables:**

* **Solver Beta:** Launch on testnet and controlled mainnet; monitor economic metrics and set guardrails.
* **Taiga End-to-End:** Implement sealed-bid system; introduce Anoma interop Beta.
* **Adapter framework:** Open public beta with incentives.
* **Interest-Free Margin R\&D:** Develop risk engine v1 (limits and liquidation), perform simulations.
* **Security:** Address findings from Audit #1 and initiate Audit #2 covering protocol and off-chain solver.

**KPIs:**

* Daily intent rates
* MEV leakage compared to baseline
* Monthly marketplace contributions

***

### Q3 2026 (Jul - Sept)

**Theme:** Solver GA & LPaaS v1\
**Objective:** Finalize solving solutions for production, and launch Lending-Pool-as-a-Service (LPaaS).

**Deliverables:**

* **Solver GA:** Collaborate with exchange(s); include SLO/SLA, and create on-call incident playbooks.
* **Interest-Free Margin Pilot:** Test with partner exchange in limited cohorts.
* **LPaaS v1:** Develop factory settings, risk parameters, and monitoring tools for initial exchange.
* **Liquidity:** Finalize designs for sharing/offset; create specs for cross-venue credit lines.
* **Security:** Wrap up Audit #2 and initiate on-chain monitoring.

**KPIs:**

* GMV routed through exchanges
* Gross margin per intent
* Pool utilization rates

***

### Q4 2026 (Oct - Dec)

**Theme:** Liquidity Sharing GA & P2P Fixed-Rate Alpha\
**Objective:** Enable capital sharing across pools and trial P2P lending functions.

**Deliverables:**

* **Liquidity Sharing GA:** Implement routing and netting across partner pools.
* **P2P Fixed-Rate Alpha:** Develop matching, rate oracle, and credit scoring.
* **Adapter framework GA:** Launch with revenue-sharing, bounties, and ranking system.
* **Economic Safety:** Introduce checks and circuit breakers.

**KPIs:**

* Credit turnover rates
* Target default rate (\~0%)
* Revenue from external adapters

***

### Q1 2027 (Jan - Mar)

**Theme:** P2P Beta & Ecosystem Scaling\
**Objective:** Expand the lender/borrower base and grow the ecosystem.

**Deliverables:**

* **P2P Fixed-Rate Beta:** Rollout regionally, ensure compliance alignment.
* **Adapter Scaling:** Integrate long-tail protocols and introduce self-serve LPaaS for exchanges.
* **Security:** Conduct post-GA review and a red-team exercise.

**KPIs:**

* Number of active lenders/borrowers
* Volume of matched transactions
* Retention rates
* Net revenue growth

***
