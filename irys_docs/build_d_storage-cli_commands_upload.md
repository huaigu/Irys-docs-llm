```json
{
  "title": "Irys | upload",
  "description": "Uploads a single file.",
  "parameters": {
    "-n": "The network to check, 'mainnet' or 'devnet', defaults to 'mainnet'.",
    "-t": "The token to use when funding.",
    "-w": "Your private key.",
    "--tags": "Tags to include, format <name> <value>.",
    "--provider-url": "RPC URL to use."
  },
  "examples": {
    "mainnet": "irys upload myImage.png -t ethereum -w bf20......c9885307 --tags tagName1 tagValue1 tagName2 tagValue2",
    "devnet": "irys upload myImage.png -n devnet -t ethereum -w bf20......c9885307 --tags tagName1 tagValue1 tagName2 tagValue2 --provider-url https://rpc.sepolia.dev"
  },
  "downloading": "Files uploaded via 'irys upload' can be downloaded using the transaction ID provided after a successful upload.",
  "metadata": {
    "og:image": "https://docs.irys.xyz/opengraph-image.png?8c892bc9b92ee1a8",
    "og:title": "Irys | upload",
    "language": "en",
    "url": "https://docs.irys.xyz/build/d/storage-cli/commands/upload",
    "favicon": "https://docs.irys.xyz/favicon.ico"
  }
}
```