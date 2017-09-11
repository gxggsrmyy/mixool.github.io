---
title: VPS搭建ZeroNet，轻松接入ZeroNet
date: 2017-07-20 05:40:55
tags: 
- VPS 
- ZeroNet
---
#### ZeroNEt是什么
> 使用 Bitcoin 加密和 BitTorrent 网络的去中心化网络
  
<!--more-->
  项目中文说明：[zeronet.io](https://github.com/HelloZeroNet/ZeroNet/blob/master/README-zh-cn.md)
#### 为什么要用VPS搭建
* 不需要本地环境，随时访问，可以共享给更小白的朋友
* 吃灰小鸡不如利用起来

#### Debian 8 64搭建步骤
```Bash
apt-get update
apt-get install msgpack-python python-gevent
wget --no-check-certificate https://github.com/HelloZeroNet/ZeroBundle/raw/master/dist/ZeroBundle-linux64.tar.gz
tar xvpfz ZeroBundle-linux64.tar.gz
cd ZeroBundle
./ZeroNet.sh --ui_ip "*"
```
如果没报错，最新版本ZeroNet就已经成功安装了，访问你的IP:43110即可进入ZeroNet。
#### 添加访问密码和自启动
`mv /root/ZeroBundle/ZeroNet/plugins/disabled-UiPassword /root/ZeroBundle/ZeroNet/plugins/UiPassword`  
`vi /etc/systemd/system/zeronet.service`
```Bash
[Unit]
Description=zeronet

[Service]
ExecStart=/root/ZeroBundle/ZeroNet.sh --ui_ip "*" --ui_password yourpassword
Restart=always

[Install]
WantedBy=multi-user.target
```
`systemctl enable zeronet.service && systemctl start zeronet.service`
`reboot`
访问你的IP或者域名**:43110**测试是否成功
#### 一些资源
海盗湾种子站：IP:43110/1PLAYgDQboKojowD3kwdb3CtWmWaokXvfp
MSDN资源区：IP:43110/1AJB5rtjfB9imjDGVk5vtRtZp3zgYizbpG
#### 参考和PS
1. **不能确保你绝对匿名的情况下勿发表敏感言论**
2. [Yichengr](http://ryc111.com/2016/05/02/zeronet-on-vps/)
3. [项目地址](https://github.com/HelloZeroNet/ZeroNet)
4. 进入ZeroNet后继续学习吧
5. [cioic.cc](http://cioic.cc) 密码挺好猜的，勿滥用，~~随时失效~~ **失效吧，不安全**
6. [Docker搭建](http://zeronet.daoapp.io)