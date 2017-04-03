# rpi-kickstart

## Purpose
Turn a Raspberry Pi 3 (or regular Debian/CentOS machine) into a Kickstart server.

## Words describing things
The project started initially with the goal of being able to easily deploy a Raspberry Pi 3 as a portable kickstart/PXE boot server. While crafting the Ansible job, I found myself covering both Raspbian and CentOS, and after some testing, it's confirmed it'll worth in both contexts. As it stands, the ansible playbook is designed to be pulled down to the RPI and run locally. I may make it work remotely as well in the future.

The playbook is built in such a way that the main playbook is a generic framework that will include another playbook with site-specific custom configuration. This allows the main playbook to be updated independently of individual customizations.

It's currently fairly rigid in its expectations of interface names (mainly since it was born on a RPi) and IP address networks. I may decided to make it more flexible later, and I may not.

## Installation
* Install your OS
* Configure your networking so that you're connecting through something other than eth0 (either your wifi interface or another ethernet card). Configure eth0 with the IP address of `192.168.42.1` and netmask of `255.255.255.0`.
* Install git and ansible. If you're on Raspbian, install a newer ansible, as the version that comes with Raspbian is way too old.
```bash
echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" > /etc/apt/sources.list.d/ansible.list
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
apt-get update
apt-get upgrade ansible
```
* Clone the repo somewhere
```bash
cd /usr/src
git clone https://github.com/d0ct0rvenkman/rpi-kickstart.git
```
* Copy your local playbook to `/root/rpi-kickstart-local.yaml`. If you don't have a local playbook, edit the main playbook and remove/comment the last two lines.
* Run the ansible job
```bash
cd /usr/src/rpi-kickstart/
ansible-playbook rpi-kickstart.yaml -i hosts.yaml
```
* Profit?

## Local playbook
Included is a sample playbook that does some helpful things like deploying custom nginx configs, a PXE menu, pulling down kickstart configs into the nginx docroot, and getting up to date PXE boot media. You'll want to make your own.
