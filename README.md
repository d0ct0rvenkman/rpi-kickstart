# rpi-kickstart
Turn a Raspberry Pi 3 into a Kickstart server

First, install newer ansible. Raspbian's current version of 1.7.2 is ancient.
```bash
echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" > /etc/apt/sources.list.d/ansible.conf
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367
apt-get update
apt-get upgrade ansible
```
