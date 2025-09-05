Search... `⌘K`

[Explorer](https://explorer.irys.xyz/) [Github](https://github.com/Irys-xyz)

### Learn

### What

### Why

### Network Overview

### Protocol Overview

### Build

### ONCHAIN STORAGE

[Quickstart](https://docs.irys.xyz/build/d/quickstart) [Mainnet / Devnet](https://docs.irys.xyz/build/d/networks)

### Features

### SDK

[Irys in the Browser](https://docs.irys.xyz/build/d/irys-in-the-browser)

### Storage CLI

### REST API

### Guides

[Downloading](https://docs.irys.xyz/build/d/downloading) [Querying](https://docs.irys.xyz/build/d/graphql) [Troubleshooting](https://docs.irys.xyz/build/d/troubleshooting) [Migrating](https://docs.irys.xyz/build/d/migrating)

### PROGRAMMABILITY

# [Irys in The Browser](https://docs.irys.xyz/build/d/irys-in-the-browser\#irys-in-the-browser)

The Irys SDK reduces dependency bloat by providing dedicated packages for each token. Your install statements, import and connection code will differ depending on the token used for payment and the provider used.

Choose the code for your provider:

🚀

If you're using Irys with React, follow
[these extra setup steps](https://docs.irys.xyz/build/d/guides/irys-react). If you're using Irys with Vite, [follow these steps](https://docs.irys.xyz/build/d/guides/vite).

[Ethers v5](https://docs.irys.xyz/build/d/irys-in-the-browser#ethers-v5) \| [Ethers v6](https://docs.irys.xyz/build/d/irys-in-the-browser#ethers-v6) \| [Viem v2](https://docs.irys.xyz/build/d/irys-in-the-browser#viem-v2) \| [Solana](https://docs.irys.xyz/build/d/irys-in-the-browser#solana) \| [Aptos](https://docs.irys.xyz/build/d/irys-in-the-browser#aptos)

## [EVM Chains](https://docs.irys.xyz/build/d/irys-in-the-browser\#evm-chains)

When connecting from an EVM chain, your connection code will differ based on the token you're using. The examples below use Ethereum and the `WebEthereum` class. To change tokens, use one from the following list.

| Token | Class Name |
| --- | --- |
| Polygon | `WebMatic` |
| Binance Coin | `WebBNB` |
| Avalanche C-Chain | `WebAvalanche` |
| Base Ethereum | `WebBaseEth` |
| USDC (on Ethereum) | `WebUSDCEth` |
| Arbitrum | `WebArbitrum` |
| Chainlink | `WebChainlink` |
| USDC (on Polygon) | `WebUSDCPolygon` |
| Berachain | `WebBera` |
| Scroll Ethereum | `WebScrollEth` |
| Linea Ethereum | `WebLineaEth` |
| IoTeX | `WebIotex` |
| Ethereum | `WebEthereum` |

### [Ethers v5](https://docs.irys.xyz/build/d/irys-in-the-browser\#ethers-v5)

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install \
    @irys/web-upload \
    @irys/web-upload-ethereum \
    ethers@5

```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs js
import { WebUploader } from "@irys/web-upload";
import { WebEthereum } from "@irys/web-upload-ethereum";

const getIrysUploader = async () => {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const irysUploader = await WebUploader(WebEthereum).withProvider(provider);

  return irysUploader;
};

```

### [Ethers v6](https://docs.irys.xyz/build/d/irys-in-the-browser\#ethers-v6)

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install \
    @irys/web-upload \
    @irys/web-upload-ethereum \
    @irys/web-upload-ethereum-ethers-v6 \
    ethers@6

```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs js
import { WebUploader } from "@irys/web-upload";
import { WebEthereum } from "@irys/web-upload-ethereum";
import { EthersV6Adapter } from "@irys/web-upload-ethereum-ethers-v6";
import { ethers } from "ethers";

const getIrysUploader = async () => {
  const provider = new ethers.BrowserProvider(window.ethereum);
  const irysUploader = await WebUploader(WebEthereum).withAdapter(EthersV6Adapter(provider));

  return irysUploader;
};

```

### [Viem v2](https://docs.irys.xyz/build/d/irys-in-the-browser\#viem-v2)

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install \
    @irys/web-upload \
    @irys/web-upload-ethereum \
    @irys/web-upload-ethereum-viem-v2 \
    viem

```

Importing & Configuring:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs js
import { WebUploader } from "@irys/web-upload";
import { WebEthereum } from "@irys/web-upload-ethereum";
import { ViemV2Adapter } from "@irys/web-upload-ethereum-viem-v2";

const getIrysUploader = async () => {
  const [account] = await window.ethereum.request({ method: "eth_requestAccounts",});

  const provider = createWalletClient({
    account,
    chain: sepolia,
    transport: custom(window.ethereum),
  });

  const publicClient = createPublicClient({
    chain: sepolia,
    transport: custom(window.ethereum),
  });

  const irysUploader = await WebUploader(WebEthereum).withAdapter(ViemV2Adapter(provider, { publicClient }));

  return irysUploader;
};

```

## [Solana](https://docs.irys.xyz/build/d/irys-in-the-browser\#solana)

Installing:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install \
    @irys/web-upload \
    @irys/web-upload-solana
    @solana/wallet-adapter-base \
    @solana/wallet-adapter-react \
    @solana/wallet-adapter-react-ui \
    @solana/wallet-adapter-wallets \
    @solana/web3.js

```

Importing & Configuring:

The Solana library uses the React provider pattern. Start by setting up a top-level file named `ClientProviders.tsx` that wraps all your child components.

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
"use client";

import { ReactNode, useMemo } from "react";
import { ConnectionProvider, WalletProvider } from "@solana/wallet-adapter-react";
import { WalletAdapterNetwork } from "@solana/wallet-adapter-base";
import { UnsafeBurnerWalletAdapter } from "@solana/wallet-adapter-wallets";
import { WalletModalProvider } from "@solana/wallet-adapter-react-ui";
import { clusterApiUrl } from "@solana/web3.js";

require("@solana/wallet-adapter-react-ui/styles.css");

export default function ClientProviders({ children }: { children: ReactNode }) {
 const network = WalletAdapterNetwork.Devnet;

 const endpoint = useMemo(() => clusterApiUrl(network), [network]);
 const wallets = useMemo(
   () => [new UnsafeBurnerWalletAdapter()],
   [network]
 );

 return (
   <ConnectionProvider endpoint={endpoint}>
     <WalletProvider wallets={wallets} autoConnect>
       <WalletModalProvider>
         {children}
       </WalletModalProvider>
     </WalletProvider>
   </ConnectionProvider>
 );
}

```

Then load this component via `layout.tsx`:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import type { Metadata } from "next";
import ClientProviders from "@/app/components/ClientProviders";
import { Inter } from "next/font/google";
const inter = Inter({ subsets: ["latin"] });

export default function RootLayout({
 children,
}: Readonly<{
 children: React.ReactNode;
}>) {
 return (
   <html lang="en">
     <body className={inter.className}>
       <ClientProviders>
         {children}
       </ClientProviders>
     </body>
   </html>
 );
}

```

[Solana's wallet-adapter library](https://solana.com/developers/cookbook/wallets/connect-wallet-react) make it easy to manage wallet connections. Create a component using this library to connect to a Solana wallet:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts

"use client";

import React, { useEffect, useState } from "react";
import { WalletMultiButton, WalletDisconnectButton } from "@solana/wallet-adapter-react-ui";

import "@solana/wallet-adapter-react-ui/styles.css";

const ConnectSolana: React.FC = () => {
  const [isClient, setIsClient] = useState(false);

  // Prevent hydration errors by ensuring this runs only on the client side
  useEffect(() => {
    setIsClient(true);
  }, []);

  if (!isClient) {
    return null;
  }

  return (
    <div className="border-2 border-primary rounded-2xl p-4 w-full max-w-md">
      {/* Solana wallet connect button */}
      <div className="mr-5">
        <WalletMultiButton />
      </div>
      {/* Solana wallet disconnect button */}
      <div className="ml-5">
        <WalletDisconnectButton />
      </div>
    </div>
  );
};

export default ConnectSolana;

```

Then create a component called `ConnectIrys.tsx` that connects to an Irys bundler.

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts

"use client";

import { useState } from "react";
import { useWallet } from "@solana/wallet-adapter-react";
import { WebUploader } from "@irys/web-upload";
import { WebSolana } from "@irys/web-upload-solana";

const getIrysUploader = async (wallet: any) => {
 try {
   const irysUploader = await WebUploader(WebSolana).withProvider(wallet);

   return irysUploader;
 } catch (error) {
   console.error("Error connecting to Irys:", error);
   throw new Error("Error connecting to Irys");
 }
};

const ConnectIrys = (): JSX.Element => {
 const wallet = useWallet();
 const [isConnected, setIsConnected] = useState<boolean>(false);

 const connectToIrys = async () => {
   if (!wallet) {
     console.log("Wallet not connected");
     return;
   }

   try {
     const irysUploader = await getIrysUploader(wallet);
     console.log(`Connected to Irys from ${irysUploader.address}`);
     setIsConnected(true);
   } catch (error) {
     console.log("Error connecting to Irys");
   }
 };

 return (
   <div>
     <button onClick={connectToIrys}>
       {isConnected ? "Connected to Irys" : "Connect Irys"}
     </button>
   </div>
 );
};

export default ConnectIrys;

```

And load them all through your `page.tsx` file:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import Image from "next/image";
import ConnectSolana from "./components/ConnectSolana";
import ConnectIrys from "./components/ConnectIrys";

export default function Home() {
  return (
    <main className="flex min-h-screen flex-col justify-around items-center p-24 bg-black">
      <ConnectSolana />
      <ConnectIrys />
    </main>
  );
}

```

## [Aptos](https://docs.irys.xyz/build/d/irys-in-the-browser\#aptos)

Start by scaffolding a blank Aptos project using [`npx create-aptos-dapp`](https://aptos.dev/en/build/create-aptos-dapp).

Next, install the following packages needed by Irys:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs console
npm install \
    @irys/web-upload \
    @irys/web-upload-aptos \
    axios

```

Replace your `App.tsx` file with the following:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs tsx
import React, { useState } from "react";
import { useWallet } from "@aptos-labs/wallet-adapter-react";
import { WebUploader } from "@irys/web-upload";
import { WebAptos } from "@irys/web-upload-aptos";

// Radix UI Components
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Header } from "@/components/Header";

function App() {
  const { connected } = useWallet();
  const wallet = useWallet();
  const [irysStatus, setIrysStatus] = useState("Not connected");

  const connectIrys = async () => {
    console.log("connect irys called");
    console.log({wallet})
    try {
      const irysUploader = await WebUploader(WebAptos).withProvider(wallet);
      console.log({irysUploader})

      setIrysStatus(`Connected to Irys: ${irysUploader.address}`);
    } catch (error) {
      console.error("Error connecting to Irys:", error);
      setIrysStatus("Error connecting to Irys");
    }
  };

  return (
    <>
      <Header />
      <div className="flex items-center justify-center flex-col">
        <Card className="mt-6">
          <CardHeader>
            {connected ? (
              <CardTitle>
                <button onClick={connectIrys}>
                  {irysStatus === "Not connected" ? "Connect Irys" : irysStatus}
                </button>
              </CardTitle>
            ) : (
              <CardTitle>To get started, connect a wallet</CardTitle>
            )}
          </CardHeader>
        </Card>
      </div>
    </>
  );
}

export default App;

```

The `npx create-aptos-dapp` CLI uses React + Vite. Vite does not automatically polyfill Node.js core modules like crypto, stream, os, or path. To fix compatibility issues, install the necessary polyfill packages:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs bash
npm install --save-dev \
    crypto-browserify \
    stream-browserify \
    os-browserify \
    path-browserify \
    vite-plugin-node-polyfills

```

Modify your `vite.config.js` to use `vite-plugin-node-polyfills` to handle the polyfills required for Node.js core modules:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs ts
import path from "path";
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import { nodePolyfills } from "vite-plugin-node-polyfills";

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [\
    react(),\
    nodePolyfills({\
      // Enable polyfills for specific globals and modules\
      globals: {\
        Buffer: true,\
        global: true,\
        process: true,\
      },\
      protocolImports: true, // Polyfill node: protocol imports\
    }),\
  ],
  resolve: {
    alias: {
      // Polyfill Node.js core modules
      crypto: "crypto-browserify",
      stream: "stream-browserify",
      os: "os-browserify/browser",
      path: "path-browserify",
      "@": path.resolve(__dirname, "./frontend"),
    },
  },
  build: {
    outDir: "dist", // Output directory
  },
  server: {
    open: true,
  },
});

```

After making these changes, restart your development server:

```bg-grey2/80 p-1 rounded-md text-grey5 before:!content-none after:!content-none normal-case hljs bash
npm run dev

```