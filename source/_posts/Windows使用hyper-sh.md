---
title: windows使用hyper.sh
date: 2017-07-14 14:37:47
tags:
---

[Hyper.sh](https://console.hyper.sh/register/invite/Wqwq4zj25nCQ8Q0267waig7g9dMrOWTR)是一家国外的容器服务提供商，新注册有送10刀。

定价页面: https://hyper.sh/pricing.html

#### 将下载的hyper.exe放在CMD的相应路径下运行，windows下使用常用命令：

##### 建立s4大小的容器

`.\hyper.exe run --size s4 -d --name centos-ssh -p 22:22 -p 443:443 -p 80:80 kinogmt/centos-ssh`

<!--more-->

##### 查看所有容器

`.\hyper.exe ps -a`

##### 停止某个容器(容器Name 或者 ID)

`.\hyper.exe stop centos-ssh`

##### 重启某个容器(容器Name 或者 ID),重启不会丢容器的数据。

`.\hyper.exe restart centos-ssh`

##### 启动某个容器(容器Name 或者 ID)

`.\hyper.exe start centos-ssh`

##### 删除某个容器(容器Name 或者 ID) 删除前请停止

`.\hyper.exe rm centos-ssh`

##### 查看所有镜像获取ID

`.\hyper.exe images -a`

##### 删除镜像(ID)

`.\hyper.exe rmi ID`

##### 删除所有资源后，释放FIP，避免扣费。