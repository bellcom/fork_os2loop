# Useful information

OS2Web project development environment are driven by [Docksal](https://docksal.io/)

## Quick start

First of all, you need to install docksal by using [installation guide](https://docksal.io/installation) for your OS.

The quickest way to get up with OS2Web development flow is to use demo OS2Web installation. 
It will install OS2Web in the demo mode and will take care about all basic setting on you local environment.
Run following two command to get it started:
```
cd /path/to/os2web
fin start
fin rebuild-test
```

## Start up / shut down local environment.

After you installed docksal you have to simply navigate to OS2Web project folder and run `fin start`.
Docksal will download all required services and startup local environment.

To shut down local environment use command `fin stop`

## Get demo OS2Web 

To get demo installation in your local environment use command `fin rebuild-test`


## Troubleshoothing

1. On MacOs you might probably get an error with platform incompatibility
```
"qemu-x86_64: Could not open '/lib64/ld-linux-x86-64.so.2': No such file or directory nvm is not compatible with the npm config "prefix"
```
To get it solved you need to overwrite CLI image you using and add `--platform=linux/amd64`.
To do so add `Dockerfile` to the path `.docksal/services/cli/Dockerfile`
```
# Specify correct platform
FROM --platform=linux/amd64 docksal/cli:php7.4-3.0
```
and override cli service definition in `.docksal/docksal-local.yml`

```
version: "2.1"
services:
  cli:
    image: ${COMPOSE_PROJECT_NAME_SAFE}_cli
    build: services/cli
```

More info about [overriding or extending service images in Dcoksal](https://docs.docksal.io/stack/extend-images/).
