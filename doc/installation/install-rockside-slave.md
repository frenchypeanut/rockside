
# <a name="install_rockside_slave"></a> Install Rockside Slave
A slave is controlled by a Rockside Engine. It's in charge of running nodes on a server. You can install it on the same server as the engine, but we recommend that you install it on a dedicated server. Slave requires a lot of space on the hard drive and CPU to synchronize with the blockchain.


### Requirements

Rockside Slave requires the Docker Engine to run. Follow Docker installation instructions for your platform at https://docs.docker.com/engine/installation/#supported-platforms.

If you install the Slave on the save server as the Engine, Docker engine should be already installed.

### Operating systems

Rockside can be installed on Linux and MacOS.
**If you are on linux please prefix all the following commands with 'sudo'**


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

```
rockside-slave --engine.key SLAVE_REGISTRATION_TOKEN --engine.url ROCKSIDE_ENGINE_URL:PORT
```

If you run rockside slave on the same machine as the engine, add the parameter **-http.detectIp**


```
rockside-slave --engine.key SLAVE_REGISTRATION_TOKEN --engine.url ROCKSIDE_ENGINE_URL:PORT -http.detectIp
```


**Tips:** To run Rockside Slave in background, add "&" at the end of the command. When it's running in background, simply type fg to bring it to foreground.

### Configure Rockside slave service on systemd

If you run a a linux distribution on your server, and use systemd, here are the configuration steps:

Create and edit /lib/systemd/system/rockside-slave.service file with the following lines. Don(t forget to replace ENGINE-KEY and ENGINE-URL by your own Rockside engine parameters

    [Unit]
    Description=Rockside Slave
    After=docker.service
    Requires=docker.service
    [Service]
    Type=simple
    Restart=always
    RestartSec=5s
    ExecStart=/usr/local/bin/rockside-slave -data /var/lib/rockside-slave -engine.key ENGINE-KEY -engine.url ENGINE-URL
    [Install]
    WantedBy=multi-user.target

Enable the service

    systemctl enable rockside-slave.service

Start the service

    systemctl start rockside-slave.service
    
### Run Rockside Slave using https

To enable https communication with the slave you have to add those parameters : -http.tls -http.ip=SLAVE_ACCESSIBLE_IP

```
rockside-slave --engine.key SLAVE_REGISTRATION_TOKEN --engine.url ROCKSIDE_ENGINE_URL:PORT -http.tls -http.ip=SLAVE_ACCESSIBLE_IP
```




## Deploy facilities on cloud provider

You can deploy Rockside Slave on any cloud provider. Rockside helps you to deploy your slave in one click on Amazon Web Services and Microsoft Azure with pre-provisioned scripts. You need to be logged in an existing account. Google Cloud Platform is coming soon.

![Image of Rockside Slave deployment possibilities](https://raw.githubusercontent.com/blockchain-studio/rockside/master/doc/slave_deployment.png)


### Deployment on Microsoft Azure

Please ensure to be logged in your browser on your Microsoft Azure account. Click on the Azure button on your Rockside Engine interface. A new page will be opened, and you will be directly on the Microsoft custom deployment. Fill the requested details with **your own** parameters. You can find the Engine key under the name of 'slave registration token' on the slave registration page where you had the choice between Azure, AWS or manual installation. Then launch the deployment. You will be able to see your new slave instance of the slave page of your Rockside Engine in a few minutes.


![Image of Rockside Slave deployment on Azure](https://raw.githubusercontent.com/blockchain-studio/rockside/master/doc/azure_custom_deployment.png)


### Deployment on AWS

Please ensure to be logged in your browser on your AWS account, and to have already an existing EC2 key pair. Click on the AWS button on your Rockside Engine interface. You will be asked to choose a timezone.

![Image of Rockside Slave deployment on AWS - zone](https://raw.githubusercontent.com/blockchain-studio/rockside/master/doc/aws_zone.png)


Then a new page will be opened, and you will directly be on the AWS Cloudformation page. Engine Key is already pre-filled. Fill the other requested details with **your own** parameters. Then launch the deployment. You will be able to see your new slave instance of the slave page of your Rockside Engine in a few minutes.


![Image of Rockside Slave deployment on AWS - deployment](https://raw.githubusercontent.com/blockchain-studio/rockside/master/doc/aws_deployment.png)
