## What is a project in Rockside?

A rockside project is a place where you can set up specific environments to develop and test a given application that needs to interact with the ethereum blockchain through nodes.

## What is an environment?

An environment consists in a list of endpoints of different networks (such as Rinkeby, Ropsten, Mainnet) defined by the user. These endpoints can be any ethereum node under the requirement that it belongs to the network defined in the environment. Setting up different endpoints within an environment brings redundancy and can be helpful in case of failure of a node.

## How to use an environment?

You just have to reference the rpc url of the environment in your app or your project configuration, instead of pasting the rpc url of a node.
Each environment includes this url, called 'virtual rpc url'. Sending a request to a virtual rpc url will allow Rockside to dispatch the request to all the endpoints defined in the environment: a transaction which has been sent to an environment’s virtual rpc url will be sent to every nodes listed in that environment, in order to reach the ethereum pending transactions queue as fast and safely as possible.

## What is a network gate?

Network gates are existing Rockside nodes that you can link to an environment, using them as endpoints to process the requests which are sent to the virtual rpc environment url.

## What transactions will be listed in my environment?

Only transactions that were sent to the environment virtual rpc url will be listed.
If you send a transaction to environment RPC, the transaction detail will be displayed in the environment detail, not in node's details (node which corresponds to the network gate). Furthermore, deleting a network gate from an environment will have no impact on the Rockside node itself.
