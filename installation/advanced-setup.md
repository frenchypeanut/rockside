# <a name="advanced_setup"></a>Advanced configuration(SMTP, Certificates, Data dir...)

### How to configure SMTP Server

Rockside provide a notification feature, but before to be able to use it, you need to configure your SMTP provider.

You can use this command :


```
rockside engine configure-smtp
```

You will be asked for SMTP host, SMTP port, SMTP username and password, and mail encryption. Rockside Engine will be reloaded with new configuration.


### Use a custom data dir for Rockside Engine installation
By default Rockside Engine installs in your HOME directory. It create a folder at this path "~/.rockside/engine". This folder contains all settings required by the application.  To specify a custom datadir use:

```
rockside engine install --datadir /ssd/rockside-engine
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