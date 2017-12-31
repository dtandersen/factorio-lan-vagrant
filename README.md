# Factorio Vagrant Box

This guide provides instructions to setup a Factorio server on a VirtualBox virtual machine (VM). Vagrant is used to create an Ubuntu VM with Docker installed. The [dtandersen/docker_factorio_server](https://github.com/dtandersen/docker_factorio_server) container is loaded into Docker.

The intended audience is users with basic familiarity with the command line.

# Introduction

Factorio has a headless server, but it only runs on Linux, which presents a problem for Windows users. Luckily, VirtualBox can run a Linux VM on Windows.

VMs can be tricky to setup. This is where Vagrant comes in. Vagrant starts a VM and runs scripts on it to configure it. This is accomplished with a Vagrantfile.

The final piece is Docker. Docker runs application containers. In this case, it runs the Factorio container. Docker containers are easy to upggrade, which is good, because Factorio has lots of updates during experimental cycles.


# Usage

## Before you begin

Install [Vagrant](https://www.vagrantup.com/downloads.html) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads).


## Quick Start

* Copy and paste the Vagrantfile and docker-compose.yml into a directory, e.g. `C:\Users\You\Factorio`, or clone this repository with git (recommend [TortoiseGit](https://tortoisegit.org/download/) for beginners).
* Press WIN+R and run `cmd` to open a command prompt.
* Type `cd C:\Users\You\Factorio` to change the directory to `C:\Users\You\Factorio`.
* Run `vagrant up` to start the VM.

Ubuntu will start and install various things. After installation completes, open Factorio, browse LAN games, and the server should appear.

A `factorio` directory is created with configuration files, mods, and saves.


## Log into the VM

To change server settings it's necessary to login to the server. This can be done through VirtualBox or ssh.


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

# Server configuration

## Modifying Ubuntu

The VM is for all intents and purposes a standard Ubuntu box. Feel free to run any commands you want on it. If something breaks Vagrant makes it easy to start over.


## Modifying Factorio



To change settings login to the virtual machine (VM).

```
cd /opt/factorio/config
sudo nano server-settings.json
```

To edit the docker-compose.yml:

```
cd /vagrant
sudo nano docker-compose.yml
```


## Restarting Server

```
cd /vagrant
sudo docker-compose stop
sudo docker-compose start
```


## Upgrade Factorio to latest version

```
cd /vagrant
sudo docker-compose stop
sudo docker-compose pull
sudo docker-compose restart
```


## Upgrade Factorio to a specific version

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


## Starting from scratch

If something got messed up sometimes its easiest to start over.

WARNING: This destroys everything including configuration, mods, and saves.

Open a command prompt:

```
vagrant destroy
```