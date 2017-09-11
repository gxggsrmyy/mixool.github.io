---
title: Openvpn
date: 2017-09-11 19:41:49
tags: openvpn
---
### OpenVPN-install
> This script will let you setup your own secure VPN server in just a few minutes.

实测用这个安装脚本可以科学上网，安全性未知，速度尚可。
<!--more-->
```
wget https://raw.githubusercontent.com/Angristan/OpenVPN-install/master/openvpn-install.sh  
chmod +x openvpn-install.sh
./openvpn-install.sh
```
#### 设置建议
* port 3389
* cipher AES-256-CBC

### 免流相关
免流测试使用http-proxy-option失败,使用HTTP Injector成功。
Host: apk.mmarket.com  每天可以领1G的流量。
#### http-proxy-option
```
http-proxy 10.0.0.172 80
http-proxy-retry
http-proxy-option VERSION HTTP/1.1
http-proxy-option AGENT user-agent -- Set HTTP "User-Agent" string to user-agent.
http-proxy-option CUSTOM-HEADER GET http://apk.mmarket.com/ HTTP/1.1
http-proxy-option CUSTOM-HEADER HOST apk.mmarket.com
http-proxy-option EXT1 "POST http://rd.go.10086.cn"
http-proxy-option EXT1 "GET http://rd.go.10086.cn"
http-proxy-option EXT1 "X-Online-Host: rd.go.10086.cn"
```
#### HTTP Injector
> OpenVPN - Disable "Start SSH" and use HTTP Injector with your OpenVPN if you don't have SSH server.
You have to add http-proxy 127.0.0.1 8989 and bypass route route replace_to_your_remote_proxy_ip 255.255.255.255 net_gateway (change "replace_to_your_remote_proxy_ip" to IP) to your VPN config.

China mobile:
> HTTP Injector 载荷生成器勾选 /正常 GET 后面注入/ 填写HOST/ 然后生成有效载荷.

```
http-proxy 127.0.0.1 8989
route 10.0.0.172 255.255.255.255 net_gateway
```

### 参考
[Angristan/OpenVPN-install](https://github.com/Angristan/OpenVPN-install)
[HTTP Injector](https://apps.evozi.com/httpinjector/)
[Latest version of OpenVPN](https://openvpn.net/index.php/open-source/downloads.html)