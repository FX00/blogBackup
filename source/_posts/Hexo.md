---
title: 使用Hexo搭建个人博客
date: 2017-07-24 14:54:02
tags:
	- hexo
	- blog
---
###安装Hugo
1.首先安装Git,Node.js

2.安装hexo 
hexo的常用的命令
    
    ```bash
    $ hexo g  #完整命令为hexo generate,用于生成静态文件
    $ hexo s  #完整命名为hexo server,用于启动服务器，主要用来本地预览
    $ hexo d  #完整命令为hexo deploy,用于将本地文件发布到github上
    $ hexo n  #完整命令为hexo new,用于新建一篇文章
    ```
<!--more-->

   鼠标右键任意地方，选择Git Bash，使用以下命令安装hexo
    
    ```bash
    $ npm install hexo-cli -g
    ```
   如果之后在使用过程中，遇到以下错误
    ```bash
    ERROR Deployer not found : github
    ```
   则运行以下命令，或者你直接先运行这个命令更好
   
    ```bash
    $  npm install hexo-deployer-git --save
    ```
    
   接下来创建放置博客文件的文件：Hexo文件夹。（名字和位置自由选择，最好不
   要放在中文目录下），如我的位置`C:\web\Hexo`，进入文件夹，鼠标右键选择
   Git Bash，执行以下命令，Hexo会自动在该文件夹下下载搭建网站 所需的所有文件
   
    ```bash
    $ hexo init
    ```
   安装依赖包
   
    ```bash
    $ npm install
    ```
   在`C:\web\Hexo`内执行以下命令

    ```bash
    $ hexo g
    $ hexo s
    ```
   然后用浏览器访问`http://localhost:4000/`，此时可以看到博客，当然这个博客只
   是在本地的，别人是看不到的。

###注册Github账号
   已有Github账号跳过此步，首先进入Github进行注册，用户名，邮箱和密码之后都需要用到。
###创建repository
   repository相当于一个仓库，用来放置你的代码文件，首先，登陆进入Github，并进入个人页面，选择Repositories,
   然后New一个repository
   ![一](/assets/blogImg/20170724150118.png)       
   创建时，只需要填写Repository-name即可，当然这个名字的格式必须为你的github用户名,我的是FX00.github.io
   ![二](/assets/blogImg/20170724150249.png)       
###部署本地文件到Github
   既然Repository已经创建，当然先把博客放到Github上去看看效果，编辑`C:\web\Hexo`下的`_config.yml`文件。
   在`_config.yml`最下方，添加如下配置   
   
   ```
   deploy: 
  	type: git
  	repository: http://github.com/FX00/FX00.github.io.git
  	branch: master
   ```
   
   配置好并保存后，执行以下命令部署到Github上。
   
   ```bash
   $ hexo g
   $ hexo d
   ```
   
###发表一篇文章
1.在Git Bash执行命令：`$ hexo new "my first post"`
2.在`C:\web\Hexo\source\_post`中打开my-first-post.md编辑