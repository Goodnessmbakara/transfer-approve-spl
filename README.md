# 🚀 SPL Token Transfer & Approval on Neon EVM

## 📝 Overview
This project demonstrates the implementation of SPL token transfer and approval functionality on Neon EVM Devnet, showcasing seamless cross-chain interactions between Ethereum and Solana ecosystems. The project enables users to approve and transfer SPL tokens (like USDC) using Solidity smart contracts on Neon EVM while leveraging Solana's native token infrastructure.

## 🛠️ Technical Implementation

### Architecture
- **Neon EVM**: Enables Solidity smart contracts to interact with Solana programs
- **Cross-Chain Integration**: Bridges Ethereum and Solana ecosystems
- **SPL Token Integration**: Native Solana token support through ERC20ForSPL contracts
- **Composability Libraries**: Modular design for different Solana program interactions

### Key Components
1. **Token Transfer SDK**: Handles SPL token transfers across chains
2. **Token Approval SDK**: Manages token approvals for delegated spending
3. **Composability Libraries**: Modular libraries for different Solana programs
4. **ERC20ForSPL Contracts**: Solidity wrappers for SPL tokens
5. **Utility Libraries**: Helper functions for data conversion and validation

## 🚀 Setup and Deployment

### Prerequisites
- Node.js and npm
- Neon Devnet wallet
- Solana Devnet wallet
- USDC tokens on Neon EVM

### Installation
```bash
# Clone the repository
git clone https://github.com/Goodnessmbakara/transfer-approve-spl.git
cd transfer-approve-spl

# Install dependencies
npm install

# Install additional dependencies for bigint support
npm install --save-dev @types/node
```

### Configuration
1. Create `.env` file:
```env
NEON_RPC_URL=https://devnet.neonevm.org
PRIVATE_KEY=your_neon_wallet_private_key
SOLANA_RPC_URL=https://api.devnet.solana.com
PRIVATE_KEY_SOLANA=your_solana_wallet_private_key
```

2. Update `hardhat.config.js`:
```javascript
module.exports = {
  solidity: {
    version: "0.8.20",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200
      },
      viaIR: true
    }
  },
  networks: {
    neondevnet: {
      url: process.env.NEON_RPC_URL,
      accounts: [process.env.PRIVATE_KEY],
      chainId: 245022926,
      allowUnlimitedContractSize: true,
      timeout: 1000000
    }
  }
};
```

## 🔗 Contract Addresses and Transactions

### Deployed Contracts
- **USDC Token**: `0x512E48836Cd42F3eB6f50CEd9ffD81E0a7F15103` [View on Neonscan](https://devnet.neonscan.org/address/0x512E48836Cd42F3eB6f50CEd9ffD81E0a7F15103)

### Key Transactions

#### Token Approval
- **Transaction Hash**: `0xbad6e1bff8f64b8c71f94c8c281df818033fb6e10cfd6cb53dd03ac4f61b4b64` [View on Neonscan](https://devnet.neonscan.org/tx/0xbad6e1bff8f64b8c71f94c8c281df818033fb6e10cfd6cb53dd03ac4f61b4b64)
- **Scheduled Transaction**: `44FH6ApBHrBTt152CSVyaEKJMWNtPh8BxXB6v8qwRxJkH6gNAL6pi6gyF2s5LvvyvoTeaBs3YSfTBnQRZ7LjnwsG`
- **Approval Amount**: 1,750,690,426 (1750690426n)
- **Gas Estimation**: Successful with proper fee calculation

#### Token Transfer
- **Transaction Hash**: `0x557c4b840d291f96aafcfa09c3f22ebb80c36abd895c40d49c22fbf4c530b583` [View on Neonscan](https://devnet.neonscan.org/tx/0x557c4b840d291f96aafcfa09c3f22ebb80c36abd895c40d49c22fbf4c530b583)
- **Scheduled Transaction**: `48wWGduzcEEiGt7Jjm4DcpUP8TXVzvqi43bYoUuyW8T6hdMoNpzdWpkzv3cWrrSbqaLodQoX9TRkPygpQcj1P7Kt`
- **Transfer Amount**: 1,000,000 USDC
- **Gas Estimation**: Successful execution

## 🧪 Testing and Execution Results

### Token Approval Test
```bash
node token-approval-solana-signer-sdk.js
```

**Results:**
- ✅ Initial USDC approval: 0n
- ✅ Gas estimation successful
- ✅ Scheduled transaction created: `44FH6ApBHrBTt152CSVyaEKJMWNtPh8BxXB6v8qwRxJkH6gNAL6pi6gyF2s5LvvyvoTeaBs3YSfTBnQRZ7LjnwsG`
- ✅ Neon EVM transaction hash: `0xbad6e1bff8f64b8c71f94c8c281df818033fb6e10cfd6cb53dd03ac4f61b4b64`
- ✅ Final USDC approval: 1,750,690,426n

### Token Transfer Test
```bash
node token-transfer-solana-signer-sdk.js
```

**Results:**
- ✅ Sender USDC balance before: 7,000,000n
- ✅ Receiver USDC balance before: 0n
- ✅ ATA creation successful: `5aefPmrDsreDRWu48ie2fg5pH1MZwqNH4bjjWFJGPyYZJnS9wNYvM6ZYVH4gEx4f4CouJLC3KygLhMxVCMdc7jcH`
- ✅ Gas estimation successful
- ✅ Scheduled transaction created: `48wWGduzcEEiGt7Jjm4DcpUP8TXVzvqi43bYoUuyW8T6hdMoNpzdWpkzv3cWrrSbqaLodQoX9TRkPygpQcj1P7Kt`
- ✅ Neon EVM transaction hash: `0x557c4b840d291f96aafcfa09c3f22ebb80c36abd895c40d49c22fbf4c530b583`
- ✅ Sender USDC balance after: 6,000,000n
- ✅ Receiver USDC balance after: 1,000,000n

## 🔍 Technical Details

### Gas Estimation and Network Parameters
- **Chain ID**: `0xe9ac0cf` (245022926)
- **Max Fee Per Gas**: `0x5de097c1`
- **Max Priority Fee Per Gas**: `0x5de097c0`
- **Gas Estimation**: Successfully handled for both approval and transfer operations

### Cross-Chain Integration Features
- **Solana ATA Management**: Automatic creation of Associated Token Accounts
- **Balance Tracking**: Real-time balance monitoring across chains
- **Transaction Scheduling**: Proper scheduling of cross-chain transactions
- **Error Handling**: Graceful handling of execution reverts

### Composability Libraries
The project includes comprehensive libraries for different Solana program interactions:

#### SPL Token Program
- `LibSPLTokenProgram.sol`: Core SPL token operations
- `LibSPLTokenData.sol`: Data structures for SPL tokens
- `LibSPLTokenErrors.sol`: Error handling for SPL operations

#### Associated Token Program
- `LibAssociatedTokenProgram.sol`: ATA management
- `LibAssociatedTokenData.sol`: ATA data structures

#### Raydium Program
- `LibRaydiumProgram.sol`: Raydium DEX integration
- `LibRaydiumData.sol`: Raydium data structures
- `LibRaydiumErrors.sol`: Raydium error handling

#### System Program
- `LibSystemProgram.sol`: Solana system operations
- `LibSystemData.sol`: System program data structures
- `LibSystemErrors.sol`: System program error handling

## 🎯 Key Features Demonstrated

### 1. Cross-Chain Token Operations
- Seamless transfer of SPL tokens between Neon EVM and Solana
- Proper approval mechanisms for delegated spending
- Real-time balance synchronization

### 2. Gas Optimization
- Efficient gas estimation for cross-chain operations
- Proper fee calculation and priority fee handling
- Optimized transaction scheduling

### 3. Error Handling
- Graceful handling of execution reverts
- Proper error codes and messages
- Fallback mechanisms for failed operations

### 4. ATA Management
- Automatic creation of Associated Token Accounts
- Proper account initialization for token operations
- Balance tracking across different account types

## 🔐 Security Considerations
- Implemented proper approval mechanisms
- Added balance validation before transfers
- Used safe token transfer patterns
- Implemented proper error handling and revert mechanisms

## 📚 Project Structure
```
transfer-approve-spl/
├── composability/           # Cross-chain composability libraries
│   ├── CallSPLTokenProgram.sol
│   ├── CallAssociatedTokenProgram.sol
│   ├── CallRaydiumProgram.sol
│   ├── CallSystemProgram.sol
│   └── libraries/          # Modular program libraries
├── token/                  # ERC20ForSPL token contracts
│   └── ERC20ForSpl/
├── precompiles/           # Neon EVM precompile interfaces
├── oracles/              # Oracle integrations (Pyth, VRF)
├── utils/                # Utility libraries
├── mocks/                # Mock contracts for testing
├── token-approval-solana-signer-sdk.js
├── token-transfer-solana-signer-sdk.js
└── hardhat.config.js
```

## 🚀 Usage Examples

### Token Approval
```javascript
// Approve tokens for spending
const approvalAmount = ethers.parseUnits("1000000", 6); // 1M USDC
await usdcToken.approve(spenderAddress, approvalAmount);
```

### Token Transfer
```javascript
// Transfer tokens to another address
const transferAmount = ethers.parseUnits("1000000", 6); // 1M USDC
await usdcToken.transfer(receiverAddress, transferAmount);
```

## 📄 License
MIT License

## 🔗 Resources
- [Neon EVM Documentation](https://docs.neonfoundation.io/)
- [Solana Documentation](https://docs.solana.com/)
- [SPL Token Program](https://spl.solana.com/token)
- [ERC20ForSPL Documentation](https://docs.neonfoundation.io/docs/developing/contracts/erc20forspl)

## 🤝 Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Support
For support and questions, please open an issue on GitHub or contact the development team.
