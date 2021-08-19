## Full stack Upgradeable NFT Marketplace built with BSC, Solidity, IPFS, & Next.js


### Running this project

#### Gitpod

To deploy this project to Gitpod, follow these steps:

1. Click this link to deploy

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#github.com/dabit3/polygon-ethereum-nextjs-marketplace)

2. In __pages/index.js__, pass in the RPC address given to you by GitPod to the call to `JsonRpcProvider` function:

```javascript
/* update this: */
const provider = new ethers.providers.JsonRpcProvider()

/* to this: */
const provider = new ethers.providers.JsonRpcProvider("https://8545-youendpoint.gitpod.io/")
```

3. Import the RPC address given to you by GitPod into your MetaMask wallet

![MetaMask RPC Import](wallet.png)

#### Local setup

To run this project locally, follow these steps.

1. Clone the project locally, change into the directory, and install the dependencies:

```sh
git clone https://github.com/liuhaidong/bsc-nextjs-marketplace.git

cd bsc-nextjs-marketplace

# install using NPM or Yarn
npm install

# or

yarn
```

2. Start the local Hardhat node

```sh
npx hardhat node
```

3. With the network running, 
3.1. deploy the contracts to the local network in a separate terminal window

```sh
npx hardhat run scripts/deploy.js --network localhost
```
3.2. deploy the contracts to the bsc test network by

```sh
npx hardhat run scripts/deploy.js --network testnet
```
For latest bsc rpc node , please check the page:
https://docs.binance.org/smart-chain/developer/rpc.html

4. Start the app

```
npm run dev
```

### Configuration

To deploy to Polygon test or main networks, update the configurations located in __hardhat.config.js__ to use a private key and, optionally, deploy to a private RPC like Infura.

```javascript
require("@nomiclabs/hardhat-waffle");
const fs = require('fs');
const privateKey = fs.readFileSync(".secret").toString().trim() || "01234567890123456789";

// infuraId is optional if you are using Infura RPC
const infuraId = fs.readFileSync(".infuraid").toString().trim() || "";

module.exports = {
  defaultNetwork: "hardhat",
  networks: {
    hardhat: {
      chainId: 1337
    },
    testnet: {
      url: "https://data-seed-prebsc-1-s1.binance.org:8545",
      chainId: 97,
      gasPrice: 20000000000,
      accounts: [privateKey]
    },
    //accounts: {mnemonic: mnemonic}
    mainnet: {
      url: "https://bsc-dataseed.binance.org/",
      chainId: 56,
      gasPrice: 20000000000,
      accounts: [privateKey]
    }
  },
  solidity: {
    version: "0.8.4",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200
      }
    }
  }
};
```

If using Infura, update __.infuraid__ with your [Infura](https://infura.io/) project ID.
