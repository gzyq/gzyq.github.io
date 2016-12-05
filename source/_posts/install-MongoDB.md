---
title: window下安装MongoDB
date: 2016-12-05 10:51:10
tags: [MongoDB]
categories: note
---

因为想在node.js搭建的聊天室的基础上，加上数据存储的功能，推荐较多的属MongoDB，所以自己就学习安装了一个MongoDB数据库，将过程记录下来，方便后续回顾总结。
<!-- more -->
### 一、MongoDB下载 ###
根据自己系统配置，在官网[https://www.mongodb.com/](https://www.mongodb.com/ "MongoDB官网")下载相应版本。
![](http://i.imgur.com/qiGl0k7.png)
**注意**：选择Download Source时，尽量选择zip格式，同时避免直接点msi安装包（安装包安装时，目录层级较多，稍麻烦）。
### 二、MongoDB安装###
1、在D盘（其他盘均可）的根目录下新建一个名为mongodb的文件夹，将下载的压缩包解压至改文件夹内。
2、在此文件夹新建data文件夹，用于存放数据库及日志文件。
![](http://i.imgur.com/zZWAl2N.png)
3、data文件下新建db文件夹用来存放数据库，新建log文件夹存放日志文件mongo.log。
![](http://i.imgur.com/tPPdc8L.png)
**说明**：一定要在MongoDB服务启动之前，手动创建存放数据库文件的文件夹，即此处的db文件夹，该目录不会自动创建。
4、打开CMD命令行，进入安装目录，此处为D:\mongodb，进入D:\mongodb\bin目录
![](http://i.imgur.com/hd8caH5.png)
执行启动MongoDB服务，需要输入`mongod.exe --dbpath d:mongodb\data\db`
![](http://i.imgur.com/crI8uRM.png)

可以看到，MongoDB默认连接端口号为27017，此时，在浏览器地址中打开`http://localhost:27017/`可以看到以下提示，则表示连接成功。![](http://i.imgur.com/GKmQlD0.png)
### 三、将MongoDB作为Windows服务启动###
1、在mongodb文件夹下新建mongo.config配置文件
![](http://i.imgur.com/T0ZQG0c.png)

其中，mongo.config内容为：
![](http://i.imgur.com/n8d8HzV.png)

    参数说明：    
	dbpath=D:\mongodb\data\db  //指定MongoDB数据存储路径
    logpath=D:\mongodb\data\log\mongo.log  //MongoDB日志输出文件名称，即日志路径
 2、打开CMD命令行，进入D:\mongodb\bin目录，
需要输入 `mongod --config D:\mongodb\mongo.config --install --serviceName "MongoDB"`

	参数说明：
	install：安装MongoDB服务
    serviceName：安装Window服务时使用的服务器名
![](http://i.imgur.com/fRMgBCB.png)
打开mongo.log就可以看到有详细的日志输入了。
3、打开CMD命令行，输入service.msc,就可以看到MongoDB服务了。
![](http://i.imgur.com/AvwVv45.png)

![](http://i.imgur.com/e6txJVs.png)

至此，启动服务就成功注册了。
### 四、总结###
虽然很简单的安装，一开始也出现不少问题。如直接安装msi文件，导致目录层级过多，在安装服务时目录名称中包含空格导致不能识别命令，配置文件位置放错，或者在输入命令时不仔细导致错误等，希望以后都够细心注意。