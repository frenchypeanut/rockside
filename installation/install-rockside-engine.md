# How to install Rockside Engine on Linux or OS X (LCP Release)
First, you need to install Rockside Engine. It allows you to manage your blockchain projects by inviting users, running blockchain nodes, displaying your node transactions, providing node's RPC endpoint ...
[Learn more about Rockside architecture](https://github.com/blockchain-studio/rockside/wiki/FAQ#what-is-rockside-technical-architecture)


### Install Docker Engine

Rockside Engine requires the Docker Engine to run. Public Rockside images will be pulled by installation scripts from the public official Docker hub registry.

On OS X, docker compose come with the docker installation.

For linux, follow Docker installation instructions for your platform at https://docs.docker.com/engine/installation/#supported-platforms.


### Install Docker Compose

With the Docker Engine installed you can now install Docker Compose which is also required by Rockside Engine: https://docs.docker.com/compose/install.

### Operating systems

Rockside can be installed on Linux and MacOS.
**If you are on linux please prefix all the following commands with 'sudo'**


### Download Rockside installer

The following command will ask you to enter your **root password** to install Rockside:

```
curl -sSL http://releases.rockside.io/cli/get.sh | sh
```


### Run Rockside Engine install

```
rockside engine install
```

Rockside engine install will ask you:

```
Server Hostname:localhost
HTTP Server Port: 80
HTTPS Server Port: 443
```
If you want Rockside Engine to be available on your **local network or internet**, see the [hostname options](advanced-setup.md#hostname_options)

At the end of installation, Rockside Engine is running. If you want to understand exactly what is done on your system, please read the [FAQ](../more-about-rockside.md#artefacts)

⚠️Rockside Engine use a self-signed certificate for SSL. You may see a warning about this upon accessing your workspace for the first time. There’s nothing to worry about: you can safely proceed to the website.

You also can use a more [advanced setup](./advanced-setup.md)

### Run Rockside Slave

If you want to try Rockside on your local machine, you can launch Rockside Slave directly after Rockside Engine installation

```
rockside slave start
```

This command download and install Rockside slave, and register it to the local instance of Rockside engine. More infos [here](../more-about-rockside.md#artefacts)

This way of running Rockside Slave is super-convenient for local testing purpose, or for a single node deployment.
Prefer manual [install](https://github.com/blockchain-studio/rockside/blob/Ethcc-release/installation/install-rockside-slave.md) if you want to run multiple instances of Rockside Slave on remote servers, for example if you node to maintain multiple different nodes.


### Create an account and sign-up on Rockside Engine

- Open a browser and fill your Rockside Engine Url
- Click on sign-up
- Fill the form
- You can now sign-in on Rockside Engine. Rockside engine comes with default login for convenience. Default user credentials are 'default_user@rockside.io' and 'password'. ⚠️ Please change password of the default user while connected ⚠️


### Uninstall Rockside Engine

```
rockside engine uninstall
```

This command will stop Rockside Engine instance and delete all the files relative to instance on your filesystem. If you also started rockside Slave with the rockside installer (command mentioned previously on this page), the useful files inherent to Rockside Slave will also be deleted, including blockchain data. If you need persistent data folder for your blockchain data please follow [manual installation](./install-rockside-slave.md) of rockside Slave with a custom data directory.