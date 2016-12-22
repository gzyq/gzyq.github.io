---
title: 计算机丢失api-ms-win-crt-runtime-|1-1-0.dll
date: 2016-12-21 20:18:49
tags: [note]
---

在笔记本 win7系统 安装mongoDB时，报错“计算机无法启动此程序，因为计算机丢失api-ms-win-crt-runtime-|1-1-0.dll。尝试重新安装改程序以解决此问题。”。在网上找了很多解决方案，多数是说，下载api-ms-win-crt-runtime-l1-1-0.dll复制到对应系统文件中就行，经过尝试失败了，现在问题解决了，记录下来给遇到相同的问题的大家做参考。
<!-- more -->
### 问题 ###
先贴一张我遇到的问题，如下：
![](http://i.imgur.com/NEX9FZA.png)
之前在台式机上面，安装mongoDB时，没有遇到过该问题，看网上有些帖子里面说，可能是因为安装了比较精简的系统导致这个文件缺失，不过真实的原因不是很清楚，有知道的可以告诉我，很想知道。
### 解决 ###
1. 根据电脑系统，下载[Visual C++ Redistributable for Visual Studio 2015](https://www.microsoft.com/zh-cn/download/details.aspx?id=48145)相应版本，vc_redist.x64.exe(64位)或者vc_redist.x86.exe(32位)进行安装。
2. 安装过程中，通常会报下面错误，0x80240017未指定错误，导致设置失败。
![](http://i.imgur.com/XGlgAHA.png)
注：该图为引用（自己报错时忘记截图）
接下来主要解决该问题，此处主要是需要获取权限：
- WIN+R，在运行对话框中，输入：gpedit.msc
- 查找：计算机配置-Window设置-安全设置-安全选项-用户账户控制：以管理员批准模式运行所有管理员，默认为启用，双击，在弹出选项中，设置为禁用
- 重启计算机

至此，问题解决，再次运行mongodb时，成功!
