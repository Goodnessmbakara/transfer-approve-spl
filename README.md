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

## 🔬 **Observations: How Solana Native SDK Works for Token Approval and Transfer Logic**

Based on the understanding of this codebase and the [Neon EVM Solana Native SDK documentation](https://neonevm.org/docs/composability/sdk_solana_native), below are comprehensive observations about how the Solana Native SDK operates for token approval and transfer logic:

### **1. Core Architecture and Cross-Chain Bridge**

#### **Dual-Layer Transaction System**
The Solana Native SDK implements a sophisticated dual-layer transaction system:
- **Solana Layer**: Handles transaction signing and scheduling using Solana wallets
- **Neon EVM Layer**: Executes the actual token operations on Neon EVM

#### **Key Components Identified:**
- **NeonProxyRpcApi**: Manages communication between Solana and Neon EVM
- **Scheduled Transactions**: Enables cross-chain transaction orchestration
- **Balance Account Management**: Handles Neon EVM account initialization on Solana

### **2. Token Approval Logic Analysis**

#### **Approval Flow Implementation:**
```javascript
// 1. Initialize Solana user and get Neon wallet
const {chainId, solanaUser} = await proxyApi.init(keypair);

// 2. Check current approval status
const currentApproval = await USDC.allowance(solanaUser.neonWallet, solanaUser.neonWallet);

// 3. Create approval transaction data
const transactionData = {
    from: solanaUser.neonWallet,
    to: USDC_ADDRESS,
    data: USDC.interface.encodeFunctionData("approve", [spender, amount])
};

// 4. Estimate gas and create scheduled transaction
const transactionGas = await proxyApi.estimateScheduledTransactionGas({
    solanaPayer: solanaUser.publicKey,
    transactions: [transactionData]
});
```

#### **Critical Observations:**
- **Self-Approval Pattern**: The implementation uses `solanaUser.neonWallet` as both owner and spender, enabling self-approval for delegated spending
- **Timestamp-Based Approval**: Uses `Math.floor(Date.now() / 1000)` for approval amount, creating time-based approval windows
- **Cross-Chain Approval State**: Approval state is maintained on Neon EVM while being initiated from Solana

### **3. Token Transfer Logic Analysis**

#### **Transfer Flow Implementation:**
```javascript
// 1. ATA Management and Validation
const solanaUserUSDC_ATA = await getAssociatedTokenAddress(
    new web3.PublicKey(ethers.encodeBase58(usdcTokenMint)),
    solanaUser.publicKey,
    true
);

// 2. Automatic ATA Creation
if (e instanceof TokenAccountNotFoundError) {
    const ataIx = createAssociatedTokenAccountInstruction(
        keypair.publicKey,             // payer
        solanaUserUSDC_ATA,            // associated token address
        keypair.publicKey,             // owner
        new web3.PublicKey(ethers.encodeBase58(usdcTokenMint)) // USDC mint
    );
}

// 3. Delegation Check and Approval
if (ataInfo.delegate == null || ataInfo.delegate.toBase58() != usdcContractPDA.toBase58()) {
    scheduledTransaction.instructions.unshift(
        createApproveInstruction(
            solanaUserUSDC_ATA,
            usdcContractPDA, // delegate to contract PDA
            solanaUser.publicKey,
            '18446744073709551615' // max uint64 approval
        )
    );
}
```

#### **Critical Observations:**
- **PDA-Based Delegation**: The USDC contract PDA (`usdcContractPDA`) acts as the delegate for spending from Solana ATAs
- **Automatic ATA Management**: The SDK automatically creates missing Associated Token Accounts
- **Max Approval Strategy**: Uses maximum uint64 approval (`18446744073709551615`) for delegation, enabling unlimited spending

### **4. Scheduled Transaction Mechanism**

#### **Transaction Lifecycle:**
1. **Initialization**: Solana wallet connects and Neon EVM account is derived
2. **Gas Estimation**: Cross-chain gas estimation for Neon EVM operations
3. **Transaction Creation**: Scheduled transaction with Solana instructions
4. **Balance Account Setup**: Automatic creation of Neon EVM balance accounts
5. **Transaction Signing**: Solana wallet signs the scheduled transaction
6. **Execution**: Transaction executes on Neon EVM with Solana confirmation

#### **Key Technical Insights:**
- **Nonce Management**: Each transaction uses a unique nonce derived from the Neon wallet
- **Instruction Batching**: Multiple Solana instructions can be batched in a single scheduled transaction
- **Cross-Chain State Synchronization**: Balance and approval states are synchronized between Solana and Neon EVM

### **5. Composability and Modular Design**

#### **Library Architecture:**
The project implements a modular composability system:
- **LibSPLTokenProgram**: Handles core SPL token operations (transfer, mint, approve)
- **LibAssociatedTokenProgram**: Manages ATA creation and management
- **LibSystemProgram**: Handles Solana system operations
- **CallSolanaHelperLib**: Provides utility functions for Solana instruction formatting

#### **Instruction Formatting:**
```solidity
// Example: Transfer instruction formatting
function formatTransferInstruction(
    bytes32 senderATA,
    bytes32 recipientATA,
    bytes32 sender,
    uint64 amount
) internal pure returns (
    bytes32[] memory accounts,
    bool[] memory isSigner,
    bool[] memory isWritable,
    bytes memory data
) {
    // Instruction variant 0x03 for transfer
    data = abi.encodePacked(
        bytes1(0x03),
        bytes8(amountLE) // Little-endian amount
    );
}
```

### **6. Security and Error Handling**

#### **Security Mechanisms:**
- **Authentication**: Solana keypair authentication for transaction signing
- **Authorization**: PDA-based delegation for token spending
- **Validation**: Balance and account existence checks before operations
- **Error Recovery**: Graceful handling of missing accounts and failed operations

#### **Error Handling Patterns:**
- **TokenAccountNotFoundError**: Automatic ATA creation when missing
- **Balance Validation**: Checks for sufficient SOL and token balances
- **Delegation Validation**: Ensures proper delegation before transfers

### **7. Performance and Optimization**

#### **Gas Optimization:**
- **Batch Instructions**: Multiple operations in single scheduled transaction
- **Efficient Gas Estimation**: Cross-chain gas estimation for cost optimization
- **Minimal Cross-Chain Calls**: Reduced communication overhead

#### **State Management:**
- **Cached Account Info**: Reuse of account information across operations
- **Optimistic Updates**: Immediate state updates with rollback capabilities
- **Efficient Balance Tracking**: Real-time balance synchronization

### **8. Integration Patterns**

#### **ERC20ForSPL Integration:**
- **Dual Interface**: Supports both ERC20 and SPL token interfaces
- **Cross-Chain Compatibility**: Seamless interaction between Ethereum and Solana ecosystems
- **Event Emission**: Proper event emission for both ERC20 and SPL operations

#### **Wallet Integration:**
- **Solana Wallet Support**: Native Solana wallet integration (Phantom, etc.)
- **Keypair Management**: Secure keypair handling with bs58 encoding
- **Transaction Signing**: Native Solana transaction signing with Neon EVM execution

### **9. Development and Testing Insights**

#### **Development Workflow:**
- **Environment Setup**: Proper configuration of both Solana and Neon EVM environments
- **Dependency Management**: Careful version management of cross-chain dependencies
- **Testing Strategy**: Comprehensive testing of both approval and transfer flows

#### **Debugging and Monitoring:**
- **Transaction Tracking**: Both Solana and Neon EVM transaction monitoring
- **Balance Verification**: Cross-chain balance verification
- **Error Diagnostics**: Detailed error reporting and debugging information

## 📄 License
MIT License

## 🔗 Resources
- [Neon EVM Documentation](https://docs.neonfoundation.io/)
- [Solana Documentation](https://docs.solana.com/)
- [SPL Token Program](https://spl.solana.com/token)
- [ERC20ForSPL Documentation](https://docs.neonfoundation.io/docs/developing/contracts/erc20forspl)
- [Neon EVM Solana Native SDK](https://neonevm.org/docs/composability/sdk_solana_native)

## 🤝 Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Support
For support and questions, please open an issue on GitHub or contact the development team.
