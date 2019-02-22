# What is Rockside technical architecture?

## Rockside-engine (Hosted on private cloud or on-premise)

Rockside-engine is the entry point of the service. It is accessible via a graphical interface in a web browser. It's a kind of super proxy that simplifies the orchestration of Blockchain nodes. Like the whole Rockside solution, this proxy is self hosted. It means that you have to deploy it on your own servers.

## Rockside-slave (Hosted on private cloud or on-premise)

A slave is controlled by a Rockside Engine. It’s in charge of running nodes on a server. You can install it on the same server as the engine, but we recommend that you install it on a dedicated server. Slave requires a lot of space on the hard drive and CPU to synchronize with the blockchain.

![Image of Rockside Alpha Architecture](https://raw.githubusercontent.com/blockchain-studio/rockside/master/doc/rockside-lcp-architecture.jpg)

## Why separate engine and nodes in different layers ?
The main idea is to separate responsibilities.

**engine**

The engine exposes a REST API and a UI. It manages authentication, services, storage and communication with nodes overs slaves.

**slave**

Slave is an abstraction layer above nodes.  For example your organization  can deploy several slaves dispatched geographically in the world operating different nodes.  This slave will be orchestrated by a single engine.

With this architecture, your organization is able to manage different level of resources depending on the constraints of each Blockchain project (Test / Development, high availability, regulation constraints, ...). Plus, the architecture is super scalable so you can run as many different nodes as you want.