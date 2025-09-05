# Using Irys With npx create-react-app

ℹ️

If you're using React with Vite, polyfills are handled differently. You'll need to follow [this guide instead](https://docs.irys.xyz/build/d/guides/vite).

Irys is fully compatible with React, however, if you’re using `npx create-react-app` to create your project, you will need to do some additional configuration and installation. This guide details how to create a new React project and add Irys support. If you already have a React project, skip the first step.

## Step 1: Create a New React Project

Create a new directory for your project, cd into it, and create your React project:

```bash
mkdir irys-react
cd irys-react
npx create-react-app .
```

## Step 2: Install the Irys SDK, Ethers, and Axios

```bash
npm install \
    @irys/web-upload \
    @irys/web-upload-ethereum \
    @irys/web-upload-ethereum-ethers-v6 \
    ethers@6 \
    axios
```

## Step 3: Initialize the Irys Uploader

In your `App.js` file, write an initialization function that sets up an Irys uploader. The following code shows how to use ethers6. We also have code examples for [different providers](https://docs.irys.xyz/build/d/irys-in-the-browser).

```typescript
import React, { useState } from "react";
import { ethers } from "ethers";
import { WebUploader } from "@irys/web-upload";
import { WebEthereum } from "@irys/web-upload-ethereum";
import { EthersV6Adapter } from "@irys/web-upload-ethereum-ethers-v6";

function App() {
  const [walletStatus, setWalletStatus] = useState("Not connected");
  const [irysStatus, setIrysStatus] = useState("Not connected");

  const connectWallet = async () => {
    try {
      const provider = new ethers.BrowserProvider(window.ethereum);
      await provider.send("eth_requestAccounts", []);
      const signer = await provider.getSigner();
      const address = await signer.getAddress();
      setWalletStatus(`Connected: ${address}`);
    } catch (error) {
      console.error("Error connecting to wallet:", error);
      setWalletStatus("Error connecting to wallet");
    }
  };

  const connectIrys = async () => {
    try {
      const provider = new ethers.BrowserProvider(window.ethereum);
      const irysUploader = await WebUploader(WebEthereum).withAdapter(EthersV6Adapter(provider));
      setIrysStatus(`Connected to Irys: ${irysUploader.address}`);
    } catch (error) {
      console.error("Error connecting to Irys:", error);
      setIrysStatus("Error connecting to Irys");
    }
  };

  return (
    <div>
      <button onClick={connectWallet}>Connect Wallet</button>
      <p>{walletStatus}</p>
      <button onClick={connectIrys}>Connect Irys</button>
      <p>{irysStatus}</p>
    </div>
  );
}

export default App;
```

When you try to run the app, you see this similar to this `BREAKING CHANGE: webpack < 5 used to include polyfills for node.js core modules by default`.

To fix this, you'll need to include Node.js polyfills that are not included by default.

## Step 4: Install React-App-Rewired and Polyfills

Install react-app-rewired, a package that allows you to customize the Webpack configuration to handle the polyfills, and the missing dependencies:

```bash
npm install react-app-rewired
npm install --save-dev crypto-browserify stream-browserify assert stream-http https-browserify os-browserify url buffer process
npm install browserify-zlib path-browserify path
npm install node-polyfill-webpack-plugin --save-dev
```

## Step 5: Create the Webpack Configuration Override

At the root level of your project, create a new file called `config-overrides.js` and paste the following:

```typescript
const NodePolyfillPlugin = require("node-polyfill-webpack-plugin");
const webpack = require("webpack");

module.exports = function override(config) {
  config.plugins = (config.plugins || []).concat([
    new NodePolyfillPlugin(),
    new webpack.ProvidePlugin({
      process: "process/browser.js",
    }),
  ]);

  const fallback = config.resolve.fallback || {};
  Object.assign(fallback, {
    crypto: require.resolve("crypto-browserify"),
    stream: require.resolve("stream-browserify"),
    assert: require.resolve("assert"),
    http: require.resolve("stream-http"),
    https: require.resolve("https-browserify"),
    os: require.resolve("os-browserify"),
    url: require.resolve("url"),
    zlib: require.resolve("browserify-zlib"),
    buffer: require.resolve("buffer"),
    path: require.resolve("path-browserify"),
  });

  config.resolve.fallback = fallback;
  config.resolve.extensions = [".js", ".jsx", ".json", ".mjs", ".wasm", ".css"];

  return config;
};
```

## Step 6: Update package.json Scripts

Modify your `package.json` to use the new Webpack configuration. Look for this code block:

```json
 "scripts": {
   "start": "react-scripts start",
   "build": "react-scripts build",
   "test": "react-scripts test",
   "eject": "react-scripts eject"
 },
```

and replace it with this block:

```json
"scripts": {
   "start": "react-app-rewired start",
   "build": "react-app-rewired build",
   "test": "react-app-rewired test",
   "eject": "react-scripts eject"
},
```

## Step 7: Restart Your React App

Quit the React development server if it's running and restart it:

```bash
npm start
```

You should now be good to go! Your React app is set up with all necessary polyfills and is ready to use the Irys SDK.
