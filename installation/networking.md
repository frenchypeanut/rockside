# How to configure network ports

Typical network topology of a consortium is composed of:
- one server which runs rockside-engine
- several servers which run rockside-slave. On each rockside-slave instance can run one or more nodes

## Rockside engine

The default ports specified during the install of rockside-engine are **80** and **443**. These one has to be opened on your server.

## Rockside-slave

Rockside-slave server listens by default on the port **3000**.
You have to open this port on each running slave, in order to be able to be reached by rockside-engine.

Also, on each slave run one or more nodes. Each Ethereum node needs to communicate with other nodes.
By default, the first node instanciated by rockside-slave listen on the port **30303**. The second one on **30304**, and so on. So you have to open these ports in orderer Ethereum nodes to communicate with other nodes.
If you plan to manage ten nodes on your slave, you can open ports from **30303** to **30313**.