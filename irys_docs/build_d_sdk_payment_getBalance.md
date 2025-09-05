{
  "title": "Irys | getBalance()",
  "url": "https://docs.irys.xyz/build/d/sdk/payment/getBalance",
  "description": "Returns the connected wallet's balance.",
  "returns": {
    "type": "BigNumber",
    "description": "Wallet balance in atomic units. You can convert it into standard units using irys.utils.fromAtomic()."
  },
  "example": "const irys = await getIrysUploader();\n// Get loaded balance in atomic units\nconst atomicBalance = await irys.getBalance();\nconsole.log(`Node balance (atomic units) = ${atomicBalance}`);\n// Convert balance to standard\nconst convertedBalance = irys.utils.fromAtomic(atomicBalance);\nconsole.log(`Node balance (converted) = ${convertedBalance}`);",
  "metadata": {
    "twitter:title": "Irys | getBalance()",
    "ogImage": "https://docs.irys.xyz/opengraph-image.png?8c892bc9b92ee1a8",
    "twitter:image": "https://docs.irys.xyz/opengraph-image.png?8c892bc9b92ee1a8",
    "twitter:image:type": "image/png",
    "viewport": "width=device-width, initial-scale=1",
    "twitter:image:width": "1200",
    "og:title": "Irys | getBalance()",
    "twitter:image:height": "600",
    "og:image:type": "image/png",
    "favicon": "https://docs.irys.xyz/favicon.ico",
    "language": "en",
    "og:image:width": "1200",
    "twitter:card": "summary_large_image",
    "og:image:height": "600",
    "scrapeId": "c7deb1c1-b332-4a59-b944-48e9ccaadd45",
    "sourceURL": "https://docs.irys.xyz/build/d/sdk/payment/getBalance"
  }
}