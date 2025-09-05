```json
{
  "title": "Irys | Connecting to the Testnet",
  "networkRPC": {
    "node": "testnet-rpc.irys.xyz",
    "wallet": "wallet.irys.xyz",
    "explorer": "testnet-explorer.irys.xyz",
    "description": "The chain is EVM compatible so you can use all standard EVM tooling including Metamask. The network also has custom endpoints for all datachain related activity."
  },
  "chainInfo": {
    "ticker": "IRYS",
    "atomicUnit": "mIRYS (mini IRYS)",
    "decimals": 18,
    "chainID": 1270,
    "jsonRPCURL": "https://testnet-rpc.irys.xyz/v1/execution-rpc"
  },
  "connectingWithEthers": "const irysClient = await new IrysClient(\"https://testnet-rpc.irys.xyz/v1\")\nconst provider = irysClient.api.rpcProvider\n// or\nconst provider = new JsonRpcProvider(\"https://testnet-rpc.irys.xyz/v1/execution-rpc\")\n\nconst balance = await provider.getBalance(\"<address>\")"
}
```