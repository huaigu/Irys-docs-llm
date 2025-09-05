{
  "networks": [
    {
      "name": "Mainnet",
      "description": "Uploads are paid for with real tokens. At mainnet L1 launch, all data uploaded to these bundlers will be uploaded to mainnet, with no changes to transaction IDs."
    },
    {
      "name": "Devnet",
      "description": "Uploads are paid for with free faucet tokens. Data is deleted after ~60 days."
    }
  ],
  "testnet": {
    "name": "L1 testnet",
    "description": "An L1 testnet for testing purposes."
  },
  "connectingToMainnet": {
    "codeSnippet": "import { Uploader } from \"@irys/upload\";\nimport { Ethereum } from \"@irys/upload-ethereum\";\n\nconst getIrysUploader = async () => {\n  const irysUploader = await Uploader(Ethereum).withWallet(process.env.PRIVATE_KEY);\n  return irysUploader;\n};"
  },
  "connectingToDevnet": {
    "codeSnippet": "import { Uploader } from \"@irys/upload\";\nimport { Ethereum } from \"@irys/upload-ethereum\";\n\nconst getIrysUploader = async () => {\n  const rpcURL = \"\";\n  const irysUploader = await Uploader(Ethereum)\n    .withWallet(process.env.PRIVATE_KEY)\n    .withRpc(rpcURL)\n    .devnet();\n  return irysUploader;\n};"
  }
}