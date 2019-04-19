# How to upgrade Rockside

### Upgrade Rockside CLI

Download the new version .
curl -sSL http://releases.rockside.io/cli/get.sh | sh


### Upgrade Rockside Engine
When a new version of rockside is released you can upgrade your existing version with :

```
rockside engine upgrade
```

This command will clear Rockside containers, download images of the new version and create containers with the new images. Then it will execute database migrations if needed.

### Upgrade Rockside Slave

- Stop your slave.
- Download the new version .
```
curl -sSL http://releases.rockside.io/slave/get.sh | sh
```
- Start back your slave.
