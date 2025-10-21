# Contracts

### Architecture Overview

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

**UniExecutor**\
The universal execution engine with Permit2 support:

* Manages protocol adapter registry
* Executes single and batch operations
* Integrates with Permit2 for gasless approvals
* Supports conditional execution logic
* Provides reentrancy protection
* Enables multicall operations

#### Key Functions:

* `executeAction(Action)`: Execute a single protocol action
* `executeBatch(Action[])`: Atomically execute multiple actions
* `executeWithPermit2(Action, Permit2Transfer)`: Execute with gasless approval
* `executeBatchWithPermit2(...)`: Batch execution with Permit2
* `executeConditional(ConditionalAction)`: Execute conditionally based on balance checks
* `multicallWithValue(bytes[], uint256[])`: Multi-call with value splitting

#### Security Modules

**PriceValidator**

* Integrates RedStone oracle for price validation
* Provides slippage protection (default max 10%)
* Checks for price staleness (max 5 minutes)
* Supports batch price validation

**MultiSigManager**

* Facilitates multi-signature governance
* Includes a 24-hour timelock for critical operations
* Provides emergency execution mode
* Manages ownership with voting

### Protocol Adapters

#### Ethereum Adapters

* **LidoAdapter**: Stake ETH to receive stETH\
  Methods: `deposit(amount)`
* **WstETHAdapter**: Wrap and unwrap stETH to and from wstETH\
  Methods: `wrap(amount)`, `unwrap(amount)`
* **MorphoAdapter**: Interact with Morpho for collateral and borrowing\
  Methods: `supply(amount)`, `borrow(amount)`, `repay(amount)`, `withdraw(amount)`

#### Cross-Chain Adapter

* **AcrossAdapter**: Bridge assets from Ethereum to Hyperliquid\
  Method: `deposit(token, amount, destinationChainId, recipient)`

#### Hyperliquid Adapters

* **StakedHypeAdapter**: Stake and unstake HYPE\
  Methods: `stake(amount)`, `unstake(amount)`
* **HyperLendAdapter**: Aave V3-style lending protocol on Hyperliquid\
  Methods: `supply(asset, amount)`, `borrow(asset, amount)`, `repay(asset, amount)`, `withdraw(asset, amount)`
* **FelixAdapter**: Collateralized Debt Position (CDP) protocol\
  Methods: `openCdp(collateral, amount)`, `deposit(cdpId, amount)`, `withdraw(cdpId, amount)`, `borrow(cdpId, amount)`, `repay(cdpId, amount)`
* **HyperBeatAdapter**: Meta vault with automated strategy management\
  Methods: `deposit(asset, amount, vault, recipient)`, `withdraw(asset, shares, vault, recipient)`, `swap(tokenIn, tokenOut, amountIn, minAmountOut, recipient)`
