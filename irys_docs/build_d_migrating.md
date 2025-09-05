# Migrating to the Irys L1

The Irys testnet is now live with support for permanent data uploads, and temporary data support coming soon. In the coming weeks, we’ll also introduce the [IrysVM](https://docs.irys.xyz/learn/why-build-on-irys/irysvm) and [Programmable Data](https://docs.irys.xyz/learn/why-build-on-irys/programmable-data). **Irys provides early access to all these new features for developers building on our platform.**

At mainnet launch, all data uploaded to bundlers will be migrated from testnet to mainnet, with no changes to transaction IDs.

ℹ️

If you're not ready to migrate yet, you do not have to do anything. Irys's bundlers and gateway for Arweave will continue to operate as normal.

## How to Migrate

The new Irys Bundler SDK reduces dependency bloat by providing dedicated packages for each token. Previously, Irys used a single import statement and connection code regardless of token, with our new SDK, code is unique per token.

**Migrating your code is simple and straight-forward.**

### NodeJS

Change This:

```typescript
import Irys from "@irys/sdk";

const getIrys = async () => {
	const irys = new Irys({
		network: "mainnet",
		token: "ethereum",
		key: process.env.PRIVATE_KEY,
	});
	return irys;
};
```

To This:

```typescript
import { Uploader } from "@irys/upload";
import { Ethereum } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Ethereum).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

ℹ️

The above code is for ethereum only, [we also have examples](https://docs.irys.xyz/build/d/sdk/setup) covering all supported tokens.

### Browser

Change This:

```typescript
import { WebIrys } from "@irys/sdk";
import { ethers } from "ethers";

const getWebIrys = async () => {
	await window.ethereum.enable();
	const provider = new providers.Web3Provider(window.ethereum);
	const wallet = { rpcUrl: rpcUrl, name: "ethersv5", provider: provider };
	const webIrys = new WebIrys({ network: "mainnet", token: "ethereum", wallet });
	await webIrys.ready();

	return webIrys;
};
```

To This:

```typescript
import { WebUploader } from "@irys/web-upload";
import { WebEthereum } from "@irys/web-upload-ethereum";
import { EthereumEthersv5 } from "@irys/web-upload-ethereum-ethers-v5";

const getIrysUploader = async () => {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const irysUploader = await WebUploader(WebEthereum).withProvider(EthereumEthersv5(provider));
  return irysUploader;
};
```

ℹ️

The above code is for ethereum with ethers v5 only, [we also have examples](https://docs.irys.xyz/build/d/irys-in-the-browser) covering all supported tokens and providers.

## Support

Need help or just have questions? Come [find us in Discord](https://discord.gg/irys).