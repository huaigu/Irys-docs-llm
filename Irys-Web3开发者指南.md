# Irys Web3 开发者指南

## 目录
- [什么是 Irys？](#什么是-irys)
- [核心架构](#核心架构)
- [技术特性](#技术特性)
- [支持的区块链](#支持的区块链)
- [快速开始](#快速开始)
- [Node.js 集成](#nodejs-集成)
- [React 前端集成](#react-前端集成)
- [智能合约与可编程数据](#智能合约与可编程数据)
- [实际应用场景](#实际应用场景)
- [最佳实践](#最佳实践)

---

## 什么是 Irys？

Irys 是世界首个**可编程数据链（Programmable Datachain）**，专为 Web3 开发者设计的去中心化存储解决方案。

### 核心价值主张

- 🔗 **数据链**：作为 L1 区块链，原生激励数据存储
- ⚡ **可编程性**：智能合约可以直接访问、操作和写入存储层
- 🛡️ **永久存储**：一次付费，永久存储，数据不可篡改
- ⚙️ **多链支持**：支持 20+ 区块链网络付费（ETH、MATIC、SOL、AVAX 等）
- 📊 **精确时间戳**：毫秒级准确的时间戳和加密收据
- 🔄 **可变引用**：通过链式引用实现"可变"数据

### 与传统存储方案对比

| 特性 | Irys | IPFS | AWS S3 | Arweave |
|------|------|------|--------|---------|
| 永久存储 | ✅ | ❌ | ❌ | ✅ |
| 可编程性 | ✅ | ❌ | ❌ | ❌ |
| 多链支付 | ✅ | ❌ | ❌ | ❌ |
| 毫秒时间戳 | ✅ | ❌ | ❌ | ❌ |
| 智能合约访问 | ✅ | ❌ | ❌ | ❌ |

---

## 核心架构

```
╔═══════════════════════════════════════════════════════════════╗
║                           用户层                                ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────┐    ║
║  │   dApp      │  │    CLI      │  │   SDK       │  │Browser│    ║
║  │   前端      │  │   工具      │  │   集成      │  │  钱包 │    ║
║  └─────────────┘  └─────────────┘  └─────────────┘  └───────┘    ║
╠═══════════════════════════════════════════════════════════════╣
║                          应用层                                 ║
║  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             ║
║  │   NFT       │  │  社交媒体   │  │   游戏      │             ║
║  │  市场       │  │   协议      │  │   资产      │             ║
║  └─────────────┘  └─────────────┘  └─────────────┘             ║
╠═══════════════════════════════════════════════════════════════╣
║                      Irys 协议层                               ║
║  ┌─────────────────────────────────────────────────────────┐    ║
║  │                   Bundler 网络                         │    ║
║  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  │    ║
║  │  │ Bundler │  │ Bundler │  │ Bundler │  │ Bundler │  │    ║
║  │  │   #1    │  │   #2    │  │   #3    │  │   #4    │  │    ║
║  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘  │    ║
║  └─────────────────────────────────────────────────────────┘    ║
║                                                               ║
║  ┌─────────────────────────────────────────────────────────┐    ║
║  │                 IrysVM (智能合约执行)                    │    ║
║  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │    ║
║  │  │ 可编程数据  │  │  时间戳     │  │   收据      │     │    ║
║  │  │   访问      │  │   系统      │  │   系统      │     │    ║
║  │  └─────────────┘  └─────────────┘  └─────────────┘     │    ║
║  └─────────────────────────────────────────────────────────┘    ║
╠═══════════════════════════════════════════════════════════════╣
║                        存储层                                  ║
║  ┌─────────────────────────────────────────────────────────┐    ║
║  │              永久数据存储                              │    ║
║  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  │    ║
║  │  │  数据   │  │  元数据 │  │  标签   │  │  索引   │  │    ║
║  │  │  分片   │  │        │  │  系统   │  │  系统   │  │    ║
║  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘  │    ║
║  └─────────────────────────────────────────────────────────┘    ║
╠═══════════════════════════════════════════════════════════════╣
║                      区块链支付层                              ║
║  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐   ║
║  │   ETH   │ │ Polygon │ │ Solana  │ │ Arbitrum│ │ Avalanche│  ║
║  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘   ║
║  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐   ║
║  │   BSC   │ │  Near   │ │  Aptos  │ │  Base   │ │   IoTeX │   ║
║  └─────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘   ║
╚═══════════════════════════════════════════════════════════════╝

数据流向：
用户 → SDK/CLI → Bundler → IrysVM → 永久存储 ← 区块链付费
     ↓
智能合约 ← 可编程数据访问 ← 存储层查询
```

### 架构说明

1. **用户层**：开发者通过 SDK、CLI 或浏览器接口与 Irys 交互
2. **应用层**：各种 Web3 应用场景，如 NFT、DeFi、社交协议等
3. **Irys 协议层**：
   - **Bundler 网络**：负责数据聚合、验证和上传
   - **IrysVM**：基于 EVM 的虚拟机，支持智能合约执行
4. **存储层**：永久数据存储，支持标签索引和 GraphQL 查询
5. **区块链支付层**：支持多链代币支付存储费用

---

## 技术特性

### 1. 永久存储（Pay-once, Store-forever）

```typescript
// 一次付费，永久存储
const receipt = await irysUploader.upload("Hello Irys!");
console.log(`永久存储 URL: https://gateway.irys.xyz/${receipt.id}`);
```

### 2. 可变引用系统

虽然数据本身不可变，但可以通过链式引用实现"可变"效果：

```typescript
// 基础交易
const baseReceipt = await irysUploader.upload("版本 1.0");

// 更新版本（引用原始交易）
const tags = [{ name: "Root-TX", value: baseReceipt.id }];
const updateReceipt = await irysUploader.upload("版本 2.0", { tags });

// 访问可变 URL，总是返回最新版本
// https://gateway.irys.xyz/mutable/${baseReceipt.id}
```

### 3. 标签系统

```typescript
const tags = [
  { name: "Content-Type", value: "application/json" },
  { name: "App-Name", value: "MyDApp" },
  { name: "Version", value: "1.0.0" },
  { name: "Author", value: "0x..." }
];

const receipt = await irysUploader.upload(data, { tags });
```

### 4. 链上文件夹

```typescript
// 上传整个文件夹
const manifest = await irysUploader.uploadFolder("./assets/", {
  indexFile: "index.html", // 默认文件
  batchSize: 50
});

// 访问文件夹中的特定文件
// https://gateway.irys.xyz/${manifest.id}/logo.png
```

### 5. 加密收据和时间戳

```typescript
const receipt = await irysUploader.upload(data);
/*
收据包含：
{
  id: "交易ID",
  timestamp: 1676891681110, // 毫秒精度
  version: "1.0.0",
  signature: "加密签名",
  public: "公钥",
  ...
}
*/
```

---

## 支持的区块链

### 主网支持的代币

| 区块链 | 代币 | 参数值 | Node.js | Browser |
|--------|------|--------|---------|---------|
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

### 网络选择

- **主网（Mainnet）**：真实代币付费，数据永久存储
- **开发网（Devnet）**：测试代币，数据 60 天后删除
- **测试网（L1 Testnet）**：Irys L1 测试链

---

## 快速开始

### 安装 CLI

```bash
# 全局安装 Irys CLI
npm i -g @irys/cli

# 查看余额
irys balance 0x[你的地址] -t ethereum

# 上传文件
irys upload myfile.txt -t ethereum -w [私钥]
```

---

## Node.js 集成

### 1. 安装依赖

```bash
npm install @irys/upload @irys/upload-ethereum
```

### 2. 基础连接

```javascript
import { Uploader } from "@irys/upload";
import { Ethereum } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Ethereum)
    .withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

### 3. 资金管理

```javascript
const fundAccount = async () => {
  const irysUploader = await getIrysUploader();
  
  // 检查余额
  const balance = await irysUploader.getBalance();
  console.log(`当前余额: ${irysUploader.utils.fromAtomic(balance)} ETH`);
  
  // 充值
  const fundTx = await irysUploader.fund(
    irysUploader.utils.toAtomic(0.01) // 充值 0.01 ETH
  );
  
  console.log(`充值成功: ${irysUploader.utils.fromAtomic(fundTx.quantity)} ETH`);
};
```

### 4. 数据上传

```javascript
// 上传文本数据
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

// 上传文件
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

// 上传文件夹
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

### 5. NFT 元数据上传示例

```javascript
import * as fs from 'fs';

const uploadNFTMetadata = async (imageFile, metadata) => {
  const irysUploader = await getIrysUploader();
  
  // 1. 上传图片
  const imageReceipt = await irysUploader.uploadFile(imageFile, {
    tags: [
      { name: "Content-Type", value: "image/png" },
      { name: "Type", value: "NFT-Asset" }
    ]
  });
  
  // 2. 创建元数据
  const nftMetadata = {
    name: metadata.name,
    description: metadata.description,
    image: `https://gateway.irys.xyz/${imageReceipt.id}`,
    attributes: metadata.attributes
  };
  
  // 3. 上传元数据
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

## React 前端集成

### 1. Create React App 配置

```bash
# 安装依赖
npm install \
  @irys/web-upload \
  @irys/web-upload-ethereum \
  @irys/web-upload-ethereum-ethers-v6 \
  ethers@6 \
  axios

# 安装 polyfills
npm install react-app-rewired
npm install --save-dev crypto-browserify stream-browserify assert \
  stream-http https-browserify os-browserify url buffer process \
  browserify-zlib path-browserify path node-polyfill-webpack-plugin
```

### 2. Webpack 配置（config-overrides.js）

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

### 3. React 组件示例

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

  // 连接钱包和 Irys
  const connectIrys = async () => {
    try {
      if (!window.ethereum) {
        alert('请安装 MetaMask!');
        return;
      }

      const provider = new ethers.BrowserProvider(window.ethereum);
      await provider.send("eth_requestAccounts", []);
      
      const uploader = await WebUploader(WebEthereum)
        .withAdapter(EthersV6Adapter(provider));
      
      setIrysUploader(uploader);
      
      // 获取余额
      const bal = await uploader.getBalance();
      setBalance(uploader.utils.fromAtomic(bal));
      
      alert(`已连接 Irys! 地址: ${uploader.address}`);
    } catch (error) {
      console.error('连接失败:', error);
    }
  };

  // 充值
  const fundIrys = async () => {
    if (!irysUploader) return;
    
    try {
      setLoading(true);
      const fundTx = await irysUploader.fund(
        irysUploader.utils.toAtomic(0.001) // 充值 0.001 ETH
      );
      
      const newBalance = await irysUploader.getBalance();
      setBalance(irysUploader.utils.fromAtomic(newBalance));
      
      alert('充值成功!');
    } catch (error) {
      console.error('充值失败:', error);
    } finally {
      setLoading(false);
    }
  };

  // 上传文件
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
      
      // 更新余额
      const newBalance = await irysUploader.getBalance();
      setBalance(irysUploader.utils.fromAtomic(newBalance));
      
    } catch (error) {
      console.error('上传失败:', error);
      alert('上传失败: ' + error.message);
    } finally {
      setLoading(false);
    }
  };

  return (
    <div style={{ padding: '20px', maxWidth: '600px', margin: '0 auto' }}>
      <h2>Irys 文件上传演示</h2>
      
      {!irysUploader ? (
        <button onClick={connectIrys} style={{ padding: '10px 20px' }}>
          连接钱包和 Irys
        </button>
      ) : (
        <div>
          <p><strong>地址:</strong> {irysUploader.address}</p>
          <p><strong>余额:</strong> {balance} ETH</p>
          
          <div style={{ margin: '20px 0' }}>
            <button 
              onClick={fundIrys} 
              disabled={loading}
              style={{ padding: '10px 20px', marginRight: '10px' }}
            >
              {loading ? '处理中...' : '充值 0.001 ETH'}
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
              <h4>上传成功！</h4>
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

### 4. Vite 配置示例

如果使用 Vite 而不是 Create React App：

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

## 智能合约与可编程数据

Irys 的革命性特性是**可编程数据**，智能合约可以直接读取链上存储的数据。

### 1. 可编程数据合约示例

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
    
    // 从 Irys 读取数据并处理
    function processIrysData() public {
        require(msg.sender == owner, "Only owner");
        
        (bool success, bytes memory data) = readBytes();
        require(success, "Failed to read Irys data");
        
        // 处理数据（例如：验证、解析、存储）
        storedData = data;
        
        emit DataProcessed(keccak256(data), block.timestamp);
    }
    
    // 获取处理后的数据
    function getProcessedData() public view returns (bytes memory) {
        return storedData;
    }
    
    // 验证数据完整性
    function verifyDataIntegrity(bytes memory expectedData) 
        public view returns (bool) {
        return keccak256(storedData) == keccak256(expectedData);
    }
}
```

### 2. JavaScript 客户端集成

```javascript
import { IrysClient } from "@irys/js";
import { Wallet } from "ethers";

// 连接 Irys L1 测试网
const irysClient = await new IrysClient("https://testnet-rpc.irys.xyz/v1");

// 上传数据到永久存储
const uploadDataForContract = async (data) => {
  const tx = irysClient.createTransaction({ data });
  await tx.prepareChunks();
  
  const signedTx = await tx.sign(process.env.PRIVATE_KEY);
  await signedTx.uploadHeader();
  await signedTx.uploadChunks();
  
  return tx.id;
};

// 创建可编程数据访问列表
const createAccessList = async (transactionId, startOffset, length) => {
  const accessList = await irysClient.programmable_data
    .read(transactionId, startOffset, length)
    .toAccessList();
    
  return accessList;
};

// 调用智能合约处理数据
const processDataWithContract = async (contractAddress, transactionId) => {
  const wallet = new Wallet(process.env.PRIVATE_KEY, irysClient.api.rpcProvider);
  
  // 创建访问列表
  const accessList = await createAccessList(transactionId, 0, 1024);
  
  // 调用合约
  const contract = new ethers.Contract(contractAddress, contractABI, wallet);
  
  const tx = await contract.processIrysData({
    accessList: [accessList],
    type: 2 // EIP-1559 类型
  });
  
  await tx.wait();
  console.log("数据处理完成!");
};
```

### 3. 高级用例：NFT 动态元数据

```solidity
// 动态 NFT 合约示例
contract DynamicNFT is ERC721, ProgrammableData {
    mapping(uint256 => bytes32) public tokenDataIds;
    mapping(uint256 => uint256) public tokenLevels;
    
    function updateNFTData(uint256 tokenId) external {
        // 从 Irys 读取游戏数据
        (bool success, bytes memory gameData) = readBytes();
        require(success, "Failed to read game data");
        
        // 解析游戏数据更新 NFT 属性
        uint256 newLevel = parseGameLevel(gameData);
        tokenLevels[tokenId] = newLevel;
        
        // 更新元数据引用
        tokenDataIds[tokenId] = keccak256(gameData);
    }
    
    function parseGameLevel(bytes memory data) 
        internal pure returns (uint256) {
        // 解析游戏数据逻辑
        return abi.decode(data, (uint256));
    }
}
```

---

## 实际应用场景

### 1. NFT 市场

```javascript
// NFT 元数据永久存储
class NFTManager {
  constructor(irysUploader) {
    this.irys = irysUploader;
  }
  
  async createNFT(imageFile, metadata) {
    // 上传图片
    const imageReceipt = await this.irys.uploadFile(imageFile);
    
    // 创建完整元数据
    const fullMetadata = {
      ...metadata,
      image: `https://gateway.irys.xyz/${imageReceipt.id}`,
      timestamp: Date.now()
    };
    
    // 上传元数据
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

### 2. 去中心化社交媒体

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
  
  // 创建可更新的用户资料
  async updateProfile(profile) {
    const tags = [
      { name: "App", value: "SocialDApp" },
      { name: "Type", value: "Profile" },
      { name: "User", value: this.userAddress }
    ];
    
    // 如果有之前的资料，使用可变引用
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

### 3. DeFi 协议数据存储

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
    
    // 生成加密收据作为审计证明
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

### 4. 游戏资产管理

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
    
    // 使用可变引用支持存档更新
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
    // 上传物品图标
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

## 最佳实践

### 1. 成本优化

```javascript
// 批量上传以降低成本
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
    
    // 批量处理，减少网络请求
    for (const chunk of this.chunks(this.batch, 10)) {
      const promises = chunk.map(({ data, tags }) => 
        this.irys.upload(data, { tags })
      );
      
      const receipts = await Promise.all(promises);
      results.push(...receipts);
    }
    
    this.batch = []; // 清空批次
    return results;
  }
  
  *chunks(array, size) {
    for (let i = 0; i < array.length; i += size) {
      yield array.slice(i, i + size);
    }
  }
}
```

### 2. 错误处理和重试机制

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
        console.log(`上传失败，重试 ${retryCount + 1}/${this.maxRetries}`);
        
        // 指数退避
        const delay = Math.pow(2, retryCount) * 1000;
        await new Promise(resolve => setTimeout(resolve, delay));
        
        return this.uploadWithRetry(data, options, retryCount + 1);
      }
      
      throw new Error(`上传失败，已重试 ${this.maxRetries} 次: ${error.message}`);
    }
  }
  
  async uploadLargeFile(filePath, chunkSize = 10 * 1024 * 1024) {
    const fs = require('fs');
    const stat = await fs.promises.stat(filePath);
    
    if (stat.size <= chunkSize) {
      return this.uploadWithRetry(await fs.promises.readFile(filePath));
    }
    
    // 大文件分块上传
    console.log(`大文件检测，分块上传: ${stat.size} bytes`);
    // 实现分块逻辑...
  }
}
```

### 3. 数据验证和完整性检查

```javascript
class SecureUploader {
  async uploadWithVerification(data, options = {}) {
    // 计算数据哈希
    const crypto = require('crypto');
    const dataHash = crypto.createHash('sha256').update(data).digest('hex');
    
    // 添加完整性标签
    const tags = [
      ...(options.tags || []),
      { name: "Data-Hash", value: dataHash },
      { name: "Upload-Timestamp", value: Date.now().toString() }
    ];
    
    const receipt = await this.irys.upload(data, { ...options, tags });
    
    // 验证上传结果
    const uploadedData = await fetch(`https://gateway.irys.xyz/${receipt.id}`)
      .then(res => res.text());
    
    const uploadedHash = crypto.createHash('sha256')
      .update(uploadedData).digest('hex');
    
    if (dataHash !== uploadedHash) {
      throw new Error('数据完整性验证失败');
    }
    
    return {
      ...receipt,
      verified: true,
      dataHash
    };
  }
}
```

### 4. 监控和分析

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

### 5. 环境配置管理

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

### 6. GraphQL 数据查询

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

## 结语

Irys 作为首个可编程数据链，为 Web3 开发者提供了革命性的数据存储解决方案。通过永久存储、可编程性和多链支持，Irys 解决了传统存储方案的诸多痛点。

### 核心优势总结

1. **永久且经济**：一次付费永久存储，长期成本更低
2. **真正去中心化**：无需依赖传统云服务提供商
3. **可编程数据**：智能合约可直接访问存储数据
4. **多链灵活性**：支持 20+ 区块链网络付费
5. **开发者友好**：丰富的 SDK 和工具链

### 快速开始建议

1. **从测试网开始**：使用 devnet 熟悉 API 和工作流程
2. **小规模试验**：先上传小文件，了解成本结构
3. **集成到现有项目**：逐步将存储需求迁移到 Irys
4. **探索可编程特性**：尝试智能合约与存储数据的交互

Irys 正在重新定义 Web3 数据存储的未来，现在是开始构建的最佳时机！

---

## 相关资源

- 📚 [官方文档](https://docs.irys.xyz/)
- 🚀 [GitHub 仓库](https://github.com/Irys-xyz/)
- 💬 [Discord 社区](https://discord.gg/irys)
- 🔍 [区块浏览器](https://explorer.irys.xyz/)
- 💧 [测试网水龙头](https://irys.xyz/faucet)