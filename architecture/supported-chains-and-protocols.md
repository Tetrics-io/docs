# Supported Protocols

## Supported Protocols

Tetrics SDK supports 8 DeFi protocols across Ethereum and Hyperliquid. This page provides an overview of all available protocols and their capabilities.

### Protocol Matrix

| Protocol         | Chain       | Category | Methods                                   | Permit2 |
| ---------------- | ----------- | -------- | ----------------------------------------- | ------- |
| **Lido**         | Ethereum    | Staking  | deposit                                   | ❌       |
| **wstETH**       | Ethereum    | Wrapping | wrap, unwrap                              | ✅       |
| **Morpho**       | Ethereum    | Lending  | supply, borrow, repay, withdraw           | ✅       |
| **Across**       | Ethereum    | Bridging | deposit                                   | ✅       |
| **HYPE Staking** | Hyperliquid | Staking  | stake, unstake                            | ✅       |
| **HyperLend**    | Hyperliquid | Lending  | supply, borrow, repay, withdraw           | ✅       |
| **Felix**        | Hyperliquid | CDP      | openCdp, deposit, withdraw, borrow, repay | ✅       |
| **HyperBeat**    | Hyperliquid | Vault    | deposit, withdraw, swap                   | ✅       |

### Ethereum Protocols

#### Lido - ETH Staking

Stake ETH to receive stETH (liquid staking token).

```typescript
{
  chain: 'ethereum',
  protocol: 'lido',
  method: 'deposit',
  params: {
    amount: '1000000000000000000' // 1 ETH in wei
  },
  value: '1000000000000000000' // ETH value to send
}
```

**Returns**: stETH tokens (1:1 ratio with ETH)

#### wstETH - stETH Wrapping

Wrap stETH into wstETH (wrapped staked ETH) for DeFi composability.

```typescript
// Wrap stETH to wstETH
{
  chain: 'ethereum',
  protocol: 'wsteth',
  method: 'wrap',
  params: {
    stETHAmount: '1000000000000000000' // 1 stETH
  }
}

// Unwrap wstETH to stETH
{
  chain: 'ethereum',
  protocol: 'wsteth',
  method: 'unwrap',
  params: {
    wstETHAmount: '900000000000000000' // ~0.9 wstETH
  }
}
```

**Note**: wstETH/stETH ratio changes over time due to staking rewards

#### Morpho - Lending & Borrowing

Supply collateral and borrow assets using Morpho Blue.

```typescript
// Supply collateral
{
  chain: 'ethereum',
  protocol: 'morpho',
  method: 'supply',
  params: {
    amount: '1000000000000000000', // 1 wstETH
    marketId: '0x...' // Market ID
  }
}

// Borrow USDC
{
  chain: 'ethereum',
  protocol: 'morpho',
  method: 'borrow',
  params: {
    amount: '1000000000', // 1000 USDC (6 decimals)
    marketId: '0x...'
  }
}
```

#### Across - Cross-Chain Bridge

Bridge assets from Ethereum to Hyperliquid.

```typescript
{
  chain: 'ethereum',
  protocol: 'across',
  method: 'deposit',
  params: {
    destinationChainId: '999', // Hyperliquid chain ID
    amount: '1000000000000000000',
    recipient: '0x...' // Recipient on destination chain
  },
  value: '1000000000000000000' // ETH to bridge
}
```

### Hyperliquid Protocols

#### HYPE Staking

Stake HYPE tokens to receive beHYPE (boosted HYPE).

```typescript
// Stake HYPE
{
  chain: 'hyperliquid',
  protocol: 'hype-staking',
  method: 'stake',
  params: {
    amount: '1000000000000000000' // 1 HYPE
  }
}

// Unstake beHYPE
{
  chain: 'hyperliquid',
  protocol: 'hype-staking',
  method: 'unstake',
  params: {
    amount: '1000000000000000000' // 1 beHYPE
  }
}
```

#### HyperLend - Aave-Style Lending

Aave V3-style lending protocol on Hyperliquid.

```typescript
// Supply assets
{
  chain: 'hyperliquid',
  protocol: 'hyperlend',
  method: 'supply',
  params: {
    asset: '0x...', // Token address
    amount: '1000000000000000000'
  }
}

// Borrow assets
{
  chain: 'hyperliquid',
  protocol: 'hyperlend',
  method: 'borrow',
  params: {
    asset: '0x...',
    amount: '500000000' // 500 USDC
  }
}
```

#### Felix - CDP Protocol

Create Collateralized Debt Positions (CDPs) and mint fUSDC.

```typescript
// Open CDP
{
  chain: 'hyperliquid',
  protocol: 'felix',
  method: 'openCdp',
  params: {
    collateral: 'ETH',
    amount: '1000000000000000000' // 1 ETH
  }
}

// Borrow fUSDC
{
  chain: 'hyperliquid',
  protocol: 'felix',
  method: 'borrow',
  params: {
    cdpId: '1',
    amount: '1000000000' // 1000 fUSDC
  }
}
```

#### HyperBeat - Meta Vault

Automated strategy vault with multiple asset support.

```typescript
// Deposit to vault
{
  chain: 'hyperliquid',
  protocol: 'hyperbeat',
  method: 'deposit',
  params: {
    asset: '0x...',
    amount: '1000000000000000000',
    vault: '0x...', // Vault address
    recipient: '0x...'
  }
}

// Swap within vault
{
  chain: 'hyperliquid',
  protocol: 'hyperbeat',
  method: 'swap',
  params: {
    tokenIn: '0x...',
    tokenOut: '0x...',
    amountIn: '1000000000000000000',
    minAmountOut: '950000000', // Slippage protection
    recipient: '0x...'
  }
}
```

### Query Available Protocols

Get a real-time list of all supported protocols:

```typescript
const client = TetricsClient.fromApiKey(keyId, secret)

const protocols = await client.getProtocols()

console.log(`Total protocols: ${protocols.total_protocols}`)

protocols.protocols.forEach(protocol => {
  console.log(`${protocol.name} (${protocol.chain}):`)
  console.log(`  Methods: ${protocol.supported_methods.join(', ')}`)
  console.log(`  Contract: ${protocol.contract_address}`)
  console.log(`  Requires approval: ${protocol.requires_approval}`)
})
```

### Protocol Categories

#### Staking Protocols

* **Lido**: Liquid ETH staking
* **HYPE Staking**: HYPE token staking

#### Lending Protocols

* **Morpho**: Over-collateralized lending
* **HyperLend**: Aave-style lending

#### CDP Protocols

* **Felix**: Collateralized debt positions

#### Bridging Protocols

* **Across**: Cross-chain asset transfer

#### Vault Protocols

* **HyperBeat**: Automated strategy vaults

#### Token Wrapping

* **wstETH**: Wrapped staked ETH

### Common Execution Patterns

#### Stake and Wrap

```typescript
[
  // 1. Stake ETH on Lido
  {
    chain: 'ethereum',
    protocol: 'lido',
    method: 'deposit',
    params: { amount: '1000000000000000000' },
    value: '1000000000000000000'
  },
  // 2. Wrap stETH to wstETH
  {
    chain: 'ethereum',
    protocol: 'wsteth',
    method: 'wrap',
    params: { stETHAmount: '1000000000000000000' }
  }
]
```

#### Collateral and Borrow

```typescript
[
  // 1. Supply wstETH as collateral
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'supply',
    params: {
      amount: '1000000000000000000',
      marketId: '0x...'
    }
  },
  // 2. Borrow USDC
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'borrow',
    params: {
      amount: '1000000000',
      marketId: '0x...'
    }
  }
]
```

#### Cross-Chain Unified Margin

```typescript
[
  // 1. Bridge ETH to Hyperliquid
  {
    chain: 'ethereum',
    protocol: 'across',
    method: 'deposit',
    params: {
      destinationChainId: '999',
      amount: '1000000000000000000',
      recipient: '0x...'
    },
    value: '1000000000000000000'
  },
  // 2. Supply to HyperLend on Hyperliquid
  {
    chain: 'hyperliquid',
    protocol: 'hyperlend',
    method: 'supply',
    params: {
      asset: '0x...',
      amount: '1000000000000000000'
    }
  }
]
```

### Parameter Formats

#### Amount Format

Always use strings in wei (18 decimals) or token's smallest unit:

```typescript
// ✅ Correct
amount: '1000000000000000000' // 1 ETH

// ❌ Wrong
amount: 1 // Number type
amount: '1' // 1 wei, not 1 ETH
```

#### Address Format

Use checksummed addresses:

```typescript
// ✅ Correct
asset: '0xae7ab96520DE3A18E5e111B5EaAb095312D7fE84'

// ❌ Wrong (lowercase)
asset: '0xae7ab96520de3a18e5e111b5eaab095312d7fe84'
```

### Protocol Discovery

Get detailed protocol information:

```typescript
const discovery = await client.getDiscoveryInfo()

console.log(`Total protocols: ${discovery.total_protocols_discovered}`)
console.log(`Enabled: ${discovery.total_protocols_enabled}`)

Object.entries(discovery.protocols_by_chain).forEach(([chain, protocols]) => {
  console.log(`${chain}: ${protocols.join(', ')}`)
})
```
