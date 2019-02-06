# Tell me more about consortium in Rockside

## I just installed Rockside. What else do I need to start a consortium ?

Did you also install rockside-slave? If you did, nothing else ! You can launch a consortium directly. Rockside will help you to manage and launch your consortium.

## How much time does it take to launch a consortium using Rockside?

Using Rockside, it could take less than five minutes to have a consortium up and running.

## One organisation of the consortium doesn’t want to use Rockside. Is it still possible to add it to the consortium ?

Absolutely. Rockside gives you deployment facilities, transaction monitoring features and a lot more, but doesn’t create any dependency with the tool itself. Consortiums can be joined by any compatible client. Just export the genesis file from the Rockside web interface and give it to the organization which needs to run the consortium.


## How to deploy a real multi-companies consortium production network, within different cloud-provider or on premises, using different rockside instances ?

The initiator of the consortium have to define members through the rockside web interface and to export Rockside consortium file.  Each member of the consortium has to install Rockside on its own instance, import Rockside Consortium File and validate. That’s all.


## I just want to try the Rockside consortium manager locally. Do I have to launch Rockside multiple times on my computer, to try to run a consortium ?

No ! You you can add as many members as you want on the consortium manager page, and launch it directly from your unique Rockside instance. It’s a good way to experiment the consortium experience really quickly.

## I created and launched a consortium locally using Rockside, with 4 organization members. What did Rockside do exactly ?

While you created members within Rockside, one node per member has been created, and one key for each one has been generated. Each key is encrypted with a randomly generated password, which has been  written in the pass.txt file inside the node’s folder. This password will be used to unlock an account for transactions validation. This is the current Rockside alpha version behaviour, but it will surely change in the next releases.  Then, a genesis file as been created, containing the 4 members, nodes have been initialized with it and 4 ethereum clients has been launched. Rockside is in charge of making them discover each other via peer to peer and launch the blockchain network. A RPC URL is also created for each peer.

## Is it possible to export the genesis file of my consortium?

Yes, Rockside provides the possibility to export the genesis file, with a simple click from the user interface. You can export 2 kinds of file : the genesis file if you don’t use Rockside


## Is it possible to dynamically add or remove a validator node from a consortium which has already been launched ?

A consortium on Ethereum provides a voting mechanism which gives the possibility to add or remove new validators. During the vote, each validator can specify an account they want to add to the consortium. If half of the validators vote for the same account, this one is added to the validator set. You can execute voting commands directly on your Rockside slave validator node instances, via command line. It will be soon integrated to Rockside’s user interface !



## Which consensus are currently available within Rockside, in order to create consortiums ?

PoA (Proof of Authority) is the only consensus algorithm supported for the moment.


## I don’t want to use Rockside anymore but I want to keep my consortium network up and running, is it possible ?

Of course, you can uninstall Rockside and keep your nodes up and running. You can also export files relative to your consortium and launch it with any compatible Ethereum client.

## Does Rockside have access to my private keys ?


Keys are stored in your own rockside slave instance, they are never exposed to the outside world, neither to rockside engine.


## How can I connect to my consortium using metamask ?

You have to paste the RPC URL of your consortium node in the Custom RPC URL of Metamask and voilà !

@
## I just installed Rockside. What else do I need to start a consortium ?

Did you also install rockside-slave? If you did, nothing else ! You can launch a consortium directly. Rockside will help you to manage and launch your consortium.

## How much time does it take to launch a consortium using Rockside?

Using Rockside, it could take less than five minutes to have a consortium up and running.

## One organisation of the consortium doesn’t want to use Rockside. Is it still possible to add it to the consortium ?

Absolutely. Rockside gives you deployment facilities, transaction monitoring features and a lot more, but doesn’t create any dependency with the tool itself. Consortiums can be joined by any compatible client. Just export the genesis file from the Rockside web interface and give it to the organization which needs to run the consortium.


## How to deploy a real multi-companies consortium production network, within different cloud-provider or on premises, using different rockside instances ?

The initiator of the consortium have to define members through the rockside web interface and to export Rockside consortium file.  Each member of the consortium has to install Rockside on its own instance, import Rockside Consortium File and validate. That’s all.


## I just want to try the Rockside consortium manager locally. Do I have to launch Rockside multiple times on my computer, to try to run a consortium ?

No ! You you can add as many members as you want on the consortium manager page, and launch it directly from your unique Rockside instance. It’s a good way to experiment the consortium experience really quickly.

## I created and launched a consortium locally using Rockside, with 4 organization members. What did Rockside do exactly ?

While you created members within Rockside, one node per member has been created, and one key for each one has been generated. Each key is encrypted with a randomly generated password, which has been  written in the pass.txt file inside the node’s folder. This password will be used to unlock an account for transactions validation. This is the current Rockside alpha version behaviour, but it will surely change in the next releases.  Then, a genesis file as been created, containing the 4 members, nodes have been initialized with it and 4 ethereum clients has been launched. Rockside is in charge of making them discover each other via peer to peer and launch the blockchain network. A RPC URL is also created for each peer.

## Is it possible to export the genesis file of my consortium?

Yes, Rockside provides the possibility to export the genesis file, with a simple click from the user interface. You can export 2 kinds of file : the genesis file if you don’t use Rockside


## Is it possible to dynamically add or remove a validator node from a consortium which has already been launched ?

A consortium on Ethereum provides a voting mechanism which gives the possibility to add or remove new validators. During the vote, each validator can specify an account they want to add to the consortium. If half of the validators vote for the same account, this one is added to the validator set. You can execute voting commands directly on your Rockside slave validator node instances, via command line. It will be soon integrated to Rockside’s user interface !



## Which consensus are currently available within Rockside, in order to create consortiums ?

PoA (Proof of Authority) is the only consensus algorithm supported for the moment.


## I don’t want to use Rockside anymore but I want to keep my consortium network up and running, is it possible ?

Of course, you can uninstall Rockside and keep your nodes up and running. You can also export files relative to your consortium and launch it with any compatible Ethereum client.

## Does Rockside have access to my private keys ?


Keys are stored in your own rockside slave instance, they are never exposed to the outside world, neither to rockside engine.


## How can I connect to my consortium using metamask ?

You have to paste the RPC URL of your consortium node in the Custom RPC URL of Metamask and voilà !

# Troubleshooting

## Each time a register a slave, it's override the previous registered slave

You are probably facing this issue because you duplicated one of your slave.

Slaves have a unique identifier that the engine uses to differentiate them. When a slave is duplicated, it does not change the unique id for now.

The simple way to solve this is to erase the original unique id

```sh
sudo rm /root/.rockside/slave.uid
```

Then restart the slave, it will generate a new one automatically.

```sh
sudo rockside-slave --engine.key YOUR_ENGINE_KEY --engine.url YOUR_ENGINE_URL
```

# Networking

Typical network topology of a consortium is composed of:
- one server which runs rockside-engine
- several servers which run rockside-slave. On each rockside-slave instance can run one or more nodes

## Rockside engine

The default ports specified during the install of rockside-engine are **80** and **443**. These one has to be opened on your server.

## Rockside-slave

Rockside-slave server listens by default on the port **3000**.
You have to open this port on each running slave, in order to be able to be reached by rockside-engine.

Also, on each slave run one or more nodes. Each Ethereum node needs to communicate with other nodes.
By default, the first node instanciated by rockside-slave listen on the port **30303**. The second one on **30304**, and so on. So you have to open these ports in orderer Ethereum nodes to communicate with other nodes