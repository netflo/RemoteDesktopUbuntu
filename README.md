# RemoteDesktopUbuntu

from  https://docs.microsoft.com/en-us/azure/virtual-machines/linux/use-remote-desktop

### Remote Desktop on Ubuntu 20.04

sudo apt-get update
sudo DEBIAN_FRONTEND=noninteractive apt-get -y install xfce4
sudo apt install xfce4-session

sudo apt-get -y install xrdp
sudo systemctl enable xrdp

echo xfce4-session >~/.xsession

sudo service xrdp restart



### To help lock down get your public IP with:   curl 'https://api.ipify.org?format=json'
#restricting access from an IP is a must    
sudo ufw allow from {ip_address/mask} to any port 3389
if not, need to access through a SSH Tunnel !




### cloud server risk on IPv6 disable if not required:
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=1

and to make permanent,  modify /etc/sysctl.conf I

with

net.ipv6.conf.all.disable_ipv6=1
net.ipv6.conf.default.disable_ipv6=1
net.ipv6.conf.lo.disable_ipv6=1

followed by:

sudo sysctl -p



and also if required edit  /etc/rc.local 

#!/bin/bash
# /etc/rc.local

/etc/sysctl.d
/etc/init.d/procps restart

exit 0

Now use chmod command to make the file executable:

sudo chmod 755 /etc/rc.local


### Install wine

from https://wine.htmlvalidator.com/install-wine-on-ubuntu-20.04.html

Verify 64-bit architecture. The following command should respond with "amd64".

$ dpkg --print-architecture

See if 32-bit architecture is installed. The following command should respond with "i386".

$ dpkg --print-foreign-architectures

/////////////////////////////////////////////////////////////////////////////
#If "i386" is not displayed, execute the following.
sudo dpkg --add-architecture i386

#Recheck with.

$ dpkg --print-foreign-architectures
#Add the WineHQ Ubuntu repository.

#Get and install the repository key.

wget -nc https://dl.winehq.org/wine-builds/winehq.key

sudo mv winehq.key /usr/share/keyrings/winehq-archive.key

wget -nc https://dl.winehq.org/wine-builds/ubuntu/dists/focal/winehq-focal.sources

sudo mv winehq-focal.sources /etc/apt/sources.list.d/

#Update the package database.

sudo apt update

#Install Wine

sudo apt install --install-recommends winehq-stable


##### Secure delete of files  when not using SSD #####

from https://www.howtogeek.com/425232/how-to-securely-delete-files-on-linux/

The secure-delete commands use the following sequence of overwrites and actions:

    1 overwrite with 0xFF value bytes.
    5 overwrites with random data.
    27 overwrites with special values defined by Peter Gutmann.
    5 more overwrites with random data.
    Rename the file to a random value.
    Truncate the file.


sudo apt-get install secure-delete

srm -rvz the_folder_slash_directory


