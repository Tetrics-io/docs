# Adapter Framework

The Tetrics Adapter Framework provides a flexible, registry-based system for integrating DeFi protocols without enforcing rigid interfaces.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### How It Works

#### Protocol Registration

* Each adapter is registered with UniExecutor by protocol name (e.g., "lido", "morpho").
* Executor maintains a mapping: `mapping(string => address) public protocols`.
* Actions specify the protocol name and method to call.

#### BaseAdapter Foundation

* All adapters inherit from `BaseAdapter` (`src/adapters/BaseAdapter.sol`).
* Provides common utilities: token transfers, approvals, balance management.
* No enforced function signatures - adapters define their own interfaces.

#### Protocol-Specific Methods

Each adapter exposes methods specific to its protocol. Examples include:

* **LidoAdapter**:
  * `deposit(uint256 amount)`
* **MorphoAdapter**:
  * `supply(uint256 amount)`
  * `borrow(uint256 amount)`
* **FelixAdapter**:
  * `openCdp(address collateral, uint256 amount)`

#### Dynamic Method Calls

* UniExecutor uses low-level calls to invoke adapter methods.
* Action struct encodes the method signature and parameters.
* Flexibility to support any protocol without interface changes.

#### Adapter Structure

**Example: LidoAdapter**

```solidity
contract LidoAdapter is BaseAdapter {
    address public immutable executor;
    address public immutable stETH;

    constructor(address _executor, address _stETH) {
        executor = _executor;
        stETH = _stETH;
    }

    /// @notice Stake ETH and receive stETH
    function deposit(uint256 amount) external payable returns (uint256) {
        // Protocol-specific implementation
        // ...
    }
}
```
