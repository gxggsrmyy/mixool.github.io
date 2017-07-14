---
title: 使用Droppy搭建私人云存储
date: 2017-07-14 11:13:55
tags:
---
#### 一个开源的网盘服务程序Droppy
通过浏览器就能够随时随地进行上传下载、预览编辑、外链分享等文件管理操作，功能强大，且十分轻量，非常适合作为个人的网络存储管理界面。
[Demo试用](https://droppy.silverwind.io/)
<!--more-->
#### 安装步骤 演示使用的系统环境为Debian 8 Jessie x64。
##### Droppy基于Node.js，所以首先需要安装Node.js环境
```Bash
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
apt-get install -y nodejs
```
##### 安装Droppy
```Bash
npm install -g droppy
```
##### 安装完成后使用`droppy -h`可以查看运行命令。
###### 如果需要让Droppy监听小于1024的端口
```Bash
apt-get install libcap2-bin
setcap cap_net_bind_service=+ep `readlink -f \`which node\``
```
然后修改配置文件`vi /root/.droppy/config/config.json`
重新运行droppy即可。
#### 参考
[teaink](https://teaink.com/archives/droppy_install.html)
[Github主页](https://github.com/silverwind/droppy)