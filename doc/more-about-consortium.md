# Tell me more about consortium in Rockside

### How much time does it take to launch a consortium using Rockside?

Using Rockside, it could take less than five minutes to have a consortium up and running.

### Which consensus are currently available within Rockside, in order to create consortiums ?

PoA (Proof of Authority) is the only consensus algorithm supported for the moment.

### How can I get Ether to use on my consortium?

When your consortium is in setup phase, before you start it, you can define a prefunded account.
This account will receive a large amount of ether when the consortium is in place.


### How can I connect to my consortium using metamask ?

You have to paste the RPC URL of your consortium node in the Custom RPC URL of Metamask and voilà !


### Does Rockside have access to my private keys ?

Keys are stored in your own rockside slave instance, they are never exposed to the outside world, neither to rockside engine.

### How can I access the account that was generated for validating transactions on my consortium?
 
Connect to the server were your account was generated.  All informations about your node are stored in **SLAVE_DATADIR/node/geth-CONSORTIUM_NAME-MEMBER_NAME/data** (by default SLAVE_DATADIR is ~/.rockside/). 
The **pass.txt** contains the password to access your account. Your account is present on the keystore folder.

### How to deploy a real multi-companies consortium production network, within different cloud-provider or on premises, using different rockside instances ?

The initiator of the consortium have to define members through the rockside web interface and to export Rockside consortium file.  Each member of the consortium has to install Rockside on its own instance, import Rockside Consortium File and validate. That’s all.

### One organisation of the consortium doesn’t want to use Rockside. Is it still possible to add it to the consortium ?

Absolutely. Rockside gives you deployment facilities, transaction monitoring features and a lot more, but doesn’t create any dependency with the tool itself. Consortiums can be joined by any compatible client. Just export the genesis file from the Rockside web interface and give it to the organization which needs to run the consortium.

### I just want to try the Rockside consortium manager locally. Do I have to launch Rockside multiple times on my computer, to try to run a consortium ?

No ! You you can add as many members as you want on the consortium manager page, and launch it directly from your unique Rockside instance. It’s a good way to experiment the consortium experience really quickly.

### I created and launched a consortium locally using Rockside, with 4 organization members. What did Rockside do exactly ?

While you created members within Rockside, one node per member has been created, and one key for each one has been generated. Each key is encrypted with a randomly generated password, which has been  written in the pass.txt file inside the node’s folder. This password will be used to unlock an account for transactions validation. This is the current Rockside alpha version behaviour, but it will surely change in the next releases.  Then, a genesis file as been created, containing the 4 members, nodes have been initialized with it and 4 ethereum clients has been launched. Rockside is in charge of making them discover each other via peer to peer and launch the blockchain network. A RPC URL is also created for each peer.

### Is it possible to export the genesis file of my consortium?

Yes, Rockside provides the possibility to export the genesis file, with a simple click from the user interface. You can export 2 kinds of file : the genesis file if you don’t use Rockside


### Is it possible to dynamically add or remove a validator node from a consortium which has already been launched ?

A consortium on Ethereum provides a voting mechanism which gives the possibility to add or remove new validators. During the vote, each validator can specify an account they want to add to the consortium. If half of the validators vote for the same account, this one is added to the validator set. You can execute voting commands directly on your Rockside slave validator node instances, via command line. It will be soon integrated to Rockside’s user interface !


### I don’t want to use Rockside anymore but I want to keep my consortium network up and running, is it possible ?

Of course, you can uninstall Rockside and keep your nodes up and running. You can also export files relative to your consortium and launch it with any compatible Ethereum client.
