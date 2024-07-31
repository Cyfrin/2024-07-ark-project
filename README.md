# ArkProject NFT Bridge 

### Prize Pool

- Total Pool - $60,000
- H/M -  $50,000
- Low - $5,500
- Community Judging -  $4,500


Starts: July 31, 2024 Noon UTC

Ends: August 28, 2024 Noon UTC

- nSLOC: 2301

[//]: # (contest-details-open)

## About the Project
The ArkProject NFT Bridge allows users to bridge NFTs (ERC-721) between Ethereum (L1) and Starknet (L2).

The ArkProject NFT Bridge currently supports the bridging of the Everai NFT collection exclusively. Holders of Everai NFTs can seamlessly transfer their assets from Ethereum (L1) to Starknet (L2) and vice versa, pioneering the integration of NFTs into the next generation of blockchain technology.

The ArkProject NFT Bridge uses the [Starknet (L1↔L2) messaging](https://docs.starknet.io/architecture-and-concepts/network-architecture/messaging-mechanism/) protocol for ERC-721 bridging smart contracts. 

[Website](https://bridge.arkproject.dev/)

[Twitter](https://x.com/ArkProjectNFTs)

[GitHub](https://github.com/ArkProjectNFTs/bridge)

## Actors

Actors:
- Starknet messaging protocol: ensure message exchange between Ethereum and Starknet.
- Bridge admin: can enable/disable bridge, enable/disable global whitelist, enable/disable whitelist for a given collection and set L1L2 mapping.
- User: can bridge a NFT from Ethereum to Starknet or from Starknet to Ethereum.

Please note that Users need to [`approve`](https://docs.openzeppelin.com/contracts/5.x/api/token/erc721#IERC721-approve-address-uint256-) bridge contract to transfer the owned NFT on their behalf.

[//]: # (contest-details-close)

[//]: # (scope-open)

## Scope (contracts)

### Ethereum
The following contracts are in scope
```js
ethereum/src/
├── Bridge.sol
├── Escrow.sol
├── IStarklaneEvent.sol
├── IStarklane.sol
├── Messaging.sol
├── Protocol.sol
├── sn
│   └── Cairo.sol
├── State.sol
├── token
│   ├── CollectionManager.sol
│   ├── Deployer.sol
│   └── TokenUtil.sol
└── UUPSProxied.sol
```

The following contracts are **NOT** in scope
```js
ethereum/src/
├── sn
│   ├── IStarknetMessagingLocal.sol
│   └── StarknetMessagingLocal.sol
├── TestMessaging.sol
└── token
    ├── ERC1155Bridgeable.sol
    ├── ERC721Bridgeable.sol
    ├── IERC1155Bridgeable.sol
    └── IERC721Bridgeable.sol
```

### Starknet
The following contracts are in scope
```js
starknet/src/
├── bridge.cairo
├── byte_array_extra.cairo
├── interfaces.cairo
├── lib.cairo
├── request.cairo
├── token
│   ├── collection_manager.cairo
│   ├── erc721_bridgeable.cairo
│   └── interfaces.cairo
└── token.cairo
```

The following contracts are **NOT** in scope
```js
starknet/src/
├── tests
│   └── bridge_t.cairo
└── tests.cairo
```


## Compatibilities

Since ArkProject NFT Bridge uses the [Starknet (L1↔L2) messaging](https://docs.starknet.io/architecture-and-concepts/network-architecture/messaging-mechanism/) only Ethereum and Starknet blockchains are supported.

```
Compatibilities:
  Blockchains:
      - Ethereum/Starknet
  Tokens:
      - [ERC721](www.tokenstandard.com)
```

On mainnet, only the following collections are whitelisted:
- Ethereum: [Everai](https://etherscan.io/token/0x9a38dec0590abc8c883d72e52391090e948ddf12)
- Starknet: [Everai](https://starkscan.co/nft-contract/0x02acee8c430f62333cf0e0e7a94b2347b5513b4c25f699461dd8d7b23c072478)

[//]: # (scope-close)

[//]: # (getting-started-open)

## Setup

## Clone the Repo:
```bash
git clone --recursive https://github.com/Cyfrin/2024-07-ark-project.git
```

Unit tests for smart contracts are available, using [foundry](https://book.getfoundry.sh/) and [starknet foundry](https://foundry-rs.github.io/starknet-foundry/index.html)

### Ethereum tests:
```bash
cd apps/blockchain/ethereum
forge test
```

### Starknet tests:
```bash
cd apps/blockchain/starknet
snforge test
```

[A guide for a local setup](https://github.com/ArkProjectNFTs/bridge/blob/main/apps/blockchain/local_setup.md) of ArkProject NFT Bridge is available.

[//]: # (getting-started-close)

[//]: # (known-issues-open)

## Known Issues

An [audit is available](https://github.com/ArkProjectNFTs/bridge/blob/main/docs/audit/Audit-Cairo_Security_Clan-Updated.pdf) in github repository.

Known Issues:
- Due to a payload size limit in Starknet L1<->L2 messaging protocol if user try to transfert a large number of NFTs, message will not to transmit and so NFT will be locked in bridge contract.

- Bridge admin is a trusted role.

[//]: # (known-issues-close)
