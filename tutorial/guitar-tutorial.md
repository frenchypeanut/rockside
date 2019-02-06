# Your first decentralized applications (DApp) on Ethereum With Rockside

In this tutorial we will learn how to:
* Host a Blockchain node with Rockside
* Configure Metamask and use your node
* Deploy a smart contract with Remix
* Interact with your smart contract in rockside guitar Dapp
* Monitor transaction on Rockside

![home-rockside-guitar-tutorial](https://github.com/blockchain-studio/rockside/blob/master/home-rockside-guitar-tutorial.png)

## I - Install Rockside environment

### Installation guide
Follow instructions of the [installation guide](https://github.com/blockchain-studio/rockside/wiki/Installation-guide).

### Create your node
Once Rockside is installed on your environment, go to "node creation form", select the Ropsten network and choose Fast for synchronization mode.

![rockside new node](https://github.com/blockchain-studio/rockside/blob/master/rockside-new-node.png)

**Get ready for a long break ☕**

*A light node would have been better for this tutorial but we have not completed the integration of Parity in our Alpha version (works on my machine ;)). At this point, owning node has many benefits, but it involves a constraint: Time. Copying and synchronizing with the Ropsten Blockchain takes time, even if it is difficult to estimate, plan 4 to 8 hours.*


## II - Configure Metamask to use this node

* Install the Metamask browser extension: https://metamask.io
* use a faucet to collect Ethers on the Ethereum Ropsten Test Network: https://faucet.metamask.io
* Configure Metamask to use your Rockside node

Go to Rockside, copy the URL of your node:

![rockside node list](https://github.com/blockchain-studio/rockside/blob/master/rockside-nodes-list.jpg)

Open your Metamask extension and add a new RPC URL.

![metamask settings](https://github.com/blockchain-studio/rockside/blob/master/metamask-settings.jpg)

## III - Write your Smartcontract and deploy it on your Rockside Node

For this tutorial we use an online IDE called remix: https://remix.ethereum.org

Check in the **Run** tab that Remix is using the Web3 API injected by your Metamask.

![remix injected web3](https://github.com/blockchain-studio/rockside/blob/master/remix-injected-web3.png)

Copy the smart contract code below.

```solidity
pragma solidity >=0.4.22 <0.6.0;

contract RocksideFlag {

    mapping (address => bool) public captured;

    event LogCaptured(address indexed whoAddress, bytes32 whoName);

    function captureTheFlag(bytes32 name) public {
        captured[msg.sender] = true;
        emit LogCaptured(msg.sender, name);
    }
}
```

**Compile** (if it's not automatic) and **Deploy** the contract.

![deploy smartcontract](https://github.com/blockchain-studio/rockside/blob/master/remix-deploy-contract.jpg)

Once the transaction confirmed, save the address of the newly deployed contract, we will need it later in this tutorial.

![adr of deployed sm](https://github.com/blockchain-studio/rockside/blob/master/remix-sm-adr.jpg)

## IV - Bookmark the address of the smart contract in Rockside

With Rockside you can mark an address to add information. Let's do that for our smart contract.

First open your rockside UI instance and go to the **Address Book** page.

Then fill the form with your previously deployed smart contract address, a label (ex: Rockside Guitar Contract) and an image ([this one](https://www.freepik.com/free-icon/bass-guitar_855554.htm) for example).

![](https://github.com/blockchain-studio/rockside/blob/master/rockside-add-bookmarked-adr.png)

Tada !!

![](https://github.com/blockchain-studio/rockside/blob/master/rockside-list-bookmarked-addresses.png)

## V - Code the dApp that will interact with your contract

Download or Clone the source code of the **rockside guitar dapp tutorial** project
> https://github.com/blockchain-studio/rockside-guitar-dapp-tutorial

In the src/index.js file Line 4, enter the address of your contract.

```js
  // file index.js, Line 4
  contractAddress: function() {
    return "enter your contract address here";
  },
```

Open a terminal, go to the root of the project and type the commands:

```
npm install
npm run dev
```
The application should open in your default browser.

## VI - Capture the Rockside Guitare
![capture-guitare](https://github.com/blockchain-studio/rockside/blob/master/capture-guitare.png)

## VII - Check your transaction in Rockside
Go back to Rockside, your transaction appears and it is decorated with the Bookmarked Address
![transaction-in-rockside](https://github.com/blockchain-studio/rockside/blob/master/transaction-in-rockside.png)

## Conclusion
With this tutorial, you've seen two different uses of your nodes: As developers, to deploy your smartcontract and as a user of your Dapp, to interact with the Smart contract. Once Rockside installed in your infrastructure, using and managing access to other Blockchain networks is really simple and fast.

The LCP version of Rockside focuses on configuring Rockside services in self-hosted environnement. Private Network, detailed monitoring and access management features will be added very soon!
### Stay tuned ! 🚀

