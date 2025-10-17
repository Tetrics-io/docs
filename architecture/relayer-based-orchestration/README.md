# Relayer-Based Orchestration

Tetrics unifies complex, multi-leg flows into a single transaction, reducing execution risk and enabling a seamless unified-margin experience on Hyperliquid.

<mark style="color:$success;">Add some image?</mark>

1. Builders define flows via JSON/REST API \
   (e.g., "Supply wETH on Aave → Borrow USDC on Aave → Bridge USDC to destination, Hyperliquid core or designated HIP-3 Exchange)
2. A relayer sequences and executes actions atomically on the same chain or orchestrates cross-chain flows with settlement guarantees.
3. Built-in safeguards include pre-trade validation, slippage guards, health checks, and failure recovery with compensating actions.

