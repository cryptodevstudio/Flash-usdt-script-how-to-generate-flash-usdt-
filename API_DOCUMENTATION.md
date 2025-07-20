# Flash USDT Generator - API Documentation

## Table of Contents
1. [Overview](#overview)
2. [Installation & Setup](#installation--setup)
3. [Configuration](#configuration)
4. [Core Classes](#core-classes)
5. [Utility Functions](#utility-functions)
6. [API Reference](#api-reference)
7. [Usage Examples](#usage-examples)
8. [Error Handling](#error-handling)
9. [Testing](#testing)
10. [Advanced Usage](#advanced-usage)

## Overview

The Flash USDT Generator is a Node.js application that simulates Flash USDT generation on the Ethereum blockchain using the ethers.js library. This documentation covers all public APIs, functions, and components available in the system.

### Key Features
- 🔐 Secure wallet management and validation
- 💰 Real-time balance checking (ETH and USDT)
- 🚀 Flash USDT generation simulation
- ⛽ Gas estimation and transaction cost calculation
- 📊 Network statistics and monitoring
- 🧪 Comprehensive testing suite

## Installation & Setup

### Prerequisites
- Node.js version 16.0.0 or higher
- npm package manager
- Ethereum wallet private key
- Infura API key

### Installation Steps

```bash
# Clone the repository
git clone <repository-url>
cd flash-usdt-generator

# Install dependencies
npm install

# Configure your credentials
# Edit flash-usdt.js and replace:
# - CLIENT_PRIVATE_KEY with your wallet's private key
# - INFURA_API_KEY with your Infura project ID
```

### Running the Application

```bash
# Run the main script
npm start
# or
node flash-usdt.js

# Run tests
npm test
# or
node test.js
```

## Configuration

### CONFIG Object

The `CONFIG` object contains all configuration constants:

```javascript
const CONFIG = {
    FLASH_AMOUNT: '300',           // Default flash amount in USDT
    NETWORK: 'mainnet',            // Ethereum network
    GAS_LIMIT: 21000,              // Gas limit for transactions
    USDT_CONTRACT_ADDRESS: '0xdAC17F958D2ee523a2206206994597C13D831ec7',
    MIN_BALANCE_REQUIRED: ethers.parseEther('0.01') // Minimum ETH balance
};
```

#### Configuration Properties

| Property | Type | Description | Default Value |
|----------|------|-------------|---------------|
| `FLASH_AMOUNT` | string | Amount of USDT to flash | '300' |
| `NETWORK` | string | Ethereum network to use | 'mainnet' |
| `GAS_LIMIT` | number | Gas limit for transactions | 21000 |
| `USDT_CONTRACT_ADDRESS` | string | USDT contract address | '0xdAC1...' |
| `MIN_BALANCE_REQUIRED` | BigInt | Minimum ETH balance required | 0.01 ETH |

## Core Classes

### FlashUSDTGenerator

The main class for Flash USDT generation simulation.

#### Constructor

```javascript
new FlashUSDTGenerator(privateKey, infuraApiKey, network = 'mainnet')
```

**Parameters:**
- `privateKey` (string): Ethereum wallet private key
- `infuraApiKey` (string): Infura API key for blockchain connection
- `network` (string, optional): Ethereum network name (default: 'mainnet')

**Example:**
```javascript
const generator = new FlashUSDTGenerator(
    '0x1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef',
    'your-infura-api-key',
    'mainnet'
);
```

#### Methods

##### getWalletAddress()

Returns the wallet address associated with the private key.

```javascript
const address = generator.getWalletAddress();
console.log(address); // "0x742d35Cc5454fB1b0C19c5c6bB8bb1c2C5f7C3d7"
```

**Returns:** `string` - The wallet address

##### getEthBalance()

Retrieves the current ETH balance of the wallet.

```javascript
const ethBalance = await generator.getEthBalance();
console.log(ethBalance); // "1.234567890123456789"
```

**Returns:** `Promise<string>` - ETH balance in Ether units
**Throws:** `Error` - If balance retrieval fails

##### getUsdtBalance()

Retrieves the current USDT balance of the wallet.

```javascript
const usdtBalance = await generator.getUsdtBalance();
console.log(usdtBalance); // "1500.000000"
```

**Returns:** `Promise<string>` - USDT balance in USDT units
**Throws:** `Error` - If balance retrieval fails

##### hasSufficientBalance()

Checks if the wallet has sufficient ETH balance for transactions.

```javascript
const hasSufficient = await generator.hasSufficientBalance();
console.log(hasSufficient); // true or false
```

**Returns:** `Promise<boolean>` - True if sufficient balance, false otherwise

##### validateWallet()

Validates the wallet configuration and network connection.

```javascript
const validation = await generator.validateWallet();
console.log(validation);
```

**Returns:** `Promise<Object>` - Validation result object

**Validation Result Object:**
```javascript
{
    isValid: boolean,
    errors: string[],
    warnings: string[],
    info: {
        network: string,
        chainId: string,
        walletAddress: string,
        ethBalance: string,
        usdtBalance?: string
    }
}
```

##### simulateFlashGeneration(amount)

Simulates the Flash USDT generation process.

```javascript
const result = await generator.simulateFlashGeneration('300');
console.log(result);
```

**Parameters:**
- `amount` (string, optional): Amount of USDT to flash (default: CONFIG.FLASH_AMOUNT)

**Returns:** `Promise<Object>` - Simulation result

**Simulation Result Object:**
```javascript
{
    success: boolean,
    amount: string,
    timestamp: string,
    steps: string[],
    gasEstimate: Object | null,
    error: string | null
}
```

##### estimateTransactionCost()

Estimates the cost of a transaction.

```javascript
const gasEstimate = await generator.estimateTransactionCost();
console.log(gasEstimate);
```

**Returns:** `Promise<Object>` - Gas estimation details

**Gas Estimation Object:**
```javascript
{
    gasLimit: number,
    gasPrice: string,           // in Gwei
    estimatedCostETH: string,   // in ETH
    estimatedCostWei: string    // in Wei
}
```

##### getContractInfo()

Retrieves detailed information about the USDT contract.

```javascript
const contractInfo = await generator.getContractInfo();
console.log(contractInfo);
```

**Returns:** `Promise<Object>` - Contract information

**Contract Info Object:**
```javascript
{
    address: string,
    name: string,
    symbol: string,
    decimals: string
}
```

##### getNetworkStats()

Retrieves current network statistics.

```javascript
const stats = await generator.getNetworkStats();
console.log(stats);
```

**Returns:** `Promise<Object>` - Network statistics

**Network Stats Object:**
```javascript
{
    currentBlock: number,
    gasPrice: string,           // in Gwei
    maxFeePerGas: string | null,// in Gwei
    networkName: string,
    chainId: string
}
```

##### cleanup()

Cleans up resources and closes connections.

```javascript
generator.cleanup();
```

**Returns:** `void`

## Utility Functions

### validatePrivateKey(privateKey)

Validates Ethereum private key format.

```javascript
const isValid = validatePrivateKey('0x1234567890abcdef...');
console.log(isValid); // true or false
```

**Parameters:**
- `privateKey` (string): Private key to validate

**Returns:** `boolean` - True if valid, false otherwise

### validateInfuraApiKey(apiKey)

Validates Infura API key format.

```javascript
const isValid = validateInfuraApiKey('12345678901234567890123456789012');
console.log(isValid); // true or false
```

**Parameters:**
- `apiKey` (string): API key to validate

**Returns:** `boolean` - True if valid format, false otherwise

### formatUSDTAmount(amount)

Formats amount to USDT units with proper decimal precision.

```javascript
const formatted = formatUSDTAmount(123.456789);
console.log(formatted); // "123.456789"
```

**Parameters:**
- `amount` (string|number): Amount to format

**Returns:** `string` - Formatted amount with up to 6 decimal places

## API Reference

### Module Exports

The main module exports the following:

```javascript
module.exports = {
    FlashUSDTGenerator,      // Main class
    CONFIG,                  // Configuration object
    validatePrivateKey,      // Utility function
    validateInfuraApiKey,    // Utility function
    formatUSDTAmount        // Utility function
};
```

### Import Examples

```javascript
// Import everything
const {
    FlashUSDTGenerator,
    CONFIG,
    validatePrivateKey,
    validateInfuraApiKey,
    formatUSDTAmount
} = require('./flash-usdt.js');

// Import only what you need
const { FlashUSDTGenerator } = require('./flash-usdt.js');
```

## Usage Examples

### Basic Usage

```javascript
const { FlashUSDTGenerator, validatePrivateKey, validateInfuraApiKey } = require('./flash-usdt.js');

async function basicExample() {
    const privateKey = 'your-private-key';
    const infuraApiKey = 'your-infura-api-key';
    
    // Validate credentials
    if (!validatePrivateKey(privateKey)) {
        throw new Error('Invalid private key');
    }
    
    if (!validateInfuraApiKey(infuraApiKey)) {
        throw new Error('Invalid Infura API key');
    }
    
    // Create generator instance
    const generator = new FlashUSDTGenerator(privateKey, infuraApiKey);
    
    // Get wallet address
    console.log('Wallet:', generator.getWalletAddress());
    
    // Check balances
    const ethBalance = await generator.getEthBalance();
    const usdtBalance = await generator.getUsdtBalance();
    
    console.log(`ETH Balance: ${ethBalance}`);
    console.log(`USDT Balance: ${usdtBalance}`);
    
    // Simulate flash generation
    const result = await generator.simulateFlashGeneration('300');
    
    if (result.success) {
        console.log('Flash generation successful!');
    } else {
        console.log('Flash generation failed:', result.error);
    }
    
    // Cleanup
    generator.cleanup();
}

basicExample().catch(console.error);
```

### Advanced Usage with Error Handling

```javascript
async function advancedExample() {
    const privateKey = process.env.PRIVATE_KEY;
    const infuraApiKey = process.env.INFURA_API_KEY;
    
    try {
        const generator = new FlashUSDTGenerator(privateKey, infuraApiKey);
        
        // Validate wallet first
        const validation = await generator.validateWallet();
        
        if (!validation.isValid) {
            throw new Error(`Wallet validation failed: ${validation.errors.join(', ')}`);
        }
        
        // Show warnings if any
        if (validation.warnings.length > 0) {
            console.warn('Warnings:', validation.warnings);
        }
        
        // Check if sufficient balance
        const hasSufficientBalance = await generator.hasSufficientBalance();
        if (!hasSufficientBalance) {
            console.warn('Warning: Insufficient ETH balance for transactions');
        }
        
        // Get network statistics
        const networkStats = await generator.getNetworkStats();
        console.log('Network Stats:', networkStats);
        
        // Get contract information
        const contractInfo = await generator.getContractInfo();
        console.log('USDT Contract:', contractInfo);
        
        // Estimate transaction cost
        const gasEstimate = await generator.estimateTransactionCost();
        console.log('Gas Estimate:', gasEstimate);
        
        // Simulate flash generation with custom amount
        const customAmount = '500';
        const result = await generator.simulateFlashGeneration(customAmount);
        
        console.log('Simulation Result:', result);
        
        generator.cleanup();
        
    } catch (error) {
        console.error('Error:', error.message);
    }
}

advancedExample();
```

### Batch Operations

```javascript
async function batchOperations() {
    const generator = new FlashUSDTGenerator(privateKey, infuraApiKey);
    
    try {
        // Run multiple operations in parallel
        const [
            ethBalance,
            usdtBalance,
            networkStats,
            contractInfo
        ] = await Promise.all([
            generator.getEthBalance(),
            generator.getUsdtBalance(),
            generator.getNetworkStats(),
            generator.getContractInfo()
        ]);
        
        console.log('Batch Results:', {
            ethBalance,
            usdtBalance,
            networkStats,
            contractInfo
        });
        
        // Run multiple simulations with different amounts
        const amounts = ['100', '300', '500'];
        const simulations = await Promise.all(
            amounts.map(amount => generator.simulateFlashGeneration(amount))
        );
        
        simulations.forEach((result, index) => {
            console.log(`Simulation ${amounts[index]}:`, result.success);
        });
        
    } catch (error) {
        console.error('Batch operation failed:', error);
    } finally {
        generator.cleanup();
    }
}

batchOperations();
```

## Error Handling

### Common Error Types

1. **Initialization Errors**
   - Invalid private key format
   - Invalid Infura API key
   - Network connection issues

2. **Network Errors**
   - Failed to connect to Ethereum network
   - RPC endpoint unavailable
   - Rate limiting

3. **Wallet Errors**
   - Insufficient balance
   - Invalid wallet address
   - Private key mismatch

4. **Contract Errors**
   - Contract not found
   - Invalid contract ABI
   - Function call failures

### Error Handling Best Practices

```javascript
async function robustErrorHandling() {
    let generator;
    
    try {
        generator = new FlashUSDTGenerator(privateKey, infuraApiKey);
        
        // Validate first
        const validation = await generator.validateWallet();
        if (!validation.isValid) {
            console.error('Validation errors:', validation.errors);
            return;
        }
        
        // Handle specific operations with try-catch
        let ethBalance;
        try {
            ethBalance = await generator.getEthBalance();
        } catch (error) {
            console.error('Failed to get ETH balance:', error.message);
            ethBalance = '0';
        }
        
        let usdtBalance;
        try {
            usdtBalance = await generator.getUsdtBalance();
        } catch (error) {
            console.error('Failed to get USDT balance:', error.message);
            usdtBalance = '0';
        }
        
        console.log(`Balances - ETH: ${ethBalance}, USDT: ${usdtBalance}`);
        
    } catch (error) {
        console.error('Fatal error:', error.message);
    } finally {
        // Always cleanup
        if (generator) {
            generator.cleanup();
        }
    }
}
```

## Testing

### Running Tests

```bash
# Run all tests
npm test

# Run with verbose output
node test.js
```

### Test Categories

1. **Utility Functions Tests**
   - Private key validation
   - API key validation
   - Amount formatting

2. **Configuration Tests**
   - CONFIG object validation
   - Required properties check

3. **Class Instantiation Tests**
   - Constructor validation
   - Basic method availability

4. **Error Handling Tests**
   - Invalid input handling
   - Network error scenarios

5. **Integration Tests**
   - Module exports verification
   - End-to-end workflows

### Writing Custom Tests

```javascript
const { TestRunner } = require('./test.js');

async function customTest() {
    const testRunner = new TestRunner();
    
    testRunner.addTest('Custom Test', async () => {
        // Your test logic here
        const result = someFunction();
        if (result !== expectedValue) {
            throw new Error('Test failed');
        }
    });
    
    const summary = await testRunner.runAll();
    console.log('Test Results:', summary);
}

customTest();
```

## Advanced Usage

### Using with Different Networks

```javascript
// Mainnet
const mainnetGenerator = new FlashUSDTGenerator(privateKey, infuraApiKey, 'mainnet');

// Testnet (Goerli)
const goerliGenerator = new FlashUSDTGenerator(privateKey, infuraApiKey, 'goerli');

// Sepolia
const sepoliaGenerator = new FlashUSDTGenerator(privateKey, infuraApiKey, 'sepolia');
```

### Custom Configuration

```javascript
// Override default configuration
const customConfig = {
    ...CONFIG,
    FLASH_AMOUNT: '1000',
    GAS_LIMIT: 50000
};

// Use in your application
const result = await generator.simulateFlashGeneration(customConfig.FLASH_AMOUNT);
```

### Monitoring and Logging

```javascript
class MonitoredFlashGenerator extends FlashUSDTGenerator {
    async simulateFlashGeneration(amount) {
        console.log(`Starting simulation for ${amount} USDT`);
        const startTime = Date.now();
        
        const result = await super.simulateFlashGeneration(amount);
        
        const duration = Date.now() - startTime;
        console.log(`Simulation completed in ${duration}ms`);
        
        return result;
    }
}

const monitoredGenerator = new MonitoredFlashGenerator(privateKey, infuraApiKey);
```

### Environment Configuration

```javascript
// Use environment variables for sensitive data
const config = {
    privateKey: process.env.PRIVATE_KEY,
    infuraApiKey: process.env.INFURA_API_KEY,
    network: process.env.NETWORK || 'mainnet'
};

// Validate environment
if (!config.privateKey || !config.infuraApiKey) {
    throw new Error('Missing required environment variables');
}

const generator = new FlashUSDTGenerator(
    config.privateKey,
    config.infuraApiKey,
    config.network
);
```

## Security Considerations

### Best Practices

1. **Never expose private keys in code**
2. **Use environment variables for sensitive data**
3. **Validate all inputs before processing**
4. **Implement proper error handling**
5. **Use HTTPS endpoints only**
6. **Keep dependencies updated**

### Example Secure Setup

```javascript
// .env file
PRIVATE_KEY=your_private_key_here
INFURA_API_KEY=your_infura_api_key_here
NETWORK=mainnet

// Application code
require('dotenv').config();

const privateKey = process.env.PRIVATE_KEY;
const infuraApiKey = process.env.INFURA_API_KEY;

if (!privateKey || !infuraApiKey) {
    console.error('Missing required environment variables');
    process.exit(1);
}

// Validate before use
if (!validatePrivateKey(privateKey)) {
    console.error('Invalid private key format');
    process.exit(1);
}

if (!validateInfuraApiKey(infuraApiKey)) {
    console.error('Invalid Infura API key format');
    process.exit(1);
}
```

---

## Support

For additional support or custom scripts, contact:
- **Telegram**: [@flash_cryptoking1](https://t.me/flash_cryptoking1)

## License

This project is licensed under the MIT License. See the LICENSE file for details.

## Disclaimer

This script is for educational and development use only. It does not perform any illegal or unauthorized operations. Always test on your own wallets and never expose your real private keys.