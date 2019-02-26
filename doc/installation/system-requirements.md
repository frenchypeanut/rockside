# System Requirements

## Rockside engine

Rockside-engine runs a mysql database, a laravel api, and an nginx server.

For a production deployment, 8GB RAM, i5 CPU or equivalent and 100GB hdd are recommended.


## Rockside slave

Each instance of rockside-slave can run one to many nodes. System requirements really depend of what type of nodes you need to deploy. For example, deploying an Ethereum proof-of-authority node for a consortium usage needs much less resources than a proof-of-work one.

To deploy a unique Geth mainnet full node, a 8gb RAM, 250 gb SSD, i7 or equivalent CPU are required

To deploy a consortium node, i5 CPU, 4GB Ram and 20GB SSD are recommended
