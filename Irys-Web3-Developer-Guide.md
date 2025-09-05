# Irys Web3 Developer Guide

## Table of Contents
- [What is Irys?](#what-is-irys)
- [Core Architecture](#core-architecture)
- [Technical Features](#technical-features)
- [Supported Blockchains](#supported-blockchains)
- [Quick Start](#quick-start)
- [Node.js Integration](#nodejs-integration)
- [React Frontend Integration](#react-frontend-integration)
- [Smart Contracts & Programmable Data](#smart-contracts--programmable-data)
- [Real-world Use Cases](#real-world-use-cases)
- [Best Practices](#best-practices)

---

## What is Irys?

Irys is the world's first **Programmable Datachain**, a decentralized storage solution designed specifically for Web3 developers.

### Core Value Propositions

- 🔗 **Datachain**: As an L1 blockchain with native incentivized data storage
- ⚡ **Programmability**: Smart contracts can directly access, manipulate, and write to the storage layer
- 🛡️ **Permanent Storage**: Pay-once, store-forever with immutable data
- ⚙️ **Multi-chain Support**: Supports 20+ blockchain networks for payments (ETH, MATIC, SOL, AVAX, etc.)
- 📊 **Precise Timestamps**: Millisecond-accurate timestamps and cryptographic receipts
- 🔄 **Mutable References**: Achieve "mutable" data through chain references

### Comparison with Traditional Storage Solutions

| Feature | Irys | IPFS | AWS S3 | Arweave |
|---------|------|------|--------|---------|
| Permanent Storage | ✅ | ❌ | ❌ | ✅ |
| Programmability | ✅ | ❌ | ❌ | ❌ |
| Multi-chain Payment | ✅ | ❌ | ❌ | ❌ |
| Millisecond Timestamps | ✅ | ❌ | ❌ | ❌ |
| Smart Contract Access | ✅ | ❌ | ❌ | ❌ |

---

## Core Architecture

```
╔═══════════════════════════════════════════════════════════════╗
║                           User Layer                           ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────┐ ║
║  │    dApp     │  │    CLI      │  │    SDK      │  │Browser│ ║
║  │  Frontend   │  │   Tools     │  │ Integration │  │Wallet │ ║
║  └─────────────┘  └─────────────┘  └─────────────┘  └───────┘ ║
╠═══════════════════════════════════════════════════════════════╣
║                        Application Layer                      ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐            ║
║  │     NFT     │  │   Social    │  │   Gaming    │            ║
║  │ Marketplace │  │  Protocol   │  │   Assets    │            ║
║  └─────────────┘  └─────────────┘  └─────────────┘            ║
╠═══════════════════════════════════════════════════════════════╣
║                       Irys Protocol Layer                     ║
║  ┌─────────────────────────────────────────────────────────┐   ║
║  │                   Bundler Network                      │   ║
║  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  │   ║
║  │  │ Bundler │  │ Bundler │  │ Bundler │  │ Bundler │  │   ║
║  │  │   #1    │  │   #2    │  │   #3    │  │   #4    │  │   ║
║  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘  │   ║
║  └─────────────────────────────────────────────────────────┘   ║
║                                                               ║
║  ┌─────────────────────────────────────────────────────────┐   ║
║  │               IrysVM (Smart Contract Execution)        │   ║
║  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐    │   ║
║  │  │ Programmable│  │  Timestamp  │  │   Receipt   │    │   ║
║  │  │Data Access  │  │   System    │  │   System    │    │   ║
║  │  └─────────────┘  └─────────────┘  └─────────────┘    │   ║
║  └─────────────────────────────────────────────────────────┘   ║
╠═══════════════════════════════════════════════════════════════╣
║                         Storage Layer                         ║
║  ┌─────────────────────────────────────────────────────────┐   ║
║  │                Permanent Data Storage                  │   ║
║  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  │   ║
║  │  │  Data   │  │Metadata │  │   Tag   │  │  Index  │  │   ║
║  │  │ Shards  │  │        │  │ System  │  │ System  │  │   ║
║  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘  │   ║
║  └─────────────────────────────────────────────────────────┘   ║
╠═══════════════════════════════════════════════════════════════╣
║                    Blockchain Payment Layer                   ║
║  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐  ║
║  │   ETH   │ │ Polygon │ │ Solana  │ │Arbitrum │ │Avalanche│  ║
║  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘  ║
║  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐  ║
║  │   BSC   │ │  Near   │ │  Aptos  │ │  Base   │ │  IoTeX  │  ║
║  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘  ║
╚═══════════════════════════════════════════════════════════════╝

Data Flow:
User → SDK/CLI → Bundler → IrysVM → Permanent Storage ← Blockchain Payment
     ↓
Smart Contract ← Programmable Data Access ← Storage Layer Query
```

### Architecture Overview

1. **User Layer**: Developers interact with Irys through SDKs, CLI, or browser interfaces
2. **Application Layer**: Various Web3 application scenarios like NFT, DeFi, social protocols
3. **Irys Protocol Layer**:
   - **Bundler Network**: Responsible for data aggregation, verification, and upload
   - **IrysVM**: EVM-based virtual machine supporting smart contract execution
4. **Storage Layer**: Permanent data storage with tag indexing and GraphQL query support
5. **Blockchain Payment Layer**: Multi-chain token payment support for storage fees

---

## Technical Features

### 1. Permanent Storage (Pay-once, Store-forever)

```typescript
// Pay once, store forever
const receipt = await irysUploader.upload("Hello Irys!");
console.log(`Permanent storage URL: https://gateway.irys.xyz/${receipt.id}`);
```

### 2. Mutable Reference System

While data itself is immutable, "mutable" effects can be achieved through chain references:

```typescript
// Base transaction
const baseReceipt = await irysUploader.upload("Version 1.0");

// Update version (reference original transaction)
const tags = [{ name: "Root-TX", value: baseReceipt.id }];
const updateReceipt = await irysUploader.upload("Version 2.0", { tags });

// Access mutable URL, always returns latest version
// https://gateway.irys.xyz/mutable/${baseReceipt.id}
```

### 3. Tag System

```typescript
const tags = [
  { name: "Content-Type", value: "application/json" },
  { name: "App-Name", value: "MyDApp" },
  { name: "Version", value: "1.0.0" },
  { name: "Author", value: "0x..." }
];

const receipt = await irysUploader.upload(data, { tags });
```

### 4. On-chain Folders

```typescript
// Upload entire folder
const manifest = await irysUploader.uploadFolder("./assets/", {
  indexFile: "index.html", // Default file
  batchSize: 50
});

// Access specific file in folder
// https://gateway.irys.xyz/${manifest.id}/logo.png
```

### 5. Cryptographic Receipts and Timestamps

```typescript
const receipt = await irysUploader.upload(data);
/*
Receipt contains:
{
  id: "Transaction ID",
  timestamp: 1676891681110, // Millisecond precision
  version: "1.0.0",
  signature: "Cryptographic signature",
  public: "Public key",
  ...
}
*/
```

---

## Supported Blockchains

### Mainnet Supported Tokens

| Blockchain | Token | Parameter Value | Node.js | Browser |
|------------|-------|-----------------|---------|---------|
| Ethereum | ETH | `ethereum` | ✅ | ✅ |
| Polygon | MATIC | `matic` | ✅ | ✅ |
| Solana | SOL | `solana` | ✅ | ✅ |
| Arbitrum | ETH | `arbitrum` | ✅ | ✅ |
| Avalanche | AVAX | `avalanche` | ✅ | ✅ |
| BSC | BNB | `bnb` | ✅ | ✅ |
| Base | ETH | `base-eth` | ✅ | ✅ |
| Near | NEAR | `near` | ✅ | ✅ |
| Aptos | APT | `aptos` | ✅ | ✅ |
| USDC | USDC | `usdc-eth` | ✅ | ✅ |

### Network Selection

- **Mainnet**: Real token payments, permanent data storage
- **Devnet**: Test tokens, data deleted after 60 days
- **Testnet (L1 Testnet)**: Irys L1 test chain

---

## Quick Start

### Install CLI

```bash
# Install Irys CLI globally
npm i -g @irys/cli

# Check balance
irys balance 0x[your-address] -t ethereum

# Upload file
irys upload myfile.txt -t ethereum -w [private-key]
```

---

## Node.js Integration

### 1. Install Dependencies

```bash
npm install @irys/upload @irys/upload-ethereum
```

### 2. Basic Connection

```javascript
import { Uploader } from "@irys/upload";
import { Ethereum } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Ethereum)
    .withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

### 3. Fund Management

```javascript
const fundAccount = async () => {
  const irysUploader = await getIrysUploader();
  
  // Check balance
  const balance = await irysUploader.getBalance();
  console.log(`Current balance: ${irysUploader.utils.fromAtomic(balance)} ETH`);
  
  // Fund account
  const fundTx = await irysUploader.fund(
    irysUploader.utils.toAtomic(0.01) // Fund 0.01 ETH
  );
  
  console.log(`Funding successful: ${irysUploader.utils.fromAtomic(fundTx.quantity)} ETH`);
};
```

### 4. Data Upload

```javascript
// Upload text data
const uploadText = async (text) => {
  const irysUploader = await getIrysUploader();
  
  const receipt = await irysUploader.upload(text, {
    tags: [
      { name: "Content-Type", value: "text/plain" },
      { name: "App", value: "MyDApp" }
    ]
  });
  
  return `https://gateway.irys.xyz/${receipt.id}`;
};

// Upload file
const uploadFile = async (filePath) => {
  const irysUploader = await getIrysUploader();
  
  const receipt = await irysUploader.uploadFile(filePath, {
    tags: [
      { name: "Content-Type", value: "image/png" },
      { name: "Collection", value: "MyNFTs" }
    ]
  });
  
  return `https://gateway.irys.xyz/${receipt.id}`;
};

// Upload folder
const uploadFolder = async (folderPath) => {
  const irysUploader = await getIrysUploader();
  
  const receipt = await irysUploader.uploadFolder(folderPath, {
    indexFile: "index.html",
    batchSize: 50
  });
  
  return {
    manifestUrl: `https://gateway.irys.xyz/${receipt.id}`,
    manifestId: receipt.id
  };
};
```

### 5. NFT Metadata Upload Example

```javascript
import * as fs from 'fs';

const uploadNFTMetadata = async (imageFile, metadata) => {
  const irysUploader = await getIrysUploader();
  
  // 1. Upload image
  const imageReceipt = await irysUploader.uploadFile(imageFile, {
    tags: [
      { name: "Content-Type", value: "image/png" },
      { name: "Type", value: "NFT-Asset" }
    ]
  });
  
  // 2. Create metadata
  const nftMetadata = {
    name: metadata.name,
    description: metadata.description,
    image: `https://gateway.irys.xyz/${imageReceipt.id}`,
    attributes: metadata.attributes
  };
  
  // 3. Upload metadata
  const metadataReceipt = await irysUploader.upload(
    JSON.stringify(nftMetadata),
    {
      tags: [
        { name: "Content-Type", value: "application/json" },
        { name: "Type", value: "NFT-Metadata" }
      ]
    }
  );
  
  return {
    imageUrl: `https://gateway.irys.xyz/${imageReceipt.id}`,
    metadataUrl: `https://gateway.irys.xyz/${metadataReceipt.id}`
  };
};
```

---

## React Frontend Integration

### 1. Create React App Configuration

```bash
# Install dependencies
npm install \
  @irys/web-upload \
  @irys/web-upload-ethereum \
  @irys/web-upload-ethereum-ethers-v6 \
  ethers@6 \
  axios

# Install polyfills
npm install react-app-rewired
npm install --save-dev crypto-browserify stream-browserify assert \
  stream-http https-browserify os-browserify url buffer process \
  browserify-zlib path-browserify path node-polyfill-webpack-plugin
```

### 2. Webpack Configuration (config-overrides.js)

```javascript
const NodePolyfillPlugin = require("node-polyfill-webpack-plugin");
const webpack = require("webpack");

module.exports = function override(config) {
  config.plugins = (config.plugins || []).concat([
    new NodePolyfillPlugin(),
    new webpack.ProvidePlugin({
      process: "process/browser.js",
      Buffer: ["buffer", "Buffer"],
    }),
  ]);

  config.resolve.fallback = {
    crypto: require.resolve("crypto-browserify"),
    stream: require.resolve("stream-browserify"),
    assert: require.resolve("assert"),
    http: require.resolve("stream-http"),
    https: require.resolve("https-browserify"),
    os: require.resolve("os-browserify"),
    url: require.resolve("url"),
    zlib: require.resolve("browserify-zlib"),
    buffer: require.resolve("buffer"),
    path: require.resolve("path-browserify"),
  };

  return config;
};
```

### 3. React Component Example

```jsx
import React, { useState } from 'react';
import { ethers } from 'ethers';
import { WebUploader } from '@irys/web-upload';
import { WebEthereum } from '@irys/web-upload-ethereum';
import { EthersV6Adapter } from '@irys/web-upload-ethereum-ethers-v6';

function IrysUploader() {
  const [irysUploader, setIrysUploader] = useState(null);
  const [balance, setBalance] = useState('0');
  const [uploadUrl, setUploadUrl] = useState('');
  const [loading, setLoading] = useState(false);

  // Connect wallet and Irys
  const connectIrys = async () => {
    try {
      if (!window.ethereum) {
        alert('Please install MetaMask!');
        return;
      }

      const provider = new ethers.BrowserProvider(window.ethereum);
      await provider.send("eth_requestAccounts", []);
      
      const uploader = await WebUploader(WebEthereum)
        .withAdapter(EthersV6Adapter(provider));
      
      setIrysUploader(uploader);
      
      // Get balance
      const bal = await uploader.getBalance();
      setBalance(uploader.utils.fromAtomic(bal));
      
      alert(`Connected to Irys! Address: ${uploader.address}`);
    } catch (error) {
      console.error('Connection failed:', error);
    }
  };

  // Fund account
  const fundIrys = async () => {
    if (!irysUploader) return;
    
    try {
      setLoading(true);
      const fundTx = await irysUploader.fund(
        irysUploader.utils.toAtomic(0.001) // Fund 0.001 ETH
      );
      
      const newBalance = await irysUploader.getBalance();
      setBalance(irysUploader.utils.fromAtomic(newBalance));
      
      alert('Funding successful!');
    } catch (error) {
      console.error('Funding failed:', error);
    } finally {
      setLoading(false);
    }
  };

  // Upload file
  const uploadFile = async (event) => {
    const file = event.target.files[0];
    if (!file || !irysUploader) return;
    
    try {
      setLoading(true);
      
      const receipt = await irysUploader.upload(file, {
        tags: [
          { name: "Content-Type", value: file.type },
          { name: "App", value: "React-Irys-Demo" }
        ]
      });
      
      const url = `https://gateway.irys.xyz/${receipt.id}`;
      setUploadUrl(url);
      
      // Update balance
      const newBalance = await irysUploader.getBalance();
      setBalance(irysUploader.utils.fromAtomic(newBalance));
      
    } catch (error) {
      console.error('Upload failed:', error);
      alert('Upload failed: ' + error.message);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div style={{ padding: '20px', maxWidth: '600px', margin: '0 auto' }}>
      <h2>Irys File Upload Demo</h2>
      
      {!irysUploader ? (
        <button onClick={connectIrys} style={{ padding: '10px 20px' }}>
          Connect Wallet and Irys
        </button>
      ) : (
        <div>
          <p><strong>Address:</strong> {irysUploader.address}</p>
          <p><strong>Balance:</strong> {balance} ETH</p>
          
          <div style={{ margin: '20px 0' }}>
            <button 
              onClick={fundIrys} 
              disabled={loading}
              style={{ padding: '10px 20px', marginRight: '10px' }}
            >
              {loading ? 'Processing...' : 'Fund 0.001 ETH'}
            </button>
            
            <input
              type="file"
              onChange={uploadFile}
              disabled={loading}
              style={{ marginLeft: '10px' }}
            />
          </div>
          
          {uploadUrl && (
            <div style={{ marginTop: '20px' }}>
              <h4>Upload Successful!</h4>
              <p>
                <a href={uploadUrl} target="_blank" rel="noopener noreferrer">
                  {uploadUrl}
                </a>
              </p>
            </div>
          )}
        </div>
      )}
    </div>
  );
}

export default IrysUploader;
```

### 4. Vite Configuration Example

For Vite instead of Create React App:

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import { nodePolyfills } from 'vite-plugin-node-polyfills';

export default defineConfig({
  plugins: [
    react(),
    nodePolyfills({
      globals: {
        Buffer: true,
        global: true,
        process: true,
      },
      protocolImports: true,
    }),
  ],
  resolve: {
    alias: {
      crypto: 'crypto-browserify',
      stream: 'stream-browserify',
      os: 'os-browserify/browser',
      path: 'path-browserify',
    },
  },
});
```

---

## Smart Contracts & Programmable Data

Irys's revolutionary feature is **programmable data**, where smart contracts can directly read on-chain stored data.

### 1. Programmable Data Contract Example

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@irys/precompile-libraries/libraries/ProgrammableData.sol";

contract MyDataProcessor is ProgrammableData {
    bytes public storedData;
    address public owner;
    
    event DataProcessed(bytes32 indexed txId, uint256 timestamp);
    
    constructor() {
        owner = msg.sender;
    }
    
    // Read and process data from Irys
    function processIrysData() public {
        require(msg.sender == owner, "Only owner");
        
        (bool success, bytes memory data) = readBytes();
        require(success, "Failed to read Irys data");
        
        // Process data (e.g., validate, parse, store)
        storedData = data;
        
        emit DataProcessed(keccak256(data), block.timestamp);
    }
    
    // Get processed data
    function getProcessedData() public view returns (bytes memory) {
        return storedData;
    }
    
    // Verify data integrity
    function verifyDataIntegrity(bytes memory expectedData) 
        public view returns (bool) {
        return keccak256(storedData) == keccak256(expectedData);
    }
}
```

### 2. JavaScript Client Integration

```javascript
import { IrysClient } from "@irys/js";
import { Wallet } from "ethers";

// Connect to Irys L1 testnet
const irysClient = await new IrysClient("https://testnet-rpc.irys.xyz/v1");

// Upload data to permanent storage
const uploadDataForContract = async (data) => {
  const tx = irysClient.createTransaction({ data });
  await tx.prepareChunks();
  
  const signedTx = await tx.sign(process.env.PRIVATE_KEY);
  await signedTx.uploadHeader();
  await signedTx.uploadChunks();
  
  return tx.id;
};

// Create programmable data access list
const createAccessList = async (transactionId, startOffset, length) => {
  const accessList = await irysClient.programmable_data
    .read(transactionId, startOffset, length)
    .toAccessList();
    
  return accessList;
};

// Call smart contract to process data
const processDataWithContract = async (contractAddress, transactionId) => {
  const wallet = new Wallet(process.env.PRIVATE_KEY, irysClient.api.rpcProvider);
  
  // Create access list
  const accessList = await createAccessList(transactionId, 0, 1024);
  
  // Call contract
  const contract = new ethers.Contract(contractAddress, contractABI, wallet);
  
  const tx = await contract.processIrysData({
    accessList: [accessList],
    type: 2 // EIP-1559 type
  });
  
  await tx.wait();
  console.log("Data processing completed!");
};
```

### 3. Advanced Use Case: Dynamic NFT Metadata

```solidity
// Dynamic NFT contract example
contract DynamicNFT is ERC721, ProgrammableData {
    mapping(uint256 => bytes32) public tokenDataIds;
    mapping(uint256 => uint256) public tokenLevels;
    
    function updateNFTData(uint256 tokenId) external {
        // Read game data from Irys
        (bool success, bytes memory gameData) = readBytes();
        require(success, "Failed to read game data");
        
        // Parse game data to update NFT attributes
        uint256 newLevel = parseGameLevel(gameData);
        tokenLevels[tokenId] = newLevel;
        
        // Update metadata reference
        tokenDataIds[tokenId] = keccak256(gameData);
    }
    
    function parseGameLevel(bytes memory data) 
        internal pure returns (uint256) {
        // Game data parsing logic
        return abi.decode(data, (uint256));
    }
}
```

---

## Real-world Use Cases

### 1. NFT Marketplace

```javascript
// NFT metadata permanent storage
class NFTManager {
  constructor(irysUploader) {
    this.irys = irysUploader;
  }
  
  async createNFT(imageFile, metadata) {
    // Upload image
    const imageReceipt = await this.irys.uploadFile(imageFile);
    
    // Create complete metadata
    const fullMetadata = {
      ...metadata,
      image: `https://gateway.irys.xyz/${imageReceipt.id}`,
      timestamp: Date.now()
    };
    
    // Upload metadata
    const metadataReceipt = await this.irys.upload(
      JSON.stringify(fullMetadata),
      {
        tags: [
          { name: "Content-Type", value: "application/json" },
          { name: "NFT-Collection", value: metadata.collection },
          { name: "Creator", value: metadata.creator }
        ]
      }
    );
    
    return {
      tokenURI: `https://gateway.irys.xyz/${metadataReceipt.id}`,
      imageUrl: `https://gateway.irys.xyz/${imageReceipt.id}`
    };
  }
}
```

### 2. Decentralized Social Media

```javascript
class SocialProtocol {
  async publishPost(content, media = null) {
    const tags = [
      { name: "App", value: "SocialDApp" },
      { name: "Type", value: "Post" },
      { name: "Timestamp", value: Date.now().toString() }
    ];
    
    let mediaUrl = null;
    if (media) {
      const mediaReceipt = await this.irys.uploadFile(media);
      mediaUrl = `https://gateway.irys.xyz/${mediaReceipt.id}`;
    }
    
    const post = {
      content,
      media: mediaUrl,
      author: this.userAddress,
      timestamp: Date.now()
    };
    
    const receipt = await this.irys.upload(JSON.stringify(post), { tags });
    return `https://gateway.irys.xyz/${receipt.id}`;
  }
  
  // Create updatable user profile
  async updateProfile(profile) {
    const tags = [
      { name: "App", value: "SocialDApp" },
      { name: "Type", value: "Profile" },
      { name: "User", value: this.userAddress }
    ];
    
    // If previous profile exists, use mutable reference
    if (this.profileTxId) {
      tags.push({ name: "Root-TX", value: this.profileTxId });
    }
    
    const receipt = await this.irys.upload(JSON.stringify(profile), { tags });
    
    if (!this.profileTxId) {
      this.profileTxId = receipt.id;
    }
    
    return {
      staticUrl: `https://gateway.irys.xyz/${receipt.id}`,
      mutableUrl: `https://gateway.irys.xyz/mutable/${this.profileTxId}`
    };
  }
}
```

### 3. DeFi Protocol Data Storage

```javascript
class DeFiDataManager {
  async storeTransactionBatch(transactions) {
    const batch = {
      transactions,
      blockNumber: await this.provider.getBlockNumber(),
      timestamp: Date.now(),
      protocolVersion: "1.0.0"
    };
    
    const receipt = await this.irys.upload(JSON.stringify(batch), {
      tags: [
        { name: "Protocol", value: "MyDeFiProtocol" },
        { name: "Type", value: "TransactionBatch" },
        { name: "Block", value: batch.blockNumber.toString() }
      ]
    });
    
    // Generate cryptographic receipt as audit proof
    return {
      dataUrl: `https://gateway.irys.xyz/${receipt.id}`,
      auditReceipt: receipt.signature
    };
  }
  
  async storeGovernanceProposal(proposal) {
    const receipt = await this.irys.upload(JSON.stringify(proposal), {
      tags: [
        { name: "Protocol", value: "MyDeFiProtocol" },
        { name: "Type", value: "Proposal" },
        { name: "ProposalId", value: proposal.id.toString() }
      ]
    });
    
    return `https://gateway.irys.xyz/${receipt.id}`;
  }
}
```

### 4. Game Asset Management

```javascript
class GameAssetManager {
  async saveGameState(playerId, gameState) {
    const state = {
      playerId,
      level: gameState.level,
      inventory: gameState.inventory,
      achievements: gameState.achievements,
      timestamp: Date.now()
    };
    
    const tags = [
      { name: "Game", value: "MyGame" },
      { name: "Type", value: "SaveGame" },
      { name: "Player", value: playerId }
    ];
    
    // Use mutable reference to support save updates
    if (gameState.previousSaveId) {
      tags.push({ name: "Root-TX", value: gameState.previousSaveId });
    }
    
    const receipt = await this.irys.upload(JSON.stringify(state), { tags });
    
    return {
      saveId: receipt.id,
      staticUrl: `https://gateway.irys.xyz/${receipt.id}`,
      mutableUrl: gameState.previousSaveId ? 
        `https://gateway.irys.xyz/mutable/${gameState.previousSaveId}` : 
        `https://gateway.irys.xyz/mutable/${receipt.id}`
    };
  }
  
  async createGameItem(itemData, image) {
    // Upload item icon
    const imageReceipt = await this.irys.uploadFile(image);
    
    const item = {
      ...itemData,
      image: `https://gateway.irys.xyz/${imageReceipt.id}`,
      createdAt: Date.now()
    };
    
    const receipt = await this.irys.upload(JSON.stringify(item), {
      tags: [
        { name: "Game", value: "MyGame" },
        { name: "Type", value: "GameItem" },
        { name: "Rarity", value: itemData.rarity }
      ]
    });
    
    return `https://gateway.irys.xyz/${receipt.id}`;
  }
}
```

---

## Best Practices

### 1. Cost Optimization

```javascript
// Batch upload to reduce costs
class BatchUploader {
  constructor(irysUploader) {
    this.irys = irysUploader;
    this.batch = [];
  }
  
  addToBatch(data, tags = []) {
    this.batch.push({ data, tags });
  }
  
  async uploadBatch() {
    const results = [];
    
    // Process in batches to reduce network requests
    for (const chunk of this.chunks(this.batch, 10)) {
      const promises = chunk.map(({ data, tags }) => 
        this.irys.upload(data, { tags })
      );
      
      const receipts = await Promise.all(promises);
      results.push(...receipts);
    }
    
    this.batch = []; // Clear batch
    return results;
  }
  
  *chunks(array, size) {
    for (let i = 0; i < array.length; i += size) {
      yield array.slice(i, i + size);
    }
  }
}
```

### 2. Error Handling and Retry Mechanism

```javascript
class RobustUploader {
  constructor(irysUploader, maxRetries = 3) {
    this.irys = irysUploader;
    this.maxRetries = maxRetries;
  }
  
  async uploadWithRetry(data, options = {}, retryCount = 0) {
    try {
      const receipt = await this.irys.upload(data, options);
      return receipt;
    } catch (error) {
      if (retryCount < this.maxRetries) {
        console.log(`Upload failed, retrying ${retryCount + 1}/${this.maxRetries}`);
        
        // Exponential backoff
        const delay = Math.pow(2, retryCount) * 1000;
        await new Promise(resolve => setTimeout(resolve, delay));
        
        return this.uploadWithRetry(data, options, retryCount + 1);
      }
      
      throw new Error(`Upload failed after ${this.maxRetries} retries: ${error.message}`);
    }
  }
  
  async uploadLargeFile(filePath, chunkSize = 10 * 1024 * 1024) {
    const fs = require('fs');
    const stat = await fs.promises.stat(filePath);
    
    if (stat.size <= chunkSize) {
      return this.uploadWithRetry(await fs.promises.readFile(filePath));
    }
    
    // Large file chunked upload
    console.log(`Large file detected, chunked upload: ${stat.size} bytes`);
    // Implement chunking logic...
  }
}
```

### 3. Data Validation and Integrity Check

```javascript
class SecureUploader {
  async uploadWithVerification(data, options = {}) {
    // Calculate data hash
    const crypto = require('crypto');
    const dataHash = crypto.createHash('sha256').update(data).digest('hex');
    
    // Add integrity tags
    const tags = [
      ...(options.tags || []),
      { name: "Data-Hash", value: dataHash },
      { name: "Upload-Timestamp", value: Date.now().toString() }
    ];
    
    const receipt = await this.irys.upload(data, { ...options, tags });
    
    // Verify upload result
    const uploadedData = await fetch(`https://gateway.irys.xyz/${receipt.id}`)
      .then(res => res.text());
    
    const uploadedHash = crypto.createHash('sha256')
      .update(uploadedData).digest('hex');
    
    if (dataHash !== uploadedHash) {
      throw new Error('Data integrity verification failed');
    }
    
    return {
      ...receipt,
      verified: true,
      dataHash
    };
  }
}
```

### 4. Monitoring and Analytics

```javascript
class IrysAnalytics {
  constructor() {
    this.uploads = [];
    this.costs = [];
  }
  
  trackUpload(receipt, cost, size, type) {
    this.uploads.push({
      id: receipt.id,
      timestamp: Date.now(),
      size,
      cost,
      type,
      url: `https://gateway.irys.xyz/${receipt.id}`
    });
  }
  
  getStats() {
    const totalUploads = this.uploads.length;
    const totalSize = this.uploads.reduce((sum, upload) => sum + upload.size, 0);
    const totalCost = this.uploads.reduce((sum, upload) => sum + upload.cost, 0);
    
    return {
      totalUploads,
      totalSize: this.formatBytes(totalSize),
      totalCost: `${totalCost} ETH`,
      averageCost: `${(totalCost / totalUploads).toFixed(6)} ETH`,
      averageSize: this.formatBytes(totalSize / totalUploads)
    };
  }
  
  formatBytes(bytes) {
    const sizes = ['Bytes', 'KB', 'MB', 'GB'];
    if (bytes === 0) return '0 Bytes';
    const i = Math.floor(Math.log(bytes) / Math.log(1024));
    return `${Math.round(bytes / Math.pow(1024, i) * 100) / 100} ${sizes[i]}`;
  }
}
```

### 5. Environment Configuration Management

```javascript
// config/irys.js
const configs = {
  development: {
    network: 'devnet',
    gateway: 'https://gateway.irys.xyz',
    bundler: 'https://devnet.irys.xyz'
  },
  production: {
    network: 'mainnet',
    gateway: 'https://gateway.irys.xyz',
    bundler: 'https://uploader.irys.xyz'
  },
  testnet: {
    network: 'testnet',
    gateway: 'https://gateway.irys.xyz',
    bundler: 'https://testnet-rpc.irys.xyz/v1'
  }
};

export const getConfig = () => {
  const env = process.env.NODE_ENV || 'development';
  return configs[env];
};
```

### 6. GraphQL Data Querying

```javascript
class IrysQuery {
  constructor() {
    this.endpoint = 'https://uploader.irys.xyz/graphql';
  }
  
  async queryByTags(tags, limit = 10) {
    const query = `
      query GetTransactions($tags: [TagFilter!], $first: Int) {
        transactions(tags: $tags, first: $first) {
          edges {
            node {
              id
              timestamp
              tags {
                name
                value
              }
            }
          }
        }
      }
    `;
    
    const response = await fetch(this.endpoint, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        query,
        variables: { tags, first: limit }
      })
    });
    
    return response.json();
  }
  
  async queryByOwner(address, limit = 10) {
    const query = `
      query GetTransactionsByOwner($owner: String!, $first: Int) {
        transactions(owners: [$owner], first: $first) {
          edges {
            node {
              id
              timestamp
              tags {
                name
                value
              }
            }
          }
        }
      }
    `;
    
    const response = await fetch(this.endpoint, {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        query,
        variables: { owner: address, first: limit }
      })
    });
    
    return response.json();
  }
}
```

---

## Conclusion

Irys, as the first programmable datachain, provides Web3 developers with a revolutionary data storage solution. Through permanent storage, programmability, and multi-chain support, Irys solves many pain points of traditional storage solutions.

### Core Advantages Summary

1. **Permanent and Economical**: Pay-once, store-forever with lower long-term costs
2. **Truly Decentralized**: No dependency on traditional cloud service providers
3. **Programmable Data**: Smart contracts can directly access stored data
4. **Multi-chain Flexibility**: Support for 20+ blockchain networks for payments
5. **Developer Friendly**: Rich SDKs and toolchains

### Quick Start Recommendations

1. **Start with Testnet**: Use devnet to familiarize with APIs and workflows
2. **Small-scale Testing**: Upload small files first to understand cost structure
3. **Integrate into Existing Projects**: Gradually migrate storage needs to Irys
4. **Explore Programmable Features**: Try smart contract interactions with stored data

Irys is redefining the future of Web3 data storage, and now is the perfect time to start building!

---

## Related Resources

- 📚 [Official Documentation](https://docs.irys.xyz/)
- 🚀 [GitHub Repository](https://github.com/Irys-xyz/)
- 💬 [Discord Community](https://discord.gg/irys)
- 🔍 [Block Explorer](https://explorer.irys.xyz/)
- 💧 [Testnet Faucet](https://irys.xyz/faucet)