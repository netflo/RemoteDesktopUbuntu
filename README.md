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


#restricting access from an IP is a must
sudo ufw allow from {ip_address/mask} to any port 3389

if not, need to access through a SSH Tunnel !


