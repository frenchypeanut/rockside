# <a name="advanced_setup"></a>Advanced configuration(SMTP, Certificates, Data dir...)

Rockside provide a notification feature, but before to be able to use it, you need to configure your SMTP provider.



By default you can use this command :



```

nano ~/.rockside/engine/rockside.env

```

And then complete those variable with your smtp informations :

```

MAIL_HOST=<your mail host>

MAIL_PORT=<your mail port>

MAIL_ENCRYPTION=<your mail encryption, by default put tls>

MAIL_USERNAME=<your mail username>

MAIL_PASSWORD=<your mail password>

```

And finally, relaunch the engine with the new configuration

```

sudo rockside engine reconfigure

```

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