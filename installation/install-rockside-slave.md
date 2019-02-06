
# <a name="install_rockside_slave"></a> Install Rockside Slave
A slave is controlled by a Rockside Engine. It's in charge of running nodes on a server. You can install it on the same server as the engine, but we recommend that you install it on a dedicated server. Slave requires a lot of space on the hard drive and CPU to synchronize with the blockchain.


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

