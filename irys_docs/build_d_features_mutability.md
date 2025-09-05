# Mutability

Data on Irys is immutable. However, you can simulate mutability on using mutable references.

With mutable references you create a single, static URL that is linked to a sequential series of transactions. You can add a new transaction to the series at any time, and the URL will always resolve to the most recent transaction in the chain.

![](https://docs.irys.xyz/build/img/mutable-references.png)

To create a mutable reference:

1. Upload a base transaction to Irys and reference it using a URL in the following format `https://gateway.irys.xyz/mutable/:txId`

ℹ️

Use a token-specific version of `getIrysUploader()` to connect to an Irys Bundler before uploading. Choose [one from here](https://docs.irys.xyz/build/d/sdk/setup).

```bash
const irysUploader = await getIrysUploader();
const receiptOne = await irysUploader.upload("First TX");
console.log(`TX 1 uploaded https://gateway.irys.xyz/mutable/${receiptOne.id}`);
```

2. Upload an addition to the series as a new transaction, and add a tag named `Root-TX` with the value of the original transaction ID.

```bash
const tags = [{ name: "Root-TX", value: receiptOne.id }];
const receiptTwo = await irysUploader.upload("Second TX", { tags: tags });
console.log(`TX 2 uploaded https://gateway.irys.xyz/mutable/${receiptOne.id}`);
```

The original URL ( `https://gateway.irys.xyz/mutable/:txId`) now resolves to the second transaction in the chain.

ℹ️

When building a transaction chain, additions must be made using the same wallet that created the original transaction.
This prevents unauthorized actors from maliciously modifying someone else’s transaction chain.

## Granularity

Mutable references are based on Irys’s millisecond-accurate timestamps. You can publish multiple sequential updates to a given transaction and be confident the transaction served by the `/mutable/` endpoint will always be the most recent chronological one.

## Versions

While the `https://gateway.irys.xyz/mutable/:txId` endpoint will always resolve to the most recent transaction in a chain, it is possible to directly access any transaction in a chain using the transaction’s ID and a URL in the format `https://gateway.irys.xyz/:id`

You can query a version chain using GraphQL:

```javascript
query getChain {
  transactions(
    tags: [
      {
        name: "Root-TX"
        values: ["WF--VR1ZERvABYy1aNYD3QJ0OAVDSUF8dTlg6zFKveQ"]
      }
    ]
    owners: ["0x591b5ce7ca10a55a9b5d1516ef89693d5b3586b8"]
    order: ASC
  ) {
    edges {
      node {
        id
        timestamp
      }
    }
  }
}
```

## Use-Cases

Irys’s mutable references open up new opportunities for builders, including:

- Gaming NFTs: Metadata changes based on in-game actions
- Dynamic NFTs: Images change based on onchain activity
- Software distribution: The latest version is always available via the same link
- Content publishing / social media: Content can be updated at any time and users will always have the most recent version
- Website hosting / dApp front-ends: Websites can be updated at any time without changing the main URL