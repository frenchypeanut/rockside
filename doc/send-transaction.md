# How to send a transaction to my Node?

## Example using CURL

This is an example of JSON-RPC Methods in command line using CURL

    $ curl -X POST
    -H "Content-Type: application/json"
    --data '{"jsonrpc": "2.0", "method": "eth_blockNumber", "id": 1,
    "params": []}'
    "https://{rocksideHost}/api/nodes/rpc/{token}"

Read more informations about [JSON-RPC](https://github.com/ethereum/wiki/wiki/JSON-RPC)

## Are all RPC methods accessible from my Node?

The open RPC api open on your Node are `eth`, `web3`, `txpool`, `net` on `geth` and `eth`, `web3`, `net`, `parity` on `parity`.

Moreover we block `eth_coinbase`, `eth_accounts`, `eth_sign`, `eth_sendTransaction` due to their reliance on local Node's accounts.

## How to use Rockside Node in your Truffle project ?

During the development of a Dapp, there can be many stages before release project to the users (production environment). In development environment, the maturity of tools is quite good, thanks to [Truffle](https://truffleframework.com) in particular. As soon the developer want to test his application on a public  network or a private consortium, new problems can happen. How to obtain Ether, how to deploy the smart contract, how to debug transactions… Rockside provides helpers to support the developers to deploy their project on public network (test and production) or to easily deploy corsortiums.

### Generate truffle networks configuration file
In the Rockside graphical interface, a button "use with truffle" is available. The system generates a [configuration file](https://truffleframework.com/docs/truffle/reference/configuration#networks) that can be directly integrated into your Truffle project. This file is used for deployment target during migrations.

### HDWalletProvider and Mnemonic
A mnemonic is a pattern of letters, words, or associations which allows you to easily remember information. This system gives a human readable format of words to back-up your wallet for recovery. You can generate a mnemonic using [Metamask Seed](https://metamask.zendesk.com/hc/en-us/articles/360015489431-Exporting-Your-Seed-Phrase) or [hardware wallet](https://www.ledger.com/) or [online mnemonic](https://iancoleman.io/bip39/) generator. **Mnemonic = private keys = your identity = your wallets = your tokens = 😱! We highly recommend keep your mnemonic secret. Never pass it on to anyone and keep it as safe as possible.**

## Can I use my node with websocket

The current release does not allow websocket connection to nodes deployed with Rockside. To query a Rockside node, you can use RPC requests through the URLs displayed on the node details page.
