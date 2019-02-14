# How to install Rockside Engine on Linux or OS X (LCP Release)
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

### Run Rockside Slave

If you want to try Rockside on your local machine, you can launch Rockside Slave directly after Rockside Engine installation

```
rockside slave start
```

This command download and install Rockside slave, and register it to the local instance of Rockside engine.

Prefer manual [install](https://github.com/blockchain-studio/rockside/blob/Ethcc-release/installation/install-rockside-slave.md) if you want to run a single/multiple production instance(s) of Rockside Slave on remote servers


### Create an account and sign-up on Rockside Engine

- Open a browser and fill your Rockside Engine Url
- Click on sign-up
- Fill the form
- You can now sign-in on Rockside Engine


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

#### Renew letsenscrypt certificate
```
rockside engine letsencrypt renew --hostname=demo.rockside.io
rockside engine stop && rockside engine start
```