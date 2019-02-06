# How to install Rockside on Linux or OS X (LCP Release)
First, you need to install Rockside Engine. It allows you to manage your blockchain projects by inviting users, running blockchain nodes, displaying your node transactions, providing node's RPC endpoint ...
[Learn more about Rockside architecture](https://github.com/blockchain-studio/rockside/wiki/FAQ#what-is-rockside-technical-architecture)


### <a name="requirements"></a>Requirements
* Be part of the [Launch Customer Program](https://github.com/blockchain-studio/rockside/wiki#launch-customer-program-lcp)
* Have access to our Docker Hub image repository. For that you must contact us to request an access at tech@rockside.io

### Install Docker Engine

Rockside Engine requires the Docker Engine to run.

On OS X, docker compose come with the docker installation.

For linux, follow Docker installation instructions for your platform at https://docs.docker.com/engine/installation/#supported-platforms.


### Install Docker Compose

With the Docker Engine installed you can now install Docker Compose which is also required by Rockside Engine: https://docs.docker.com/compose/install.


### Login to docker

Login to docker with an account that has permission to access our Docker Hub image repository. (See [requirements](#requirements))

If you are **on linux** you should log using super user right:

```
sudo docker login -u=LOGIN
```

On **OS X** just run:

```
docker login -u=LOGIN
```

### Download Rockside installer

The following command will ask you to enter your **root password** to install Rockside:

```
curl -sSL http://releases.rockside.io/cli/get.sh | sh
```


### Run Rockside Engine install

If you are **on linux** you should run the installer with super user right:

```
sudo rockside engine install
```

On **OS X** just run:

```
rockside engine install
```

Rockside engine install will ask you:

```
Server Hostname:localhost
HTTP Server Port: 80
HTTPS Server Port: 443
```
If you want Rockside Engine to be available on your **local network or internet**, see the [hostame options](#hostname_options)

At the end of installation, Rockside Engine is running.

⚠️Rockside Engine use a self-signed certificate for SSL. You may see a warning about this upon accessing your workspace for the first time. There’s nothing to worry about: you can safely proceed to the website.

### Create an account and sign-up on Rockside Engine

- Open a browser and fill your Rockside Engine Url
- Click on sign-up
- Fill the form
- You can now sign-in on Rockside Engine


## <a name="install_rockside_slave"></a> Install Rockside Slave
Now, you have to install a Rockside Slave. A slave is controlled by a Rockside Engine. It's in charge of running nodes on a server. You can install it on the same server as the engine, but we recommend that you install it on a dedicated server. Slave requires a lot of space on the hard drive and CPU to synchronize with the blockchain.


### Requirements

Rockside Slave requires the Docker Engine to run. Follow Docker installation instructions for your platform at https://docs.docker.com/engine/installation/#supported-platforms.

If you install the Slave on the save server as the Engine, Docker engine should be already installed.

### Download Rockside Slave

Download Rockside Slave executable to the server you want to install it.

The following command will ask you to enter **your root password** to install Rockside:
```
curl -sSL http://releases.rockside.io/slave/get.sh | sh
```

### Get the registration token

Login on Rockside Engine, go to the install slave page to get the **slave registration token**:

- On the top right click on your username, then select "slaves".
- On the slaves page, click on 'add slave'

You will need this registration token to connect the slave to the engine.

### Register the slave

On server where you downloaded Rockside slave executable,

If you are **on linux** you should run Rockside Slave with super user right:

```
sudo rockside-slave --engine.key SLAVE_REGISTRATION_TOKEN --engine.url ROCKSIDE_ENGINE_URL:PORT
```

On **OS X** just run:
```
rockside-slave --engine.key SLAVE_REGISTRATION_TOKEN --engine.url ROCKSIDE_ENGINE_URL:PORT
```

**Tips:** To run Rockside Slave in background, add "&" at the end of the command. When it's running in background, simply type fg to bring it to foreground.

### Create a Node

On Rockside Engine go to the node creation page:

- Click on rockside logo on the top left, to arrive on your group's blockchain nodes.
- Click on 'create one'.

Follows instructions

## Congratulations!

You’ve just successfully installed and configured Rockside and setup your first node.

Good luck in the blockchain world!🤠

## <a name="advanced_setup"></a>Advanced setup

### Use a custom data dir for Rockside Engine installation
By default Rockside Engine installs in your HOME directory. It create a folder at this path "~/.rockside/engine". This folder contains all settings required by the application.  To specify a custom datadir use:

```
rockside engine install --datadir=/ssd/rockside-engine
```
### <a name="hostname_options"></a> Rockside Engine available on your network or online

During installation process :

```
Server Hostname: SERVER_IP OR DOMAIN_NAME(without "https://")
HTTP Server Port: 80
HTTPS Server Port: 443
```
Please indicate the server ip or your domain name as Server hostname and the correct ports.


### Modify Rockside Engine URL

Edit **~/.rockside/engine/rockside.env**

```
APP_URL=https://demo.rockside.io
UI_APP_URL=https://demo.rockside.io
```

Relaunch Engine with new configuration:
```
sudo rockside engine reconfigure
```


### Use your own certificate

Replace certificate and private key in the **~/.rockside/engine/certs** directory.

Restart rockside :

```
	rockside engine stop && rockside engine start
```

### Letsencrypt

#### Requirements

- You should have your own domain name redirected to your Rockside Engine server.
- Ports 80 & 443 must be open.
- Certbot must be installed.


#### Init letsencrypt
```
rockside engine letsencrypt init --hostname=demo.rockside.io
```

#### Renew letenscrypt certificate
```
rockside engine letsencrypt renew --hostname=demo.rockside.io
rockside engine stop && rockside engine start
```