---
description: >-
  The official JavaScript client for implementing Snapshot's functionality in
  other apps.
---

# Snapshot.js

## **Overview**

**`Snapshot.js`** is an open source JavaScript client which comes with the core functions of the Snapshot's off-chain voting system. It was designed to work both in the browser and with `Node.js`.

{% embed url="https://github.com/snapshot-labs/snapshot.js" %}

## Get started

### **Installation**

**Node.js**

To install Snapshot.js on Node.js, open your terminal and run:

```shell
npm i @snapshot-labs/snapshot.js
```

**Browser**

You can create an index.html file and include Snapshot.js with:

```html
<script src="https://cdn.jsdelivr.net/npm/@snapshot-labs/snapshot.js"></script>
```

### Development

**Install dependencies**

```shell
yarn
```

**Build package**

```shell
yarn build
```

## Usage

#### Base features

#### Init client

```javascript
import snapshot from '@snapshot-labs/snapshot.js';

const hub = 'https://hub.snapshot.org'; // or https://testnet.snapshot.org for testnet
const client = new snapshot.Client712(hub);
```

#### Cast a vote

```javascript
import { Web3Provider } from '@ethersproject/providers';

const web3 = new Web3Provider(window.ethereum);
const [account] = await web3.listAccounts();

const receipt = await client.vote(web3, account, {
  space: 'yam.eth',
  proposal: '0x21ea31e896ec5b5a49a3653e51e787ee834aaf953263144ab936ed756f36609f',
  type: 'single-choice',
  choice: 1,
  reason: 'Choice 1 make lot of sense',
  app: 'my-app'
});
```

#### Create proposal

```javascript
import { Web3Provider } from '@ethersproject/providers';

const web3 = new Web3Provider(window.ethereum);
const [account] = await web3.listAccounts();

const receipt = await client.proposal(web3, account, {
  space: 'yam.eth',
  type: 'single-choice', // define the voting system
  title: 'Test proposal using Snapshot.js',
  body: 'This is the content of the proposal',
  choices: ['Alice', 'Bob', 'Carol'],
  start: 1636984800,
  end: 1637244000,
  snapshot: 13620822,
  network: '1',
  plugins: JSON.stringify({}),
  app: 'my-app' // provide the name of your project which is using this snapshot.js integration
});
```

#### **Create or edit a space**

```javascript
import { Web3Provider } from '@ethersproject/providers';

const web3 = new Web3Provider(window.ethereum);
const [account] = await web3.listAccounts();

const receipt = await client.space(web3, account, {
  "space":"pistachiodao.eth",
  "settings":{
    "name":"pistachiodao.eth",
    "network":"1",
    "symbol":"XYZ",
    "private":false,
    "members":[],
    "admins":[],
    "categories":[
      "social",
      "media"
    ],
    "plugins":{
      "hal":{}
    },
    "children":[],
    "voting":{
      "hideAbstain":false
    },
    "strategies":[{
      "name":"ticket",
      "network":"1",
      "params":{"symbol":"TICKET"}
    }], // provide up to 8 strategies with their configuration
    "validation":{
      "name":"basic",
      "params":{}
    },
    "voteValidation":{
      "name":"any",
      "params":{}
    },
    "filters":{
      "minScore":0,
      "onlyMembers":false
    },
    "treasuries":[] // provide the organization's treasury account(s)
    }
});
```

#### Join a space

```javascript
import { Web3Provider } from '@ethersproject/providers';

const web3 = new Web3Provider(window.ethereum);
const [account] = await web3.listAccounts();

const receipt = await client.follow(web3, account, {
  "name":"pistachiodao.eth"
});
```

### **Utils**

#### **getScores**

Calculate voting power for a list of voters.

```javascript
import snapshot from '@snapshot-labs/snapshot.js';

const space = 'yam.eth';
const strategies = [
  {
    name: 'erc20-balance-of',
    params: {
      address: '0x6B175474E89094C44Da98b954EedeAC495271d0F',
      symbol: 'DAI',
      decimals: 18
    }
  }
];
const network = '1';
const voters = [
  '0xa478c2975ab1ea89e8196811f51a7b7ade33eb11',
  '0xeF8305E140ac520225DAf050e2f71d5fBcC543e7',
  '0x1E1A51E25f2816335cA436D65e9Af7694BE232ad'
];
const blockNumber = 11437846;

snapshot.utils.getScores(
  space,
  strategies,
  network,
  voters,
  blockNumber
).then(scores => {
  console.log('Scores', scores);
});
```

#### **getProvider**

Return a Ethers.js JsonRPCProvider connected to an archive node.

```javascript
import snapshot from '@snapshot-labs/snapshot.js';

const network = '1';
const provider = snapshot.utils.getProvider(network);
```

