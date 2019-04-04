## What is a project in Rockside?

A rockside project is a place where you can set up specific environments to develop and test a given application that needs to interact with the ethereum blockchain through nodes.

## What is an environment?

An environment consists in a list of endpoints of a same blockchain network (such as Rinkeby, Ropsten, Mainnet)  defined by the user. These endpoints can be any ethereum node under the requirement that it belongs to the network defined in the environment.

## How to use an environment?

Each environment includes a unique url called virtual rpc url that accepts rpc requests to the Blockchain. Sending a request to a virtual rpc url will allow Rockside to dispatch the request to all the endpoints defined in the environment. A transaction which request has been sent to an environment’s virtual rpc url will therefore be sent to every node listed in that environment in order to reach the ethereum pending transactions queue as fast and safely as possible.

## What is a network gate?

A network gate is the representation of a Rockside node within an environment. It allows the environment to use this Rockside node as an endpoint to process requests that will be sent to the environment virtual rpc url. The activity of a network gate is independent from the node it represents meaning that a transaction that went through a network gate via en environment will not be displayed in the Rockside node’s details. Furthermore, deleting a network gate from an environment will have no impact on the Rockside node itself.

## What transactions will be listed in my environment?

Only transactions that were sent through the environment virtual rpc url will be listed. Even if the transaction did reach a network gate representing a Rockside node, this transaction is considered as belonging to the environment and will thus only be listed in the environment’s transaction list.
