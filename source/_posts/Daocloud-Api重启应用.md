---
title: Daocloud-Api重启应用
date: 2017-07-16 12:54:00
tags:
---
#### [Daocloud](https://www.daocloud.io/)  
> 重新定义计算的边界,业界领先的企业级应用云平台及解决方案。  

官方的测试资源回收机制:  
* 应用每 24 小时会自动停止
<!--more-->
* 长时间不使用的资源(Volume、服务)在下述情况下会被系统智能回收（当前观察期为两周，视资源池使用情况会有变动）
	* 在观察期内资源没有绑定任何应用
	* 在观察期内资源绑定的应用没有执行 启动／发布 等更新操作  
	
#### [开放API文档](http://docs.daocloud.io/api/)
当我们建立的应用停止后调用[**重新发布 App**](http://docs.daocloud.io/api/#重新发布-app)这个API就行了。
```
curl -X POST "https://openapi.daocloud.io/v1/apps/<app_id>/actions/redeploy" -H "Authorization: token <my token>" -H "Content-Type: application/json" -d '{"release_name": "v1.0.0"}'
```
* 获取**my token**： 用户中心-API页面,大概是这样子的*3od70jtlyaair4s024s77ourj7ttcuiq6eqh5wp4*
* 获取**app_id**： 点击你创建的应用，地址栏最后一长串就是咯，大概是这样子*d14591f9-f3cf-4cyb-a51d-75cb92c3b229*  
* 获取**release_name**：点击你创建的应用，应用图标下就是当前的镜像版本，一般为*latest*  
* 修改后的*curl*命令大概是这样子的：
```Shell
curl -X POST "https://openapi.daocloud.io/v1/apps/d14591f9-f3cf-4cyb-a51d-75cb92c3b229/actions/redeploy" -H "Authorization: token 3od70jtlyaair4s024s77ourj7ttcuiq6eqh5wp4" -H "Content-Type: application/json" -d '{"release_name": "latest"}'
```
  
#### VPS自动执行
先运行一下最后的curl命令，没出错的话对应的Daoapp会重新部署。然后加入计划任务完工。
`vi /etc/crontab`
```Shell
30 15 * * * root curl -X POST "https://openapi.daocloud.io/v1/apps/d14591f9-f3cf-4cyb-a51d-75cb92c3b229/actions/redeploy" -H "Authorization: token 3od70jtlyaair4s024s77ourj7ttcuiq6eqh5wp4" -H "Content-Type: application/json" -d '{"release_name": "latest"}'
```  
#### 更多使用方式和范例
* [My droppy](http://droppy.daoapp.io)  
  * 重新部署资源会清空，解决办法：使用Volume  
* [ruyo:DaoCloud.io部署指南](http://51.ruyo.net/p/3720.html)