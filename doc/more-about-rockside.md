# Tell me more about Rockside

## Which chains and implementations are supported?

 - Mainnet (geth/parity)
 - Ropsten (geth/parity)
 - Rinkeby (geth/parity)
 - Tobalaba (parity)

_(Pantheon Ethereum client integration in progress !)_

## Why use only Ethereum as a starting point?

Because we believe in the potential of this protocol. Ethereum is popular, public, open-source and robust. Furthermore, it fits to many corporate needs.

## Is it risky to send transaction to Rockside's nodes during alpha version?

Before sending transaction to **your own** Rockside node(s), you need to create and sign them offline. Rockside have no visibility of your private key. Finally the question is : is Blockchain protocol secure ? Yes, by design ;)

## What is the difference with services offering remote nodes ?

If the remote service is malicious or gets hacked, this trusted third party can censor your transactions, show you fake data, collect data on your IP, …
Rockside is different because you host your own nodes and you keep control over your interactions with Blockchain networks.


## <a name="artefacts"></a>I just installed Rockside. What has been done on my system ?

Rockside is shipped with two core components, Rockside Engine and Rockside Slave, you have to install separatly.

At the end of the installation of rockside Engine, you will have:

- a new .rockside folder containing rockside engine persistant stuff which has been created. By default this folder is created in the home directory of the user who initiated the command (usually ~/.rockside on macOS or /root/.rockside on Linux )
- 3 running docker containers on your system. Rockside engine is a combination of technologies working together and Rockside ship it under docker containers. Rockside Engine runs a mysql database, a laravel api, and an nginx server.

At the launch of Rockside Slave, you will have:
- A running Rockside slave instance of the binary which has been installed in /usr/local/bin/rockside-slave
- A running container per node instanciated through Rockside interface
- A persistent folder where will be stored you blockchain datas.

## I run a rockside instance. I noticed than anybody could create an account on Rockside interface

Indeed ! The EthCC community release don't give the possibility to restrict the signup only to whitelisted users.