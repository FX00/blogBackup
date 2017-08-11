---
title: git
date: 2017-08-11 14:57:12
categories: 
tags:
	-git
---

# Git 基础命令
Git是一个开源的分布式版本控制系统，用于敏捷高效地处理任何或小或大的项目。

-------------------

<!--more-->

## Git配置
Git提供了一个叫做 git config 的工具，用来配置或读取相应的工作环境变量，这些环境变量可以存放在以下三个不同的地方：

 -  `etc/gitconfig` 文件：系统中对所有用户都普遍使用的配置。使用 `git config` 时用 `--system`
读写
 -  `~/.gitconfig`  文件：用户目录下的配置文件只适用于该用户。使用 `git config ` 时用` --global`选项，读写的就是这个文件。
 - 工作目录中的  `.git/config` 文件，仅对当前项目有效，每一个级别的配置都会覆盖上层的相同配置。
 
 **命令**
 1.用户信息
 ```
 $ git config --global user.name "xxx"
 $ git config --global user.email test@163.com

 ```
 2.检查已有的配置信息
 
 ```$ git config --list```
 
##创建仓库
**git init**
 Git 使用 git init 命令来初始化一个 Git 仓库，Git 的很多命令都需要在 Git 的仓库中运行，所以 git init 是使用 Git 的第一个命令。
 
 ```$ git init```
 
 执行完该命令会在当前目录生成.git目录，
 使用指定目录为Git仓库：
 
 ```$ git init myTest```
 
初始化后，myTest目录下会出现.git目录，所有的
Git需要的数据和资源都会存放在这个目录中。 
如果当前目录下有几个文件想要纳入版本控制，需要先用git add命令告诉Git开始对这些文件进行跟踪，然后提交：

```
$ git add . //当前目录所有没被忽略的文件纳入版本控制
$ git add *.c // 当前目录下以.c结尾的文件
$ git status -s //查看上次提交后是否修改-s简短输出
$ git diff  //查看执行git status的结果的详细信息
$ git diff --cached //查看已缓存的改动
$ git diff HEAD //查看已缓存的与未缓存的所有改动
$ git diff --stat // 显示摘要而非整个diff
$ git add README // 当前目录下README文件 
$ git commit -m 'first commit' // 将缓存区内容添加到仓库，first commit 提交说明 
```
如果觉得 git add 提交缓存的流程太过繁琐，Git 允许用 -a选项跳过这一步。命令格式：

```
$ git commit -a
```

**git clone**
使用git clone从Git仓库中拷贝项目，克隆命令格式

```
$ git clone <repo> // repo:Git仓库地址
$ git clone <repo> <dir> //dir本地目录
```
例如

```
$ git clone https://github.com/FX00/storeAdmin.git
$ git clone https://github.com/FX00/storeAdmin.git myStore
```
**git resst HEAD**
git reset HEAD 命令用于取消已缓存的内容。执行 git reset HEAD 以取消之前 git add 添加，但不希望包含在下一提交快照中的缓存。
**git rm**
git rm 会将条目从缓存区中移除。这与 git reset HEAD 将条目取消缓存是有区别的。 "取消缓存"的意思就是将缓存区恢复为我们做出修改之前的样子。
默认情况下，git rm file 会将文件从缓存区和你的硬盘中（工作目录）删除。
如果你要在工作目录中留着该文件，可以使用 git rm --cached
***git mv**
git mv 命令用于移动或重命名一个文件、目录、软连接。

##分支管理
几乎每一种版本控制系统都以某种形式支持分支。使用分支意味着你可以从开发主线上分离开来，然后在不影响主线的同时继续工作。
创建分支命令：

```
$ git branch (branchname) //创建分支命
$ git branch //列出分支
$ git checkout (branchname) //切换分支命令
$ git checkout -b (branchname) //创建新分支并立即切换到该分支下
$ git branch -d (branchname) //删除分支
```

当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容，所以多个分支不需要多个目录，合并分支的命令：

```
$ git merge
```
合并冲突：合并不仅是简单的文件添加、移除的操作，git也会合并修改。可以用git add告诉Git 文件冲突已经解决

##Git 查看提交历史

```
$ git log
$ git log --oneline //简洁版本
$ git log --oneline --graph //查看历史中什么时候出现了分支、合并
$ git log --reverse --oneline //何时工作分叉、何时归并
$ git log --author=authername //查找指定用户的提交日志
```
##Git 远程仓库（Github）
**SSH Key**

由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以我们需要配置验证信息：
使用以下命令生成SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
后面的 your_email@youremail.com 改为你在 github 上注册的邮箱，之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。成功的话会在~/下生成.ssh文件夹，进去，打开 id_rsa.pub，复制里面的 key。回到 github 上，进入 Account => Settings（账户配置）。左边选择 SSH and GPG keys，然后点击 New SSH key 按钮,title 设置标题，可以随便填，粘贴在你电脑上生成的 key。
输入一下命令验证是否成功：

```
$ git -T git@github.com
```
**远程库**	
要添加一个新的远程仓库，可以指定一个简单的名字，以便将来引用,命令格式如下：

```
$ git remote add [shortname] [url]
```
查看远程库

```
$ git remote
$ git remote -v //加上-v可以看到每个别名的实际链接地址
```
提取远程仓库
1.从远程仓库下载新分支和数据,执行fetch后需要执行git mergr远程分支到你所在分支

```
$ git fetch
```
2.从远程仓库提取数据并尝试合并到当前分支

```
$ git pull
```
推送到远程仓库，推送你的新分支与数据到某个远端仓库命令:

```
$ git push -u origin master
```
删除远程仓库

```
$ git remote rm [别名]
```

