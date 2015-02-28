# Box server deployment
Box used for isolate used processes in project environment. It makes deployment and manage of services more easier.

## Dependency
You must use Systemd as upstart service

## Phylosophy
- There are internal server things
- There are services that must be run on your server in special environment
- This special environment is set to box user and all you need in one folder
- There are folder named by service and systemd folder to operate it via systemd
- You can install one or more service on one machine
- You can deploy box manager to machines but use only couple of services

## Structure
There is folder in root dir. One folder is one service. In folder there is log dir, configs, run files, socks and so on. That allows to isolate service generated files into one single dir.
You can create your own service with systemd/custom.service file and make folder custon in root directory and place there configs and other needed stuff.
It helps you to isolate running services and dont bother about different folders, files, logs, configs for each service.

### Example structure
* service1
  * service1.conf
  * log
  * service1.pid
* service2
  * service2.conf
  * log
  * service2.pid
* systemd
  * service1.service
  * service2.service

You can create any service you want and manage it via box tools.

## Installation
Clone into directory first
```bash
git clone git@github.com:dmitrykuzmenkov/box.git
```

Now you can deploy it to you server with deploy script. Be sure you have created box user
```bash
cd box
./deploy myserver
```

Ok. Finally done. Log into server and do cool stuff.

## Start new service
Just run install command. This command will install and start prefered service.
```bash
 ./install mysql
```
This command also will create the file used and put there service name you have already installed.

## Remove service
You can remove service from system using remove script
```bash
./remove mysql
```
This command will remove systemd.service file, stop running service and remove line from used file where all installed services stored.

## Manage installed services
There is special util to manage installed services. It's called service. It is systemctl like functionality.
```bash
./service start all
```
or for single service
```bash
./service status php-fpm
```