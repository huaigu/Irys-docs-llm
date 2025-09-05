{
  "title": "Using Irys With React + Vite",
  "steps": [
    {
      "step": 1,
      "title": "Setup a New Project",
      "description": "Create a new directory for your project, navigate into it, and initialize it with Vite:",
      "code": "mkdir irys-vite\ncd irys-vite\nnpm create vite@latest .\n",
      "note": "Choose React and select either TypeScript or JavaScript. After selecting the framework, run: \nnpm install\n"
    },
    {
      "step": 2,
      "title": "Install the Irys SDK, Ethers, and Axios",
      "description": "Install the necessary packages, including the Irys SDK, Ethers, and Axios:",
      "code": "npm install \n    @irys/web-upload \n    @irys/web-upload-ethereum \n    @irys/web-upload-ethereum-ethers-v6 \n    ethers@6 \n    axios\n"
    },
    {
      "step": 3,
      "title": "Initialize the Irys Uploader",
      "description": "In your App.tsx file, write an initialization function to set up an Irys uploader using Ethers v6:",
      "code": "import { useState } from 'react';\nimport { ethers } from 'ethers';\nimport { WebUploader } from '@irys/web-upload';\nimport { WebEthereum } from '@irys/web-upload-ethereum';\nimport { EthersV6Adapter } from '@irys/web-upload-ethereum-ethers-v6';\n\nfunction App() {\n  const [walletStatus, setWalletStatus] = useState('Not connected');\n  const [irysStatus, setIrysStatus] = useState('Not connected');\n\n  const connectWallet = async () => {\n    console.log('connect wallet');\n\n    if (typeof window.ethereum === 'undefined') {\n      console.error('No Ethereum provider found. Please install MetaMask or another wallet.');\n      setWalletStatus('No Ethereum provider found. Please install MetaMask or another wallet.');\n      return;\n    }\n\n    try {\n      const provider = new ethers.BrowserProvider(window.ethereum);\n      await provider.send('eth_requestAccounts', []);\n      const signer = await provider.getSigner();\n      const address = await signer.getAddress();\n      setWalletStatus(`Connected: ${address}`);\n    } catch (error) {\n      console.error('Error connecting to wallet:', error);\n      setWalletStatus('Error connecting to wallet');\n    }\n  };\n\n  const connectIrys = async () => {\n    if (typeof window.ethereum === 'undefined') {\n      console.error('No Ethereum provider found. Please install MetaMask or another wallet.');\n      setIrysStatus('No Ethereum provider found. Please install MetaMask or another wallet.');\n      return;\n    }\n\n    try {\n      const provider = new ethers.BrowserProvider(window.ethereum);\n      const irysUploader = await WebUploader(WebEthereum).withAdapter(EthersV6Adapter(provider));\n      setIrysStatus(`Connected to Irys: ${irysUploader.address}`);\n    } catch (error) {\n      console.error('Error connecting to Irys:', error);\n      setIrysStatus('Error connecting to Irys');\n    }\n  };\n\n  return (\n    <div>\n      <button onClick={connectWallet}>Connect Wallet</button>\n      <p>{walletStatus}</p>\n      <button onClick={connectIrys}>Connect Irys</button>\n      <p>{irysStatus}</p>\n    </div>\n  );\n}\n\nexport default App;\n"
    }
  ]
}