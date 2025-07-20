# Flash USDT Generator - Quick Reference

## 🚀 Quick Start

```javascript
const { FlashUSDTGenerator } = require('./flash-usdt.js');

const generator = new FlashUSDTGenerator(
    'your-private-key',
    'your-infura-api-key'
);

const result = await generator.simulateFlashGeneration('300');
console.log(result.success);
```

## 📋 Main APIs

### FlashUSDTGenerator Class

| Method | Returns | Description |
|--------|---------|-------------|
| `getWalletAddress()` | `string` | Get wallet address |
| `getEthBalance()` | `Promise<string>` | Get ETH balance |
| `getUsdtBalance()` | `Promise<string>` | Get USDT balance |
| `hasSufficientBalance()` | `Promise<boolean>` | Check if balance is sufficient |
| `validateWallet()` | `Promise<Object>` | Validate wallet & network |
| `simulateFlashGeneration(amount)` | `Promise<Object>` | Run flash simulation |
| `estimateTransactionCost()` | `Promise<Object>` | Estimate gas costs |
| `getContractInfo()` | `Promise<Object>` | Get USDT contract info |
| `getNetworkStats()` | `Promise<Object>` | Get network statistics |
| `cleanup()` | `void` | Clean up resources |

### Utility Functions

| Function | Returns | Description |
|----------|---------|-------------|
| `validatePrivateKey(key)` | `boolean` | Validate private key format |
| `validateInfuraApiKey(key)` | `boolean` | Validate API key format |
| `formatUSDTAmount(amount)` | `string` | Format amount to USDT precision |

## 🔧 Configuration

```javascript
const CONFIG = {
    FLASH_AMOUNT: '300',
    NETWORK: 'mainnet',
    GAS_LIMIT: 21000,
    USDT_CONTRACT_ADDRESS: '0xdAC17F958D2ee523a2206206994597C13D831ec7',
    MIN_BALANCE_REQUIRED: ethers.parseEther('0.01')
};
```

## 📦 Imports

```javascript
// Full import
const {
    FlashUSDTGenerator,
    CONFIG,
    validatePrivateKey,
    validateInfuraApiKey,
    formatUSDTAmount
} = require('./flash-usdt.js');

// Class only
const { FlashUSDTGenerator } = require('./flash-usdt.js');
```

## 🎯 Common Patterns

### Basic Usage
```javascript
const generator = new FlashUSDTGenerator(privateKey, apiKey);
const address = generator.getWalletAddress();
const balance = await generator.getEthBalance();
const result = await generator.simulateFlashGeneration('300');
generator.cleanup();
```

### With Validation
```javascript
const validation = await generator.validateWallet();
if (validation.isValid) {
    const result = await generator.simulateFlashGeneration('300');
}
```

### Error Handling
```javascript
try {
    const generator = new FlashUSDTGenerator(privateKey, apiKey);
    const result = await generator.simulateFlashGeneration('300');
} catch (error) {
    console.error('Error:', error.message);
}
```

### Batch Operations
```javascript
const [ethBalance, usdtBalance, networkStats] = await Promise.all([
    generator.getEthBalance(),
    generator.getUsdtBalance(),
    generator.getNetworkStats()
]);
```

## 🧪 Testing

```bash
# Run all tests
npm test

# Run main script
npm start
```

## 🔒 Security

- Never expose private keys in code
- Use environment variables for sensitive data
- Validate all inputs before processing
- Always use try-catch for async operations

## 📞 Support

**Telegram**: [@flash_cryptoking1](https://t.me/flash_cryptoking1)

---

📖 For detailed documentation, see [API_DOCUMENTATION.md](./API_DOCUMENTATION.md)