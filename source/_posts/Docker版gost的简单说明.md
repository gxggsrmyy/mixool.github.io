---
title: Docker版gost的简单说明
date: 2017-07-17 03:07:45
tags: docker
---
#### Gost go语言实现的安全隧道
项目地址：[ginuerzh/gost](https://github.com/ginuerzh/gost)
> * 可同时监听多端口
* 可设置转发代理，支持多级转发(代理链)
* 支持标准HTTP/HTTPS/SOCKS5代理协议
* SOCKS5代理支持TLS协商加密
* Tunnel UDP over TCP
<!--more-->
* 支持Shadowsocks协议 (OTA: 2.2+，UDP: 2.4+)
* 支持本地/远程端口转发 (2.1+)
* 支持HTTP 2.0 (2.2+)
* 实验性支持QUIC (2.3+)
* 支持KCP协议 (2.3+)
* 透明代理 (2.3+)  

#### Docker版本gost
* [Based on debian:oldstable-slim](https://hub.docker.com/r/mixool/gost/) Size: 23M
* [Based on alpine.](https://hub.docker.com/r/mixool/alpine-gost/) Size: 6M  

##### Arukas部署
* 8080-TCP|CMD `-L=:8080` 
	* client: chrome+switchyomega HTTPS Endpoint:443
	* gost client: `-L=:8080 -F=socks5://s_ip:s_port`
* 8088-UDP|CMD `-L=http2+kcp://:8088`
    * gost client: -L=:8080 -F=http2+kcp://s_ip:s_port
* 8080-TCP,8088-UDP,8338-tcp|CMD 
`-L=:8080 -L=http2+kcp://:8088 -L=ss://aes-128-cfb:password@:8338`  
	* client: shadowsocks client
	* gost client: `-L=:8080 -F=?`
###### Arukas于2017-7-31结束免费试用，可以尝试部署到Bluemix、[Hyber.sh](http://cioic.cc/2017/07/14/Windows%E4%BD%BF%E7%94%A8hyper-sh/)等其他平台。

##### Daocloud部署中转：
查找Dockerhub镜像mixool/gost,部署并设置端口443 TCP TCP 外部访问，高级设置中添加启动命令  
* https中转,替换https://xxxx.arukascloud.io为Endpoint: `-L=:443 -F=https://xxxx.arukascloud.io:443`
* ss中转: `-L=:443 -F=ss://aes-128-cfb:123456@ip:port` 

#### Tips:  
* 部署Daocloud中转后swichyomega也可设置代理类型为http或socks4,手机可使用此http代理。
* KCP加速需要使用gost的客户端。
* Arukas的Https代理地址Endpoint是固定的，Daoapp的地址和端口是固定的，均可以一次部署，长期使用（Daoapp默认的24小时关闭可用API自动重启，参考[**这篇文章**](http://cioic.cc/2017/Docker%E7%89%88gost%E7%9A%84%E7%AE%80%E5%8D%95%E8%AF%B4%E6%98%8E.html)
* 可以在CMD命令中添加更多的-L监听多端口搭建不同类型代理，搭建Https+SS服务`-L=:443 -L=ss://chacha20:123456@8338`
