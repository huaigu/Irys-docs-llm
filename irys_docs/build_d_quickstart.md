# Irys SDK

## Installing

This example uses ETH for payment. You can use any of the [supported tokens](https://docs.irys.xyz/build/d/features/supported-tokens).

Install using npm:

```bash
npm install @irys/upload @irys/upload-ethereum
```

## Connecting to the network

The following code is for using ETH for payment, we [also have examples covering all supported tokens](https://docs.irys.xyz/build/d/sdk/setup).

```typescript
import { Uploader } from "@irys/upload";
import { Ethereum } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Ethereum).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Funding Irys

Fund your account on the Irys network using any of our [supported tokens](https://docs.irys.xyz/build/d/features/supported-tokens):

```javascript
const fundAccount = async () => {
	const irysUploader = await getIrysUploader();
	try {
		const fundTx = await irysUploader.fund(irysUploader.utils.toAtomic(0.05));
		console.log(`Successfully funded ${irysUploader.utils.fromAtomic(fundTx.quantity)} ${irysUploader.token}`);
	} catch (e) {
		console.log("Error when funding ", e);
	}
};
```

## Uploading

### Uploading Data

```javascript
const uploadData = async () => {
	const irysUploader = await getIrysUploader();
	const dataToUpload = "hirys world.";
	try {
		const receipt = await irysUploader.upload(dataToUpload);
		console.log(`Data uploaded ==> https://gateway.irys.xyz/${receipt.id}`);
	} catch (e) {
		console.log("Error when uploading ", e);
	}
};
```

### Uploading a File

```javascript
const uploadFile = async () => {
	const irysUploader = await getIrysUploader();
	// Your file
	const fileToUpload = "./myImage.png";

	const tags = [{ name: "application-id", value: "MyNFTDrop" }];

	try {
		const receipt = await irysUploader.uploadFile(fileToUpload, { tags: tags });
		console.log(`File uploaded ==> https://gateway.irys.xyz/${receipt.id}`);
	} catch (e) {
		console.log("Error when uploading ", e);
	}
};
```

### Uploading a Folder

You can upload a group of files as a single transaction from both the server and the browser.

ℹ️

When [uploading a folder](https://docs.irys.xyz/build/d/sdk/upload/uploadFolder), files can be accessed either directly at
`https://gateway.irys.xyz/:transactionId` or `https://gateway.irys.xyz/:manifestId/:fileName`

```javascript
const uploadFolder = async () => {
	const irysUploader = await getIrysUploader();

	// Upload an entire folder
	const folderToUpload = "./my-images/"; // Path to folder
	try {
		const receipt = await irysUploader.uploadFolder("./" + folderToUpload, {
			indexFile: "", // Optional index file (file the user will load when accessing the manifest)
			batchSize: 50, // Number of items to upload at once
			keepDeleted: false, // whether to keep now deleted items from previous uploads
		}); // Returns the manifest ID

		console.log(`Files uploaded. Manifest ID ${receipt.id}`);
	} catch (e) {
		console.log("Error when uploading ", e);
	}
};
```

## 3rd-Party Build Tools

### Parcel

If using [Parcel](https://parceljs.org/), you will need to [manually enable package exports](https://parceljs.org/features/dependency-resolution/#package-exports) by adding the following to the `package.json` file in your project root directory.

```json
{
	"@parcel/resolver-default": {
		"packageExports": true
	}
}
```