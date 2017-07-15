---
title: Hexo发布和备份到github
date: 2017-07-14 19:34:06
tags: 
- Hexo
- Github
---
#### 搭建流程  

1. 创建仓库  

2. 创建两个分支：master 与 hexo

3. 设置hexo为默认分支（方便手动管理）

4. 本地拷贝仓库`git clone https://github.com/mixool/mixool.github.io.git`
<!--more-->

5. 在`mixool.github.io.git`文件夹下有一个隐藏的.git文件夹，通过Git bash依次执行:

   ```
   npm install hexo
   在hexo init前复制.git，完成hexo init后再黏贴回来覆盖新生成的.git
   hexo init
   npm install
   npm install hexo-deployer-git
   ```

6. 修改`_config.yml`中的deploy参数，分支应为master

7. 依次执行:
   ```
   git add .
   git commit -m "update hexo"
   git push origin hexo
   ```
8. 执行`hexo g -d`生成网站并部署到GitHub上,GitHub上的仓库就有两个分支，一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。完美( •̀ ω •́ )y  


#### 更新和恢复

   1. 更新  
   ```
   git add .
   git commit -m "update hexo"
   git push origin hexo    //更新到hexo
   hexo g -d               //发布到master
   ```
   2. 恢复
  [Install hexo](https://hexo.io/zh-cn/docs/index.html#安装)
   ```
   git clone https://github.com/mixool/mixool.github.io.git
   cd mixool.github.io
   npm install
   npm install hexo-deployer-git --save
   git clone https://github.com/iissnan/hexo-theme-next themes/next
   hexo s
   ```