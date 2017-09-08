---
title: VPS搭建HTTPS代理
date: 2017-09-08 09:53:50
tags:
---
电脑上使用HTTPS代理挺方便的，Chrome+Switchyomega即可科学上网，这里推荐两个简单的搭建方法。
准备一个域名，并解析到VPS.
<!--more-->
### Goproxy-vps
安装方法：
`curl -L git.io/get-goproxy-vps | bash`
只需输入域名即可开始享用。
### Gost
#### 申请免费证书
`curl https://get.acme.sh | bash - && cp /root/.acme.sh/acme.sh /usr/bin/acme.sh && chmod u+x /usr/bin/acme.sh`
`acme.sh  --issue  --dns --keylength ec-256 -d yourdomain.com`
> 按提示给出的字符更新 DNS TXT 记录

```acme.sh --renew --ecc -d yourdomain.com```
> 记录证书文件路径，待用。

#### 使用Gost搭建
`wget https://github.com/ginuerzh/gost/releases/download/v2.4/gost_2.4_linux_amd64.tar.gz`
`tar zxvf gost_2.4_linux_amd64.tar.gz`
`mv /root/gost_2.4_linux_amd64/gost /root/`
`chmod +x gost`
Gost可以搭建多种类型的代理，这里只是用其一个功能：
`nohup /root/gost -L="http2://:443?cert=/path/to/my/cert/file&key=/path/to/my/key/file" &`
> 修改命令中的证书文件路径，端口亦可修改。~~一般NAT VPS不提供443端口，好在便宜，低成本科学上网~~

伪装成一个HTTPS网站：[悄悄的，打枪的不要](https://9ot.top/)

###### 参考
[goproxy-vps](https://github.com/phuslu/goproxy/issues/1470)
[gost](https://github.com/ginuerzh/gost#gost---go-simple-tunnel)
