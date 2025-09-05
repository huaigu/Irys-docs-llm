# Installing, Importing & Configuring

The Irys SDK reduces dependency bloat by providing dedicated packages for each token. Your install statements, import and connection code will differ depending on the token used for payment.

Select the appropriate code from the options below when starting your project.

[APTOS](https://docs.irys.xyz/build/d/sdk/setup#aptos) | [Arbitrum](https://docs.irys.xyz/build/d/sdk/setup#arbitrum) | [Avalanche C-Chain](https://docs.irys.xyz/build/d/sdk/setup#avalanche-c-chain) | [Berachain](https://docs.irys.xyz/build/d/sdk/setup#berachain) | [BNB](https://docs.irys.xyz/build/d/sdk/setup#bnb) | [Chainlink](https://docs.irys.xyz/build/d/sdk/setup#chainlink) | [Eclipse-eth](https://docs.irys.xyz/build/d/sdk/setup#eclipse-eth) | [Ethereum](https://docs.irys.xyz/build/d/sdk/setup#ethereum) | [Base Ethereum](https://docs.irys.xyz/build/d/sdk/setup#base-ethereum) | [Linea Ethereum](https://docs.irys.xyz/build/d/sdk/setup#linea-ethereum) | [Scroll Ethereum](https://docs.irys.xyz/build/d/sdk/setup#scroll-ethereum) | [IoTeX](https://docs.irys.xyz/build/d/sdk/setup#iotex) | [Polygon](https://docs.irys.xyz/build/d/sdk/setup#polygon) | [Solana](https://docs.irys.xyz/build/d/sdk/setup#solana) | [USDC (on Ethereum)](https://docs.irys.xyz/build/d/sdk/setup#usdc-on-ethereum) | [USDC (on Polygon)](https://docs.irys.xyz/build/d/sdk/setup#usdc-on-polygon)

ℹ️

The following code examples connect to our alpha testnet. To switch to our devnet, append the functions `withRpc()` and `devnet()` as [outlined here](https://docs.irys.xyz/build/d/networks#connecting-to-devnet).

## Aptos

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-aptos
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Aptos } from "@irys/upload-aptos";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Aptos).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Arbitrum

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Arbitrum } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Arbitrum).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Avalanche C-Chain

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Avalanche } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Avalanche).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Berachain

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Bera } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Bera).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## BNB

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { BNB } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(BNB).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Chainlink

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Chainlink } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Chainlink).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Eclipse-eth

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-solana
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { EclipseEth } from "@irys/upload-solana";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(EclipseEth).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Ethereum

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Ethereum } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Ethereum).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Base Ethereum

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { BaseEth } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(BaseEth).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Linea Ethereum

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { LineaEth } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(LineaEth).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Scroll Ethereum

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { ScrollEth } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(ScrollEth).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## IoTeX

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Iotex } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Iotex).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Polygon

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Matic } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Matic).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## Solana

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-solana
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { Solana } from "@irys/upload-solana";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(Solana).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## USDC (on Ethereum)

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content.none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { USDCEth } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(USDCEth).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```

## USDC (on Polygon)

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install @irys/upload @irys/upload-ethereum
```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import { Uploader } from "@irys/upload";
import { USDCPolygon } from "@irys/upload-ethereum";

const getIrysUploader = async () => {
  const irysUploader = await Uploader(USDCPolygon).withWallet(process.env.PRIVATE_KEY);
  return irysUploader;
};
```