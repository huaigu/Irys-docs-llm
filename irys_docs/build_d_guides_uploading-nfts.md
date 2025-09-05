# Uploading NFTs to Irys

When you use Irys to store NFT assets, you’re guaranteed your NFT will be both permanent and immutable. Here’s how you do it.

## NFT Assets

![](https://docs.irys.xyz/build/guides/nfts/nft-metadata.png)

There are three parts to an NFT:

1. Smart contract
2. NFT metadata
3. NFT assets

The smart contract stores a pointer to the NFT metadata, and then the NFT metadata contains links to the NFT assets.

In the example above, there is a `name` and `description` that are shown on platforms like Opensea when the NFT is viewed. The `image` parameter points to a static image of the NFT. You can also add an optional `animation_url` that points to a video, song, or HTML animation file.

## Creating an NFT

Three steps to creating an NFT:

1. Upload your assets to Irys.
2. Embed the URLs to the assets in NFT metadata.
3. Upload metadata to Irys.
4. Use the metadata URL to mint your NFT.

## Uploading Assets (SDK)

After [installing the Irys SDK](https://docs.irys.xyz/build/d/sdk/setup), upload your assets with:

ℹ️

Use a token-specific version of `getIrysUploader()` to connect to an Irys Bundler before uploading. Choose [one from here](https://docs.irys.xyz/build/d/sdk/setup).

```js
import * as fs from "fs";

const uploadImage = async () => {
	const irys = await getIrysUploader();
	const fileToUpload = "./myNFT.png";

	// Get size of file
	const { size } = await fs.promises.stat(fileToUpload);
	// Get cost to upload "size" bytes
	const price = await irys.getPrice(size);
	console.log(`Uploading ${size} bytes costs ${irys.utils.fromAtomic(price)} ${token}`);
	await irys.fund(price);

	// Upload metadata
	try {
		const response = await irys.uploadFile(fileToUpload);
		console.log(`File uploaded ==> https://gateway.irys.xyz/${response.id}`);
	} catch (e) {
		console.log("Error uploading file ", e);
	}
};
```

## Uploading Assets (CLI)

Alternatively, you can [upload](https://docs.irys.xyz/build/d/storage-cli/commands/upload) using our [Storage CLI](https://docs.irys.xyz/build/d/storage-cli/installation).

```console
irys upload myNFT.png \
  -n devnet \
  -t ethereum \
  -w bf20......c9885307 \
  --tags Content-Type image/png \
  --provider-url https://rpc.sepolia.dev
```

## Creating Metadata

Embed the URLs generated from the above into your NFT metadata.

```json
{
	"name": "My NFT",
	"symbol": "MNFT",
	"description": "To the moooooonnnn",
	"image": "https://gateway.irys.xyz/737m0bA1kW4BlIJOg_kOGUpHAAI-3Ec9bdo8S_xTFKI"
}
```

## Uploading Metadata (SDK)

Finally, upload your NFT metadata to Irys and use the URL generated to mint the NFT.

```js
import { Uploader } from "@irys/upload";
import * as fs from "fs";

const uploadMetadata = async () => {
	const irys = await getIrysUploader();

	const fileToUpload = "./metadata.json";
	const tags = [{ name: "Content-Type", value: "application/json" }];

	// Get size of file
	const { size } = await fs.promises.stat(fileToUpload);
	// Get cost to upload "size" bytes
	const price = await irys.getPrice(size);
	console.log(`Uploading ${size} bytes costs ${irys.utils.fromAtomic(price)} ${token}`);
	await irys.fund(price);

	// Upload metadata
	try {
		const response = await irys.uploadFile(fileToUpload, { tags: tags });
		console.log(`File uploaded ==> https://gateway.irys.xyz/${response.id}`);
	} catch (e) {
		console.log("Error uploading file ", e);
	}
};
```

## Uploading Metadata (CLI)

Alternatively, you can [upload](https://docs.irys.xyz/build/d/storage-cli/commands/upload) using our [Storage CLI](https://docs.irys.xyz/build/d/storage-cli/installation).

```console
irys upload metadata.json \
  -n devnet \
  -t ethereum \
  -w bf20......c9885307 \
  --tags Content-Type application/json \
  --provider-url https://rpc.sepolia.dev
```
