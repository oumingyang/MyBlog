---
title: Build selfBlog with Hexo and Netlify for free
date: 2019-07-01 23:59:47
tags: Hexo Github Netlify
---

`注意`：本文只适合准备第一次动手搭建个人博客的读者， 不涉及站面美化

------

## 阅读要求

1. [如何安装npm并管理npm版本](https://www.npmjs.cn/getting-started/installing-node/)
2. [git Documentation](https://git-scm.com/doc)
3. [Windows下如何使用gitbash管理github](https://blog.csdn.net/luosaosao/article/details/63684470)

## 系统环境

Operation System: Win10

```c
// node.js 版本
$ node -v
v10.15.3
// npm 版本
$ npm -v
6.4.1
// git 版本
$ git --version
git version 2.21.0.windows.1
```

## 操作流程

​	**补充流程概述**

1. 使用git-bash，安装Hexo

   ```c
   npm install -g hexo-cli
   ```

   安装完毕后，执行如下命令在文件夹中创建所需文件，**要求文件夹内容必须为空**

   ```c
   hexo init <folder>
   cd <folder>
   npm install
   ```

2. 启动 __hexo__ 本地服务

   进入  `<folder>` ，执行 ` hexo server ` 命令，启动静态网站服务，访问 

   `http://localhost:4000/` 即可访问本地部署的Hexo网站

   ![访问本地部署的Hexo网站](C:\Users\oumingyang\AppData\Roaming\Typora\typora-user-images\1560579812661.png)

3. 创建新的网页

   在使用 __Netify__执行自动化部署之前，使用 `hexo generate` 将新生成的 __.md__ 文件编译成静态网页文件，在创建自动化部署之后，作者**只需要**创建新的文件并推送到github上即可。

   ```c
   // 创建文件
   hexo new Hi Mingyang
   // 生成静态文件
   hexo generate
   // 发布文件
   hexo publish Hi mingyang
   // 启动本地服务
   hexo server
   ```

4. 上传GitHub

   在托管给GitHub之前，先在<folder>文件夹下执行git初始化操作，并将不需要上传的文件放入 .gitignore文件中。

   ```c
   // git初始化
   git init
   // 屏蔽 public文件夹
   echo "/public" >> .gitignore
   // 将目录下所有文件添加到仓库
   git add .
   // 提交文件
   git commit -m "install hexo project"
   // 绑定远程仓库 <your repo url>是作者个人的远程仓库地址
   git remote add origin <your repo url>
   // 提交到远程仓库
   git push origin master
   ```

5. Netlify 托管

   [Netlify](`https://www.netlify.com/`)是一家国外的静态网站的托管平台，提供免费的https，自动化部署和升级，可以监控GitHub、GitLab或者Bitbucket做到自动更新发布。

   使用GitHub账号登录Netlify，并授权GitHub关联权限。根据页面指示，即可很快完成自动部署，此处不详细展开了。

6. 更新Blog

   现在作者要创建一篇新的blog，执行以下步骤：

   ```c
   // 创建一篇新的Blog
   hexo new "Hi New Blog"
   // 将<folder>/source/_posts目录下的Hi-New-Blog.md文件添加至暂存区
   git add Hi-New-Blog.md
   // 将暂存区的文件提价至本地库，并备注message
   git commit -m "Hi New Blog"
   // 将本地文件推送到GitHub上的master主枝上
   git push origin master
   ```

   Netlify在检测到新的push后，会立即调用`hexo generate` 将`Hi-New-Blog.md` 编译成新的静态文件，并部署在网路上。

7. 其他

   ```c
   git log ：查看提交的repo版本
   git reset --hard <目标版本号> ：为回滚至先前的版本，将Head从当前版本号处定位到<目标版本号>
   git push -f origin master ：执行回滚操作，删除目标版本到当前版本间的所有版本
   ```

8. 参考链接

   [Hexo+GitHub+Netlify搭建属于自己的博客网站](https://hhongwen.cn/20181216/build-own-blog/)

   