# Solidity / Web3 cheatsheet

## Motivation

This document is totally personal, so it won't be really useful to you, random user. Sorry.

## Useful links
[OpenZeppelin Doc](https://docs.openzeppelin.com/contracts/4.x/)
[OpenZeppelin Wizard](https://docs.openzeppelin.com/contracts/4.x/wizard)

## Communicate to other contract
```solidity
const ethers = require("ethers");
const { abi } = require("./ABI");

(async () => {
  const rpc = await new ethers.providers.JsonRpcProvider(
    "https://api.avax.network/ext/bc/C/rpc"
  );
  const wallet = new ethers.Wallet(
    "PRIVATE_KEY",
    rpc
  );
  const contract = new ethers.Contract(
    "CONTRACT_ADDRESS",
    abi,
    wallet
  );
  contract.on("Transfer", async (from, to, value) => {
    if (from === "0x0000000000000000000000000000000000000000") {
      console.log('New mint, tokenId: ', value.toNumber());
    }
  });
})();
```

ABI looks like that
```javascript
const ABI = [...];

module.exports = { abi };
```

### How to get the ABI
Go the snowtrace or etherscan on the contract address, go to #code and scroll down, export ABI -> JSON.

### How to launch with hardhat
```javascript
  networks: {
    mainnet: {
      url: "https://api.avax.network/ext/bc/C/rpc",
      gasPrice: 225000000000,
      chainId: 43114,
      accounts: [],
    },
  },
```
```bash
npx hardhat run --network mainnet scripts/XX.js
```
