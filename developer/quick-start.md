# Quick Start

## Quick Start

Get started with Tetrics SDK in less than 5 minutes! This guide will walk you through your first unified margin execution.

### Installation

```bash
# Using npm
npm install @tetrics/sdk viem

# Using pnpm
pnpm add @tetrics/sdk viem

# Using yarn
yarn add @tetrics/sdk viem
```

### Your First Execution

Let's stake ETH on Lido in just a few lines of code:

```typescript
import { TetricsClient } from '@tetrics/sdk'

// 1. Create a client with your API credentials
const client = TetricsClient.fromApiKey(
  'your-api-key-id',
  'your-api-secret'
)

// 2. Define your execution plan
const plan = {
  name: 'Stake ETH on Lido',
  actions: [{
    chain: 'ethereum',
    protocol: 'lido',
    method: 'deposit',
    params: {
      amount: '1000000000000000000' // 1 ETH in wei
    },
    value: '1000000000000000000'
  }]
}

// 3. Execute the plan
const receipt = await client.executePlanDirect({
  name: plan.name,
  steps: plan.actions,
  executionMode: 'atomic'
})

console.log('Success!', receipt)
```

### That's it! 🎉

You've just executed your first DeFi workflow with Tetrics. Here's what happened:

1. **Authentication**: You created a client with your API credentials
2. **Plan Definition**: You defined a simple staking action
3. **Execution**: The SDK handled validation, signing, and on-chain execution

### Getting an API Key

To use the SDK, you need an API key. Here's how to get one:

<figure><img src="../.gitbook/assets/Screenshot 2025-10-22 at 01.22.10.png" alt=""><figcaption></figcaption></figure>

#### Option 1: API Key from Dashboard (Production)

1. Visit [Tetrics Dashboard](https://app.tetrics.io)
2. Connect your wallet
3. Navigate to **API Keys**
4. Click **Create New Key**
5. Copy your `key_id` and `secret` (save it securely!)

#### Option 2: Wallet Authentication (Development)

For development, you can authenticate with your wallet:

```typescript
import { TetricsClient } from '@tetrics/sdk'
import { privateKeyToAccount } from 'viem/accounts'

const account = privateKeyToAccount('0x...')

// Authenticate with wallet (creates API key automatically)
const client = await TetricsClient.authenticateWithWallet(
  account.address,
  async (message) => account.signMessage({ message })
)

// Now you can use the client!
const health = await client.getHealth()
console.log(health)
```

### Environment Variables

For production apps, use environment variables:

```bash
# .env.local
NEXT_PUBLIC_TETRICS_API_URL=https://api.tetrics.io
TETRICS_API_KEY_ID=your_key_id
TETRICS_API_SECRET=your_secret
```

```typescript
// In your app
const client = TetricsClient.fromApiKey(
  process.env.TETRICS_API_KEY_ID!,
  process.env.TETRICS_API_SECRET!,
  { baseUrl: process.env.NEXT_PUBLIC_TETRICS_API_URL }
)
```

### Common Patterns

#### Check API Health

```typescript
const health = await client.getHealth()
console.log(`Status: ${health.status}`)
console.log(`Chains: ${health.chains_supported.join(', ')}`)
console.log(`Protocols: ${health.protocols_discovered}`)
```

#### Query Supported Protocols

```typescript
const protocols = await client.getProtocols()
protocols.protocols.forEach(p => {
  console.log(`${p.name} on ${p.chain}: ${p.supported_methods.join(', ')}`)
})
```

#### Validate Execution Plan Before Running

```typescript
const validation = await client.validatePlan(plan.actions)

if (!validation.valid) {
  console.error('Validation failed:', validation.errors)
} else {
  console.log('Plan valid! Estimated gas:', validation.estimated_total_gas)
  // Proceed with execution...
}
```

### Complete Example

Here's a full example with proper error handling:

```typescript
import { TetricsClient, type ActionStep } from '@tetrics/sdk'

async function stakeLidoExample() {
  // Initialize client
  const client = TetricsClient.fromApiKey(
    process.env.TETRICS_API_KEY_ID!,
    process.env.TETRICS_API_SECRET!
  )

  // Define execution plan
  const actions: ActionStep[] = [{
    chain: 'ethereum',
    protocol: 'lido',
    method: 'deposit',
    params: { amount: '1000000000000000000' },
    value: '1000000000000000000'
  }]

  try {
    // 1. Validate plan
    const validation = await client.validatePlan(actions)
    if (!validation.valid) {
      throw new Error(`Validation failed: ${validation.errors.join(', ')}`)
    }

    console.log(`Estimated gas: ${validation.estimated_total_gas}`)

    // 2. Execute plan
    const receipt = await client.executePlanDirect({
      name: 'Stake 1 ETH on Lido',
      steps: actions,
      executionMode: 'atomic'
    })

    if (receipt.success) {
      console.log('✅ Execution successful!')
      console.log(`Execution ID: ${receipt.execution_id}`)
      console.log(`Gas used: ${receipt.total_gas_used}`)
    } else {
      console.error('❌ Execution failed:', receipt.error)
    }

  } catch (error) {
    console.error('Error:', error)
  }
}

stakeLidoExample()
```

### Troubleshooting

#### "Authentication failed"

* Check that your API key and secret are correct
* Ensure you're using the right API URL
* API keys expire - create a new one if needed

#### "Validation failed"

* Check parameter formats (amounts should be strings in wei)
* Verify protocol and method names are correct
* Check that values match params for ETH transfers

#### "Rate limit exceeded"

* The SDK automatically retries with exponential backoff
* Consider upgrading your API plan for higher limits
* Check the `retry-after` header for when to retry

#### Example: Gas Savings

```typescript
// ❌ Without Tetrics: ~450k gas
// 1. approve() = 150k gas
// 2. stake() = 150k gas
// 3. wrap() = 150k gas

// ✅ With Tetrics: ~200k gas
// 1. Permit2 signature (off-chain, free)
// 2. Multicall (stake + wrap) = 200k gas
// = ~55% gas savings! 🎉
```
