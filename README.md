# Foundry Smart Contract Raffle

![Chainlink VRF](img/secured_chainlink_badge.png)

## Table of Contents

- [Foundry Smart Contract Raffle](#foundry-smart-contract-raffle)
  - [Table of Contents](#table-of-contents)
  - [About](#about)
  - [Requirements](#requirements)
  - [Dependencies](#dependencies)
  - [Foundry](#foundry)
  - [Documentation](#documentation)
  - [Deploy](#deploy)
  - [Testing](#testing)
- [Deployment to a testnet or mainnet](#deployment-to-a-testnet-or-mainnet)
  - [Scripts](#scripts)
  - [Estimate gas](#estimate-gas)
- [Formatting](#formatting)
- [Thank you!](#thank-you)
    - [Contributing](#contributing)
  - [License](#license)
- [Thank you Patrick Collins!](#thank-you-patrick-collins)

## About

This is a provably random smart contract raffle written in Solidity. The contract uses Chainlink VRF to generate true randomness and Chainlink automation to automate the raffle.

## Requirements

To use this project, you will need:

- A local Ethereum node, such as Anvil.
- A Chainlink node with VRF capability.
- Solidity compiler version 0.8.0 or higher.
- A Etherscan API key.
- If you want to deploy the contract on a testnet, you will need a node as a service provider, such as Alchemy.
- You will need to fund your contract with LINK tokens.
- Create a .env file with your PRIVATE_KEY, RPC_URL and your ETHERSCAN_API_KEY.

## Dependencies

- chainlink-brownie-contracts
```
forge install smartcontractkit/chainlink-brownie-contracts@0.6.1 --no-commit
```
- foundry-devops
```
forge install https://github.com/Cyfrin/foundry-devops --no-commit
```
- solmate
```
forge install transmissions11/solmate --no-commit
```

This is a section of the Cyfrin Foundry Solidity Course.

*[⭐️ (3:04:09) | Lesson 9: Foundry Smart Contract Lottery](https://www.youtube.com/watch?v=sas02qSFZ74&t=11049s)*

## Foundry

**Foundry is a blazing fast, portable and modular toolkit for Ethereum application development written in Rust.**

Foundry consists of:

-   **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
-   **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
-   **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
-   **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

For more information on how to use this project, please refer to the [documentation](https://book.getfoundry.sh/).

## Deploy

This will default to your local node. You need to have it running in another terminal in order for it to deploy.
```
make anvil
```

## Testing

We talk about 4 test tiers in the video.

1. Unit
2. Integration
3. Forked
4. Staging

This repo we cover #1 and #3.
```
forge test
```
- Or
```
forge test --fork-url $SEPOLIA_URL
```
# Deployment to a testnet or mainnet

1. Setup environment variables

You'll want to set your `SEPOLIA_RPC_URL` and `PRIVATE_KEY` as environment variables. You can add them to a `.env` file, similar to what you see in `.env.example`.

- `PRIVATE_KEY`: The private key of your account (like from [metamask](https://metamask.io/)). **NOTE:** FOR DEVELOPMENT, PLEASE USE A KEY THAT DOESN'T HAVE ANY REAL FUNDS ASSOCIATED WITH IT.
  - You can [learn how to export it here](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key).
- `SEPOLIA_RPC_URL`: This is url of the sepolia testnet node you're working with. You can get setup with one for free from [Alchemy](https://alchemy.com/?a=673c802981)

Optionally, add your `ETHERSCAN_API_KEY` if you want to verify your contract on [Etherscan](https://etherscan.io/).

1. Get testnet ETH

Head over to [faucets.chain.link](https://faucets.chain.link/) and get some testnet ETH. You should see the ETH show up in your metamask.

2. Deploy

```
make deploy ARGS="--network sepolia"
```

This will setup a ChainlinkVRF Subscription for you. If you already have one, update it in the `scripts/HelperConfig.s.sol` file. It will also automatically add your contract as a consumer.

3. Register a Chainlink Automation Upkeep

[You can follow the documentation if you get lost.](https://docs.chain.link/chainlink-automation/compatible-contracts)

Go to [automation.chain.link](https://automation.chain.link/new) and register a new upkeep. Choose `Custom logic` as your trigger mechanism for automation. Your UI will look something like this once completed:

![Automation](./img/automation.png)

## Scripts

After deploying to a testnet or local net, you can run the scripts.

Using cast deployed locally example:

```
cast send <RAFFLE_CONTRACT_ADDRESS> "enterRaffle()" --value 0.1ether --private-key <PRIVATE_KEY> --rpc-url $SEPOLIA_RPC_URL
```

or, to create a ChainlinkVRF Subscription:

```
make createSubscription ARGS="--network sepolia"
```

## Estimate gas

You can estimate how much gas things cost by running:

```
forge snapshot
```

And you'll see an output file called `.gas-snapshot`

# Formatting

To run code formatting:

```
forge fmt
```

# Thank you!


### Contributing

If you would like to contribute to this project, please follow these steps:

1. Fork the repository.
2. Create a new branch for your changes.
3. Make your changes and commit them.
4. Push your changes to your fork.
5. Submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

# Thank you Patrick Collins!

If you appreciated this, feel free to follow Patrick Collins or donate to the following addresses:

ETH/Arbitrum/Optimism/Polygon/etc Address: 0x9680201d9c93d65a3603d2088d125e955c73BD65

[![Patrick Collins Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/PatrickAlphaC)
[![Patrick Collins YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/channel/UCn-3f8tw_E1jZvhuHatROwA)
[![Patrick Collins Linkedin](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/patrickalphac/)
[![Patrick Collins Medium](https://img.shields.io/badge/Medium-000000?style=for-the-badge&logo=medium&logoColor=white)](https://medium.com/@patrick.collins_58673/)