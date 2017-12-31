# Factorio Vagrant Box

This guide provides instructions to setup a Factorio server on a VirtualBox virtual machine (VM). Vagrant is used to create an Ubuntu VM with Docker installed. The [dtandersen/docker_factorio_server](https://github.com/dtandersen/docker_factorio_server) container is loaded into Docker.

# Usage

## Before you begin

Install [Vagrant](https://www.vagrantup.com/downloads.html) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

## Quick Start

Copy and paste the Vagrantfile and docker-compose.yml into some directory, e.g. `C:\Users\You\Factorio`. If you know how to use git (recommend [TortoiseGit](https://tortoisegit.org/download/) for beginners) you can clone this repository.

Open a command prompt by pressing WIN+R and running `cmd`.

Now change the directory to `C:\Users\You\Factorio` by typing `cd C:\Users\You\Factorio`.

Now type `vagrant up` to start the VM.

A window with Ubuntu will open and various things will start installing.

After installation is complete open Factorio, browse LAN games, and the server should appear.

## Log into the VM

### Login with Virtual Box

If the VM isn't already visible, open VirtualBox and double click Factorio.

Login with username: vagrant and password: vagrant. The keyboard and mouse are now stuck inside the VM. To return to control the desktop press right CTRL.

### Login with ssh (advanced)

ssh has to be installed.

```
vagrant ssh
```

### Login with Putty (advanced)

Install and run the Vagrant Putty plugin:

```
vagrant plugin install vagrant-multi-putty
vagrant putty
```

## Modifying Configuration

To change settings login to the virtual machine (VM). 

```
cd /opt/factorio/config
nano server-settings.json
```

To edit the docker-compose.yml:

```
cd /vagrant
nano docker-compose.yml
```

## Restarting Server

```
cd /vagrant
sudo docker-compose stop
sudo docker-compose start
```

## Upgrade server to latest version

```
cd /vagrant
sudo docker-compose stop
sudo docker-compose pull
sudo docker-compose restart
```

## Upgrade server to specific version

Change the `image` in docker-compose.yml, e.g. `image: dtandersen/factorio:0.16.11`.

```
cd /vagrant
sudo docker-compose stop
nano docker-compose.yml
sudo docker-compose restart
```

## Adding mods

```
cd /factorio/mods
wget <link to mod>
```
