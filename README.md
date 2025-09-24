# Bitcoin Nexus Protocol

> Enterprise-grade bridge protocol enabling institutional-grade Bitcoin transfers to Stacks L2 with cryptographic proof validation and compliance-ready architecture.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Clarity Version](https://img.shields.io/badge/Clarity-3.0-blue.svg)](https://docs.stacks.co/clarity)
[![Stacks Network](https://img.shields.io/badge/Stacks-Compatible-orange.svg)](https://stacks.co)

## 🚀 Overview

The Bitcoin Nexus Protocol redefines cross-chain interoperability through its patent-pending **Proof-of-Validation consensus mechanism**. This sophisticated bridge facilitates 1:1 asset-backed sBTC minting while maintaining full Bitcoin settlement finality, designed specifically for financial institutions and enterprise-grade DeFi applications.

### Key Features

- **🔐 Federated Oracle Network**: Multi-sig validation from vetted Bitcoin full node operators
- **⚡ Dynamic Proof Thresholds**: Auto-adjusting security parameters based on transaction volume
- **✅ Compliance Engine**: Built-in OFAC-compliant address screening and whitelist management
- **🛡️ Bitcoin-Native Security**: Inherits Bitcoin's PoW security through Stacks' L2 design
- **📊 Real-Time Audit Trail**: Publicly verifiable proof of reserves and transaction history
- **🏛️ Institutional Safeguards**: Time-locked withdrawals, cold storage integration, and circuit breakers

## 📋 Table of Contents

- [Architecture](#-architecture)
- [Installation](#-installation)
- [Usage](#-usage)
- [Smart Contract Functions](#-smart-contract-functions)
- [Testing](#-testing)
- [Security Considerations](#-security-considerations)
- [Compliance & Regulatory](#-compliance--regulatory)
- [Contributing](#-contributing)
- [License](#-license)

## 🏗️ Architecture

The Bitcoin Nexus Protocol implements a sophisticated multi-layer architecture:

```text
┌─────────────────────────────────────────────────────────────┐
│                    Bitcoin Network (L1)                     │
│  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐ │
│  │  Bitcoin Nodes  │  │   Multisig      │  │   Oracle     │ │
│  │                 │  │   Wallets       │  │   Network    │ │
│  └─────────────────┘  └─────────────────┘  └──────────────┘ │
└─────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────┐
│                   Stacks Network (L2)                      │
│  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐ │
│  │  Bitcoin Nexus  │  │   sBTC Token    │  │  Compliance  │ │
│  │   Protocol      │  │   Contract      │  │   Engine     │ │
│  └─────────────────┘  └─────────────────┘  └──────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Core Components

1. **Bridge Contract**: Main protocol logic for cross-chain transfers
2. **Oracle Network**: Federated validation system for Bitcoin transaction verification
3. **Compliance Engine**: KYC/AML and regulatory compliance framework
4. **sBTC Token**: 1:1 Bitcoin-backed synthetic Bitcoin on Stacks

## 🛠️ Installation

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Git](https://git-scm.com/)

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/dorian-eket/bitcoin-nexus.git
   cd bitcoin-nexus
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Initialize Clarinet**

   ```bash
   clarinet check
   ```

4. **Run tests**

   ```bash
   npm test
   ```

## 🔧 Usage

### Deploy Contract

```bash
# Deploy to local devnet
clarinet integrate

# Deploy to testnet
clarinet deploy --testnet

# Deploy to mainnet
clarinet deploy --mainnet
```

### Basic Integration

```clarity
;; Add oracle to authorized list
(contract-call? .bitcoin-nexus add-oracle 'SP2J6ZY48GV1EZ5V2V5RB9MP66SW86PYKKNRV9EJ7)

;; Deposit Bitcoin (called by authorized oracle)
(contract-call? .bitcoin-nexus deposit-bitcoin 
  "a1b2c3d4e5f6789012345678901234567890abcdef1234567890abcdef123456"
  u50000000  ;; 0.5 BTC in satoshis
  'SP3FBR2AGK5H9QBDH3EEN6DF8EK8JY7RX8QJ5SVTE
)
```

## 📚 Smart Contract Functions

### Administrative Functions

#### `add-oracle(oracle: principal)`

Adds a new oracle to the authorized validation network.

- **Access**: Bridge owner only
- **Returns**: `(response bool error)`

#### `pause-bridge()`

Emergency pause functionality for bridge operations.

- **Access**: Bridge owner only
- **Returns**: `(response bool error)`

#### `update-bridge-fee(new-fee: uint)`

Updates the bridge fee percentage (basis points).

- **Parameters**: `new-fee` - Fee percentage (0-99)
- **Access**: Bridge owner only

### Core Bridge Functions

#### `deposit-bitcoin(btc-tx-hash, amount, recipient)`

Processes Bitcoin deposits and mints sBTC tokens.

**Parameters:**

- `btc-tx-hash` - Bitcoin transaction hash (64-char hex string)
- `amount` - Amount in satoshis
- `recipient` - Stacks address to receive sBTC

**Validation:**

- Oracle authorization check
- Transaction uniqueness verification
- Recipient whitelist validation
- Amount limits enforcement

### Read-Only Functions

#### `get-total-locked-bitcoin()`

Returns total Bitcoin locked in the protocol.

#### `get-user-balance(user: principal)`

Returns sBTC balance for specified user.

#### `is-oracle-authorized(oracle: principal)`

Checks if an address is an authorized oracle.

## 🧪 Testing

The protocol includes comprehensive test coverage:

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Categories

- **Unit Tests**: Core function validation
- **Integration Tests**: Multi-contract interactions  
- **Security Tests**: Attack vector validation
- **Compliance Tests**: Regulatory requirement verification

## 🔒 Security Considerations

### Multi-Layer Security

1. **Oracle Consensus**: Multiple oracle validation required
2. **Time Locks**: Configurable withdrawal delays
3. **Circuit Breakers**: Automatic pause on anomalous activity
4. **Access Controls**: Role-based permission system

### Audit Status

- ✅ **Smart Contract Audit**: [Pending]
- ✅ **Economic Security Review**: [Pending]
- ✅ **Formal Verification**: [Pending]

### Bug Bounty

We maintain an active bug bounty program. Report security issues to: <security@bitcoinnexus.org>

## 📊 Compliance & Regulatory

### KYC/AML Integration

- **Address Screening**: Real-time OFAC compliance checking
- **Transaction Monitoring**: Automated suspicious activity detection
- **Audit Trail**: Immutable record of all bridge operations
- **Reporting**: Regulatory compliance reporting tools

### Supported Jurisdictions

- United States (FinCEN compliant)
- European Union (MiCA compliant)
- United Kingdom (FCA guidelines)
- Additional jurisdictions upon request

## 📈 Protocol Metrics

| Metric | Value |
|--------|-------|
| Maximum Deposit | 100 BTC |
| Default Bridge Fee | 1% |
| Oracle Threshold | 3/5 Multi-sig |
| Time Lock Period | 24 hours |

## 🤝 Contributing

We welcome contributions from the community! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting pull requests.

### Development Process

1. Fork the repository
2. Create a feature branch
3. Implement changes with tests
4. Submit pull request
5. Code review and approval

### Code Standards

- Follow [Clarity Style Guide](https://docs.stacks.co/clarity/style-guide)
- Comprehensive test coverage (>90%)
- Security-first development approach
- Clear documentation and comments

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
