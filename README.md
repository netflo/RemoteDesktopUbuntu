# RemoteDesktopUbuntu

lightweight X display and as a service:
https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-22-04

then use bVNC Pro to ssh+ VNC for security




https://www.skynats.com/blog/install-ubuntu-desktop-on-a-digitalocean-droplet/

+ change RDP port to for example 12801  by mod'ying /etc/xrdp/xrdp.ini
+ sudo systemctl restart xrdp

==


dpkg --add-architecture i386
apt update
apt install wine32



as of 2024 this is the best link:
https://learn.microsoft.com/en-us/azure/virtual-machines/linux/use-remote-desktop?tabs=azure-cli


#

latest advice: use instructions under file aws_working_remote_desktop


from:  https://ubuntu.com/tutorials/ubuntu-desktop-aws#2-setting-up-tightvnc-on-aws
sudo apt install ubuntu-desktop tightvncserver gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal


and to launch this on higher res on port 51033:  vncserver :33 -geometry 1600x1200 

and need to install gecko to get a web browser ieexplorer.   wine-gecko




== or ===

from https://blog.alphavps.com/how-to-install-a-gui-on-a-linux-vps/



apt-mark hold acpid acpi-support

Here is another set of commands, which you need to run.

apt install xubuntu-desktop
apt install xrdp
adduser xrdp ssl-cert
echo "startxfce4" > ~/.xsession
chmod +x ~/.xsession
systemctl restart xrdp.service










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

sudo apt install --install-recommends winehq-stable -y


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




## Post install encryption of the home directory and swap:

from https://jumpcloud.com/blog/how-to-encrypt-ubuntu-20-04-desktop-post-installation

useradd -m user_to_encrypt

sudo apt install ecryptfs-utils cryptsetup -y

#add a new user to encrypt root

sudo adduser encryption_facilitator

sudo usermod -aG sudo encryption_facilitator

#login to encryption_facilitator
su encryption_facilitator

sudo ecryptfs-migrate-home -u user_to_encrypt



#




#Encrypt the Swap Space

swapon -s
free -h







####################  new version 22 ############################

Check installed architectures

Verify 64-bit architecture. The following command should respond with "amd64".

$ dpkg --print-architecture

See if 32-bit architecture is installed. The following command should respond with "i386".

$ dpkg --print-foreign-architectures

If "i386" is not displayed, execute the following.

$ sudo dpkg --add-architecture i386

Recheck with.

$ dpkg --print-foreign-architectures
Download and add the WineHQ repository key

$ sudo mkdir -pm755 /etc/apt/keyrings
$ sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
Download the WineHQ sources file

$ sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/jammy/winehq-jammy.sources
Update the package database

$ sudo apt update
Install Wine

The next command installs Wine Stable. To install Wine Development or Wine Staging, replace winehq-stable  by  winehq-devel or winehq-staging

After a major Wine upgrade (from Wine 6 to Wine 7, for example), Wine Stable may temporarily be unavailable, but Wine Development and Wine Staging can still be installed.

$ sudo apt install --install-recommends winehq-stable














