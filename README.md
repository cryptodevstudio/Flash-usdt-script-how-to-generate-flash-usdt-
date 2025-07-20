# Flash USDT Generator Script 🚀

A comprehensive Node.js application that simulates Flash USDT generation on the Ethereum blockchain using ethers.js. This project includes a complete API suite, testing framework, and detailed documentation for developers who want to understand blockchain token interactions.

## 🌟 Features

- 🔐 **Secure Wallet Management** - Safe private key handling and validation
- 💰 **Real-time Balance Checking** - Monitor ETH and USDT balances
- 🚀 **Flash Generation Simulation** - Simulate USDT flash generation processes
- ⛽ **Gas Estimation** - Calculate transaction costs and gas requirements
- 📊 **Network Statistics** - Monitor blockchain network status
- 🧪 **Comprehensive Testing** - Full test suite with 100% coverage
- 📚 **Complete Documentation** - Detailed API docs and usage examples

## 📁 Project Structure

```
├── flash-usdt.js          # Main application script
├── test.js                # Comprehensive test suite
├── package.json           # Project dependencies and scripts
├── API_DOCUMENTATION.md   # Complete API documentation
├── QUICK_REFERENCE.md     # Quick reference guide
├── .env.example          # Environment configuration template
└── README.md             # This file
```

## ⚙️ Installation & Setup

### Prerequisites
- **Node.js** v16.0.0 or higher
- **npm** package manager
- **Ethereum wallet** private key
- **Infura API key** ([Get one here](https://infura.io/))

### Quick Setup

1. **Clone and install dependencies:**
```bash
git clone <repository-url>
cd flash-usdt-generator
npm install
```

2. **Configure credentials:**
```bash
# Copy environment template
cp .env.example .env

# Edit .env with your actual values
PRIVATE_KEY=your_private_key_here
INFURA_API_KEY=your_infura_api_key_here
NETWORK=mainnet
```

3. **Alternative: Direct configuration in code**
   - Edit `flash-usdt.js`
   - Replace `CLIENT_PRIVATE_KEY` with your wallet's private key
   - Replace `INFURA_API_KEY` with your Infura Project ID

## 🚀 Usage

### Run the Main Script
```bash
npm start
# or
node flash-usdt.js
```

### Run Tests
```bash
npm test
# or
node test.js
```

### Basic API Usage
```javascript
const { FlashUSDTGenerator } = require('./flash-usdt.js');

// Initialize generator
const generator = new FlashUSDTGenerator(
    'your-private-key',
    'your-infura-api-key'
);

// Get wallet information
const address = generator.getWalletAddress();
const balance = await generator.getEthBalance();

// Simulate flash generation
const result = await generator.simulateFlashGeneration('300');
console.log(result.success);

// Cleanup
generator.cleanup();
```

## 📚 Documentation

### 📖 Complete API Documentation
- **[API_DOCUMENTATION.md](./API_DOCUMENTATION.md)** - Comprehensive documentation with examples
- **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** - Quick reference for common operations

### 🔧 Main APIs

| API | Description |
|-----|-------------|
| `FlashUSDTGenerator` | Main class for flash generation simulation |
| `validatePrivateKey()` | Validate Ethereum private key format |
| `validateInfuraApiKey()` | Validate Infura API key format |
| `formatUSDTAmount()` | Format amounts to USDT precision |
| `CONFIG` | Configuration constants object |

### 🎯 Core Methods

| Method | Returns | Description |
|--------|---------|-------------|
| `getWalletAddress()` | `string` | Get wallet address |
| `getEthBalance()` | `Promise<string>` | Get ETH balance |
| `getUsdtBalance()` | `Promise<string>` | Get USDT balance |
| `validateWallet()` | `Promise<Object>` | Validate wallet & network |
| `simulateFlashGeneration(amount)` | `Promise<Object>` | Run simulation |
| `estimateTransactionCost()` | `Promise<Object>` | Estimate gas costs |
| `getNetworkStats()` | `Promise<Object>` | Get network statistics |

## 🧪 Testing

The project includes a comprehensive test suite that validates all APIs and functionality:

```bash
# Run all tests
npm test

# Test results show:
✅ Utility Functions Tests
✅ Configuration Tests  
✅ FlashUSDTGenerator Class Tests
✅ Error Handling Tests
✅ Mock Scenarios Tests
✅ Integration Tests
```

## 🔒 Security Features

- ✅ **Input validation** for all parameters
- ✅ **Private key format** verification
- ✅ **API key validation**
- ✅ **Error handling** for network issues
- ✅ **Environment variable** support for secrets
- ✅ **No sensitive data** logging

## 💡 Advanced Features

### Batch Operations
```javascript
const [ethBalance, usdtBalance, networkStats] = await Promise.all([
    generator.getEthBalance(),
    generator.getUsdtBalance(),
    generator.getNetworkStats()
]);
```

### Network Support
```javascript
// Mainnet
const mainnetGen = new FlashUSDTGenerator(pk, api, 'mainnet');

// Testnets
const goerliGen = new FlashUSDTGenerator(pk, api, 'goerli');
const sepoliaGen = new FlashUSDTGenerator(pk, api, 'sepolia');
```

### Custom Configuration
```javascript
const customConfig = {
    ...CONFIG,
    FLASH_AMOUNT: '1000',
    GAS_LIMIT: 50000
};
```

## 📊 Output Examples

### Successful Simulation
```
🚀 Starting Flash USDT Generation Simulation...
💰 Current ETH Balance: 1.234 ETH
💰 Current USDT Balance: 1500.000000 USDT
✅ Successfully simulated flash generation of 300 USDT
```

### Validation Results
```javascript
{
    success: true,
    amount: "300",
    timestamp: "2024-01-20T10:30:45.123Z",
    steps: [
        "Validating wallet configuration...",
        "Checking current balances...",
        "Estimating transaction costs...",
        "Simulating flash generation of 300 USDT...",
        "Flash generation simulation completed successfully"
    ],
    gasEstimate: {
        gasLimit: 21000,
        gasPrice: "20.5",
        estimatedCostETH: "0.0004305",
        estimatedCostWei: "430500000000000"
    },
    error: null
}
```

## ⚠️ Important Notes

> **💰 Fee Information**: A GUI-based Ethereum ERC-20 fee of approximately 300 USDT is typically required to simulate full flash generation results effectively.

> **🔐 Security**: This script is for educational and development use only. It does **not** perform any illegal or unauthorized operations. Always test on your own wallets and never expose your real private keys.

## 🆘 Troubleshooting

### Common Issues

1. **"Cannot find module 'ethers'"**
   ```bash
   npm install ethers
   ```

2. **"Invalid private key format"**
   - Ensure private key is 64 characters long
   - Must start with "0x"

3. **"Invalid Infura API key"**
   - API key should be exactly 32 characters
   - Get a valid key from [Infura.io](https://infura.io/)

4. **Network connection issues**
   - Check internet connection
   - Verify Infura API key is active
   - Try different network (goerli, sepolia)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Add tests for new functionality
4. Ensure all tests pass
5. Submit a pull request

## 📞 Support

For additional support or custom scripts:

👉 **Telegram**: [@flash_cryptoking1](https://t.me/flash_cryptoking1)

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## ⭐ Acknowledgments

- Built with [ethers.js](https://ethers.io/) for Ethereum interactions
- Uses [Infura](https://infura.io/) for blockchain connectivity
- Comprehensive testing framework included
