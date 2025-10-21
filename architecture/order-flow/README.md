# Order Flow

The TETRICS workflow operates on the premise that users only need to specify their desired outcomes, allowing the system to handle the complex transaction orchestration. Technically, this protocol converts high-level signed intents into optimized, atomic on-chain transactions. In its initial version (V0), this is achieved through a relayer model, as illustrated below. This section outlines the complete process of the system and highlights the technical advantages of this declarative approach.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

### Detailed End‑to‑End Flow

#### Phase 1: Validation

1. **Composition**\
   End user(exchanges/individual users) composes the know hows of collateral.
2. **Parameter Validation**\
   The SDK validates using API and JSON protocol configurations. A generic validator confirms all parameters.

#### Phase 2: Permit2 Signing

3. **Batch Payload Preparation**\
   The API prepares the Permit2 batch payload.
4. **Signature Collection**\
   The user signs an EIP-712 message for gasless approval.

#### Phase 3: Ethereum Execution

5. **Token Transfer**\
   Permit2 transfers tokens from the user to the executor.
6. **Stake ETH with Lido**\
   Stake ETH to receive stETH.
7. **Wrap stETH to wstETH**\
   Wrap stETH to obtain wstETH.
8. **Supply Collateral to Morpho**\
   Supply wstETH as collateral.
9. **Borrow USDC from Morpho**\
   Borrow USDC.
10. **Bridge USDC with Across**\
    Bridge USDC to Hyperliquid.

#### Phase 4: Cross-Chain Bridge

11. **Relayer Processing**\
    Across relayers process the bridge operation.
12. **USDC Unlocking**\
    USDC is unlocked on Hyperliquid.

#### Phase 5: Hyperliquid Execution

13. **Supply USDC to HyperLend**\
    Supply USDC to earn yield.

#### Phase 6: Receipt Aggregation

14. **Transaction Receipt Collection**\
    The API collects all transaction receipts.
15. **Receipt Return**\
    The details are returned to the SDK, frontend, and user.

#### Phase 7: Error Handling

16. **Execution Monitoring**\
    If any action fails, execution halts, returning partial results with error information.
