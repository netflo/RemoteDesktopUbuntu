# RemoteDesktopUbuntu

on Ubuntu 20.4   from:  https://linuxize.com/post/how-to-install-xrdp-on-ubuntu-20-04/

For Gnome based:

sudo apt update

sudo apt install ubuntu-desktop


For Xfce based :

sudo apt update

sudo apt install xubuntu-desktop




sudo apt install xrdp 

sudo systemctl status xrdp

sudo adduser xrdp ssl-cert 

sudo systemctl restart xrdp



#get your public IP with:   curl 'https://api.ipify.org?format=json'

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
