# Privacy Preservation

### Shielded Intents

Exposing a trader’s margin positions on-chain is risky — especially when they are collateralizing thin-liquidity assets.

In most DeFi protocols today, every action is publicly visible on-chain, revealing who did what and at what time. While this transparency provides verifiability, it also leaks sensitive data—from user balances to strategy details. This can be detrimental to businesses or advanced traders who rely on proprietary alpha.

The Anoma architecture confronts this challenge head-on by distinguishing between “the who” and “the what,” i.e., the identity of the user (or solver) and the data/logic of their intents. By controlling which parts of an intent are visible, we can preserve privacy of traders’ margin positions.

### Intent Privacy Levels

1. **Transparent Intents**
   * Suitable for standard DeFi transactions where both user identity and transaction details can be public.
2. **Shielded Intents**
   * Offers pseudonymity by concealing user identity while exposing transaction data to authorized solvers and zero-knowledge provers for validation.
3. **Private Intents**
   * Designed for maximum secrecy to protect proprietary methods.
   * Solvers see only encrypted data, ensuring correctness via ZK proofs or cryptographic methods.
   * Hides both user identity and transaction details using technologies like TEEs, MPC, or Threshold FHE.

### Protecting Proprietary Transactions

1. **Executing Transaction with Minimal Exposure**
   * Solvers can execute or match trades by verifying only essential constraints, maintaining strategy privacy and user anonymity.
   * Using zero-knowledge proofs or partial disclosure, solvers validate logic without revealing details, either off-chain or with minimal on-chain data.
2. **Importance of Privacy**
   * **Protection Against Attack**: Publicly exposing margin operations can invite malicious actors to trigger intentional liquidations, exploit MEV and front-run execution, undermining the trader’s original intent.
   * **Enterprise Adoption**: Institutions demand confidential trading practices to protect positions and risk parameters from competitors.
   * **Competitive Edge**: Hedge funds and quants depend on unique insights, which lose value if exposed on-chain.

