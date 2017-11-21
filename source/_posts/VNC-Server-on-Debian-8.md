---
title: VNC Server on Debian 8
date: 2017-11-21 10:00:42
tags:
---
### Installing VNC and XFCE
```bash
apt-get update
apt-get upgrade -y 
mkdir /dev/fuse && chmod +x /dev/fuse  
apt-get install xfce4 xfce4-goodies gnome-icon-theme tightvncserver iceweasel -y
```
<!--more-->
### VNC Server:
* start: `vncserver`  
* stop: `vncserver -kill :1`  
### Connecting from a VNC Client
You can now connect to your VNC server. Open your local VNC client, which will vary depending on your operating system.  
* On Windows, you can use UltraVNC [here](http://www.uvnc.com/downloads/ultravnc.html).  
* On OS X, you can use the built-in Screen Sharing app or access this app through Safari. In Safari, you can enter vnc://yourserverip:5901  

For your VNC Server address, enter yourserverip:5901 and use the password you just set for your VNC connection.
### About
> From：[Digitalocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-vnc-server-on-debian-8)

### 我的使用方式
主要是c9.io运行科学上网的程序，关闭界面后会自动休眠，VNC可以解决这个痛点。