{
  "title": "Irys | Quickstart",
  "url": "https://docs.irys.xyz/build/programmability/js/quickstart",
  "sections": [
    {
      "heading": "Install",
      "content": "yarn install @irys/js"
    },
    {
      "heading": "Grab some tokens!",
      "content": "The testnet faucet can be found [here](https://irys.xyz/faucet)"
    },
    {
      "heading": "Create the client",
      "content": "const irysClient = await new IrysClient(\"https://testnet-rpc.irys.xyz/v1\")"
    },
    {
      "heading": "Get your Irys address",
      "content": "Irys uses the same private keys as Ethereum\nconst { irys: irysAddress } = irysClient.account.getAddresses(\"private key\")"
    },
    {
      "heading": "Check your balance",
      "content": "const balancemIrys = await irysClient.account.getBalance(\"address\") // you can use either your Irys or execution address!"
    },
    {
      "heading": "Create and post a data transaction",
      "content": "// Create a transaction\nconst tx = irysClient.createTransaction({...}) // the args are optional\n// Generates merkle tree for the data\nawait tx.prepareChunks(<data>);\n// Check the price (in mIrys) for uploading your transaction.\n// Irys transactions have two fees, a term and a perm fee.\n// perm is only for if you want to store your data permanently (i.e ledger 0)\n// Testnet currently only supports `perm` transactions.\nconst { termFee, permFee } = await tx.getFees();\n// get the combined fee\nconst fee = await tx.getFee();\n// Sign the transaction with your private key\nconst signedTx = await tx.sign(<key>);\n// Upload the transaction header\nawait signedTx.uploadHeader();\n// Upload the data\nawait signedTx.uploadChunks(<data>);"
    }
  ]
}