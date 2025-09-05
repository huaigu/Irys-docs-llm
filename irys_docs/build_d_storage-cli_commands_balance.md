```json
{
  "date": "2025-09-03T09:19:59.208Z",
  "title": "Irys | balance",
  "url": "https://docs.irys.xyz/build/d/storage-cli/commands/balance",
  "description": "Returns the amount of funds available on the specified node. Provide your public wallet address as an argument, along with parameters for network, token, and provider URL.",
  "parameters": [
    {
      "option": "-n",
      "description": "The network to check, 'mainnet' or 'devnet', defaults to 'mainnet'."
    },
    {
      "option": "-t",
      "description": "The token to use when funding."
    },
    {
      "option": "--provider-url",
      "description": "RPC URL to use."
    }
  ],
  "examples": [
    {
      "network": "Mainnet",
      "command": "irys balance 0x591B5Ce7cA10a55A9B5d1516eF89693D5b3586b8 -t ethereum"
    },
    {
      "network": "Devnet",
      "command": "irys balance 0x591B5Ce7cA10a55A9B5d1516eF89693D5b3586b8 -t ethereum -n devnet --provider-url https://rpc.sepolia.dev"
    }
  ],
  "note": "RPC URLs change often, use a recent one from https://chainlist.org/"
}
```