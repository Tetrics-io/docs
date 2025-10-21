# Unified Margin

## Unified Margin Examples

Real-world DeFi execution plans you can run with Tetrics SDK for unified margin management across chains. Copy, customize, and deploy!

### Basic Operations

#### 1. Stake ETH on Lido

Simple ETH staking to receive stETH - building your unified margin position.

```typescript
import { TetricsClient, type ActionStep } from '@tetrics/sdk'

const client = TetricsClient.fromApiKey(keyId, secret)

const actions: ActionStep[] = [{
  chain: 'ethereum',
  protocol: 'lido',
  method: 'deposit',
  params: { amount: '1000000000000000000' }, // 1 ETH
  value: '1000000000000000000'
}]

const receipt = await client.executePlanDirect({
  name: 'Stake ETH on Lido',
  steps: actions,
  executionMode: 'atomic'
})

console.log(`stETH received! Tx: ${receipt.action_results?.[0]?.tx_hash}`)
```

**Use Case**: Earn staking rewards on your ETH without running a validator.

**Expected Returns**: \~4% APY

#### 2. Wrap stETH to wstETH

Convert stETH to wstETH for DeFi composability.

```typescript
const actions: ActionStep[] = [{
  chain: 'ethereum',
  protocol: 'wsteth',
  method: 'wrap',
  params: { stETHAmount: '1000000000000000000' } // 1 stETH
}]

const receipt = await client.executePlanDirect({
  name: 'Wrap stETH to wstETH',
  steps: actions,
  executionMode: 'atomic'
})
```

**Use Case**: wstETH is composable with other DeFi protocols (Morpho, Aave, etc).

#### 3. Supply Collateral to Morpho

Supply wstETH as collateral on Morpho Blue.

```typescript
const actions: ActionStep[] = [{
  chain: 'ethereum',
  protocol: 'morpho',
  method: 'supply',
  params: {
    amount: '1000000000000000000', // 1 wstETH
    marketId: '0x...' // wstETH/USDC market
  }
}]
```

**Use Case**: Earn supply APY while maintaining ability to borrow.

### Intermediate Workflows

#### 4. Stake and Wrap (2-Step)

Stake ETH and automatically wrap to wstETH.

```typescript
const stakeAndWrap: ActionStep[] = [
  // Step 1: Stake ETH
  {
    chain: 'ethereum',
    protocol: 'lido',
    method: 'deposit',
    params: { amount: '1000000000000000000' },
    value: '1000000000000000000'
  },
  // Step 2: Wrap stETH
  {
    chain: 'ethereum',
    protocol: 'wsteth',
    method: 'wrap',
    params: { stETHAmount: '1000000000000000000' }
  }
]

const receipt = await client.executePlanDirect({
  name: 'Stake and Wrap',
  steps: stakeAndWrap,
  executionMode: 'atomic'
})
```

**Benefits**:

* ✅ Atomic execution (all-or-nothing)
* ✅ Gas savings (\~30% vs separate txs)
* ✅ wstETH ready for DeFi

#### 5. Collateralized Borrowing

Supply collateral and borrow USDC in one transaction.

```typescript
const collateralBorrow: ActionStep[] = [
  // Step 1: Supply wstETH
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'supply',
    params: {
      amount: '2000000000000000000', // 2 wstETH (~$7000)
      marketId: '0x...'
    }
  },
  // Step 2: Borrow USDC (70% LTV)
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'borrow',
    params: {
      amount: '4900000000', // $4,900 USDC
      marketId: '0x...'
    }
  }
]

const receipt = await client.executePlanDirect({
  name: 'Collateral + Borrow',
  steps: collateralBorrow,
  executionMode: 'atomic'
})
```

**Risk Parameters**:

* Collateral: 2 wstETH (\~$7,000)
* Borrow: $4,900 USDC
* LTV: 70%
* Liquidation threshold: \~83%

#### 6. Leverage Staking

Recursive staking for amplified returns.

```typescript
const leverageStaking: ActionStep[] = [
  // 1. Stake 1 ETH
  {
    chain: 'ethereum',
    protocol: 'lido',
    method: 'deposit',
    params: { amount: '1000000000000000000' },
    value: '1000000000000000000'
  },
  // 2. Wrap stETH
  {
    chain: 'ethereum',
    protocol: 'wsteth',
    method: 'wrap',
    params: { stETHAmount: '1000000000000000000' }
  },
  // 3. Supply as collateral
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'supply',
    params: {
      amount: '1000000000000000000',
      marketId: '0x...'
    }
  },
  // 4. Borrow ETH (70% LTV)
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'borrow',
    params: {
      amount: '700000000000000000', // 0.7 ETH
      marketId: '0x...'
    }
  },
  // 5. Stake borrowed ETH
  {
    chain: 'ethereum',
    protocol: 'lido',
    method: 'deposit',
    params: { amount: '700000000000000000' },
    value: '700000000000000000'
  }
]

const receipt = await client.executePlanDirect({
  name: 'Leveraged Staking 1.7x',
  steps: leverageStaking,
  executionMode: 'atomic'
})
```

**Effective Exposure**: 1.7 ETH staked with 1 ETH capital

**⚠️ Risks**: Liquidation risk if ETH price drops significantly

### Advanced Cross-Chain Unified Margin

#### 7. Ethereum to Hyperliquid Yield

Bridge ETH to Hyperliquid and supply to HyperLend.

```typescript
const crossChainYield: ActionStep[] = [
  // Step 1: Bridge ETH to Hyperliquid
  {
    chain: 'ethereum',
    protocol: 'across',
    method: 'deposit',
    params: {
      destinationChainId: '999',
      amount: '1000000000000000000',
      recipient: '0xYourAddress'
    },
    value: '1000000000000000000'
  },
  // Step 2: Supply to HyperLend
  {
    chain: 'hyperliquid',
    protocol: 'hyperlend',
    method: 'supply',
    params: {
      asset: '0x...', // ETH address on Hyperliquid
      amount: '1000000000000000000'
    }
  }
]

const receipt = await client.executePlanDirect({
  name: 'Cross-Chain Yield',
  steps: crossChainYield,
  executionMode: 'sequential' // Cross-chain requires sequential
})
```

**Expected Returns**: \~5-8% APY on HyperLend

#### 8. HYPE Staking and Lending

Stake HYPE for beHYPE, then use as collateral for unified margin.

```typescript
const hypePlan: ActionStep[] = [
  // 1. Stake HYPE
  {
    chain: 'hyperliquid',
    protocol: 'hype-staking',
    method: 'stake',
    params: { amount: '1000000000000000000' } // 1 HYPE
  },
  // 2. Supply beHYPE to HyperLend
  {
    chain: 'hyperliquid',
    protocol: 'hyperlend',
    method: 'supply',
    params: {
      asset: '0x...', // beHYPE address
      amount: '1000000000000000000'
    }
  },
  // 3. Borrow USDC
  {
    chain: 'hyperliquid',
    protocol: 'hyperlend',
    method: 'borrow',
    params: {
      asset: '0x...', // USDC
      amount: '500000000' // $500 USDC
    }
  }
]
```

**Benefits**:

* Earn staking rewards on HYPE
* Earn supply APY on beHYPE
* Access to borrowed capital

#### 9. Felix CDP

Create a CDP, deposit collateral, mint fUSDC for unified margin positions.

```typescript
const felixCDP: ActionStep[] = [
  // 1. Open CDP
  {
    chain: 'hyperliquid',
    protocol: 'felix',
    method: 'openCdp',
    params: {
      collateral: 'ETH',
      amount: '1000000000000000000' // 1 ETH
    }
  },
  // 2. Borrow fUSDC (assuming CDP ID = 1)
  {
    chain: 'hyperliquid',
    protocol: 'felix',
    method: 'borrow',
    params: {
      cdpId: '1',
      amount: '1500000000' // $1,500 fUSDC
    }
  }
]
```

**Collateralization Ratio**: \~66% (safe from liquidation)

### Production Workflows

#### 10. Full Yield Optimization with Unified Margin

Complete multi-chain execution plan for maximum yield using unified margin.

```typescript
const fullYieldPlan: ActionStep[] = [
  // 1. Stake ETH on Lido
  {
    chain: 'ethereum',
    protocol: 'lido',
    method: 'deposit',
    params: { amount: '5000000000000000000' }, // 5 ETH
    value: '5000000000000000000'
  },
  // 2. Wrap all stETH to wstETH
  {
    chain: 'ethereum',
    protocol: 'wsteth',
    method: 'wrap',
    params: { stETHAmount: '5000000000000000000' }
  },
  // 3. Supply to Morpho
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'supply',
    params: {
      amount: '5000000000000000000',
      marketId: '0x...'
    }
  },
  // 4. Borrow USDC (60% LTV for safety)
  {
    chain: 'ethereum',
    protocol: 'morpho',
    method: 'borrow',
    params: {
      amount: '10500000000', // $10,500 USDC
      marketId: '0x...'
    }
  },
  // 5. Bridge USDC to Hyperliquid
  {
    chain: 'ethereum',
    protocol: 'across',
    method: 'deposit',
    params: {
      destinationChainId: '999',
      amount: '10500000000',
      recipient: '0x...'
    }
  },
  // 6. Supply USDC to HyperLend
  {
    chain: 'hyperliquid',
    protocol: 'hyperlend',
    method: 'supply',
    params: {
      asset: '0x...', // USDC
      amount: '10500000000'
    }
  }
]

const receipt = await client.executePlanDirect({
  name: 'Full Yield Optimization',
  steps: fullYieldPlan,
  executionMode: 'sequential'
})
```

**Expected Returns**:

* Lido staking: 4% APY
* Morpho supply: 2% APY
* HyperLend supply: 6% APY
* **Effective APY**: \~8-12% (on 5 ETH capital)

**Risks**:

* ⚠️ Liquidation risk if ETH drops >30%
* ⚠️ Bridge risk during transfers
* ⚠️ Smart contract risk across 4+ protocols

### Execution Plan Templates

#### Reusable Plan Builder

```typescript
class PlanBuilder {
  private actions: ActionStep[] = []

  stakeETH(amount: string) {
    this.actions.push({
      chain: 'ethereum',
      protocol: 'lido',
      method: 'deposit',
      params: { amount },
      value: amount
    })
    return this
  }

  wrapToWstETH(amount: string) {
    this.actions.push({
      chain: 'ethereum',
      protocol: 'wsteth',
      method: 'wrap',
      params: { stETHAmount: amount }
    })
    return this
  }

  supplyToMorpho(amount: string, marketId: string) {
    this.actions.push({
      chain: 'ethereum',
      protocol: 'morpho',
      method: 'supply',
      params: { amount, marketId }
    })
    return this
  }

  async execute(client: TetricsClient, name: string) {
    return client.executePlanDirect({
      name,
      steps: this.actions,
      executionMode: 'atomic'
    })
  }
}

// Usage
const plan = new PlanBuilder()
  .stakeETH('1000000000000000000')
  .wrapToWstETH('1000000000000000000')
  .supplyToMorpho('1000000000000000000', '0x...')

const receipt = await plan.execute(client, 'My Unified Margin Plan')
```

### Best Practices

#### ✅ DO

```typescript
// Validate before execute
const validation = await client.validatePlan(actions)
if (!validation.valid) {
  console.error('Invalid plan:', validation.errors)
  return
}

// Use atomic mode for same-chain execution
const receipt = await client.executePlanDirect({
  name: 'My Plan',
  steps: actions,
  executionMode: 'atomic' // All-or-nothing
})

// Check receipt
if (receipt.success) {
  console.log('Success!', receipt.execution_id)
} else {
  console.error('Failed:', receipt.error)
}
```

#### ❌ DON'T

```typescript
// Don't skip validation
await client.executePlanDirect({...}) // ❌ No validation

// Don't use atomic for cross-chain
executionMode: 'atomic' // ❌ Will fail on cross-chain

// Don't ignore errors
const receipt = await client.executePlanDirect({...})
// No error checking ❌
```

### Testing Workflows

Always test with small amounts first:

```typescript
// Test with 0.01 ETH first
const testAmount = '10000000000000000' // 0.01 ETH

const testActions = actions.map(action => ({
  ...action,
  params: {
    ...action.params,
    amount: testAmount
  },
  value: action.value ? testAmount : undefined
}))

const testReceipt = await client.executePlanDirect({
  name: 'Test Run',
  steps: testActions,
  executionMode: 'atomic'
})

if (testReceipt.success) {
  console.log('Test successful! Proceeding with full amount...')
  // Now run with real amounts
}
```
