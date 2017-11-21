---
title: Heroku部署gsnova
date: 2017-11-21 12:01:49
tags: 科学上网
---
### Gsnova
> Private proxy solution.  
>> About: [yinqiwen/gsnova](https://github.com/yinqiwen/gsnova)  

<!--more-->
  
### Heroku部署-科学上网
1. 安装[git](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)和[heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)  
2. 下载[gsnova-pass](https://github.com/yinqiwen/gsnova/releases)
3. 解压gsnova-pass包,进入解压后的文件夹，依次执行:  
```Bash
git init
git add .
git commit -m "gsnova"
heroku login
heroku create
git push heroku master
```  
4. [Gsnova客户端](https://github.com/yinqiwen/gsnova/releases)修改配置文件  

### 参考
* [Github/gsnova](https://github.com/yinqiwen/gsnova)
* [Deploying Go Apps on Heroku](https://devcenter.heroku.com/articles/deploying-go)
* [一次Heroku部署完整过程](http://xpleaf.blog.51cto.com/9315560/1739940)
* [Heroku 部署说明](http://limodou.github.io/uliweb-doc/zh_CN/heroku.html)
