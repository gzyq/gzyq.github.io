---
title: Git常用命令
date: 2016-10-08 11:38:47
tags: [Git]
categories: tools
---
平时使用git管理自己这个小博客网站内容，结合经常用的一些操作，记录下来方便查阅参考，不定期修改，有错误的地方多多指正。
<!-- more -->
版本管理系统Git：
版本的分支（branch）和合并（merge）十分方便。
### 使用 ###
#### 配置 ####
	git config --list //显示当前的仓库配置
	git config [--global] user.name '[name]' //设置提交时用户信息
	git config [--global] user.email '[email地址]' //设置提交时用户信息

#### 克隆项目文件 ####
	git clone <git仓库地址>
	git clone <git仓库地址> <新名字> 

#### 初始化仓库 ####
该命令执行完后，会在当前目录下生产一个.git目录：

	git init
	git init url //使用指定目录

#### 查看状态 ####
查看哪些文件有修改：

	git status

#### 查看差异 ####
对比修改后文件，具体修改哪些信息并打印出来：

	git diff
	git diff HEAD //显示工作区与当前分支最新commit之间的差异
![](http://i.imgur.com/fcrCoCb.png)	

#### 查看日志 ####
	git log
![](http://i.imgur.com/24pLfXp.png)

	git log --oneline //每次提交的注释
![](http://i.imgur.com/Mo4UDvX.png)
	
	git reflog //显示当前分支最近的几次提交

#### 添加文件到暂存区 ####
文件至暂存区，意味着同时文件被跟踪

	git add <filename>
	git add . //添加当前目录下的所有文件

#### 提交 ####
根据暂存区内容创建提交记录

	git commit
	git commit -m '备注信息' //带备注信息，方便查阅
	git commit -a -m '全部提交' //先把所有修改的文件放入暂存区后提交
	git commit [file1] [file2...] -m '备注信息' //提交暂存区指定文件到仓库
#### 撤销修改 ####
	
	git checkout --filename //将文件内容从暂存区复制到工作目录（把文件回到之前提交到暂存区时的内容）
    git reset HEAD <filename> //将文件内容从上次提交复制到暂存区（修改暂存区的文件为上次的提交区的文件） 
	git reset HEAD <filename>// 将内容从上次提交复制到工作目录

#### 暂存区删除文件 ####
	git rm --cached <filename> //仅从暂存区删除
	git rm <filename>  //从暂存区与工作目录删除文件

#### 重命名 ####
把已经git rm --cached的文件通过add添加后，对其重命名

    git mv oldName newName

#### 分支管理 ####
	
	git branch //列出所有本地分支
	git branch -r //列出所有远程分支
	git branch -a //列出所有本地分支和远程分支
	
	git branch branchNew //新建一个branch，但依然留在当前分支
	git checkout -b [branch1] [指定哪个下建立新分支] //新建一个分支branch1，并切换到该分支
	
	git checkout [branch] //切换分支到branch

	git merge [branch1] //合并指定分支branch1到当前分支（直接指向当前分支）
	git merge --no-ff [branch1] //推荐（在当前分支下，生产一个新节点）

	git branch -d [branch1] //删除分支branch1

![](http://i.imgur.com/6qo6HMj.png)

### 远程仓库 ###
##### 查看远程仓库名 #####

	git remote
	git remote -v //显示所有远程仓库
	git remote show [remote] //显示某个远程仓库的信息
![](http://i.imgur.com/6nuydZw.png)
![](http://i.imgur.com/XNziS8O.png)
	
##### 建立仓库 #####
把本地仓库和远程仓库关联起来，如果不执行，每次push时需要制定远程服务器的地址：

	git remote add [newname] [url] //增加一个新远程仓库并命名

	git remote add origin git@github.com:用户名/仓库名.git

##### 推送至远程仓库 #####
	git push [remote] [branch] //上传本地指定分支到远程仓库
	git push [remote] --force //强行推送当前分支到远程仓库，即使有冲突
	git push [remote] --all //推送所有分支到远程仓库

	git push origin master //推送远程仓库

##### 取回远程仓库 #####
	git pull [remote] [branch] //取回远程仓库的变化，并与本地分支合并
##### 更新本地 #####
	git fetch [remote] //下载远程仓库的所有变动


### demo ###
	cd project
	git init
	git add .
	git commit -m 'commit'
	git remote add origin git@github.com:gzyq/demo.git
	git push origin master

	git checkout -b branch1 master
	git cheokout master
	git merge --no-ff branch1
	git branch -d branch1

### 其他 ###

ls 查看目录下的所有文件
