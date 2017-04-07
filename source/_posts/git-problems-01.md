---
title: git无法pull仓库refusing to merge unrelated histories 
date: 2017-02-21 10:19:20
tags: [Git]
categories: tools
---
今天在pull一个项目代码时，出现refusing to merge unrelated histories，查阅后发现，是因为本地的代码和远程仓库没有共同祖先，无法pull和push，都会报错。
<!-- more -->
### 报错 ###
修改完本地后，进行push时，遇到：
![](http://i.imgur.com/meDtELE.png)
然后想到的就是直接pull下远程仓库，后来就遇到下面这个问题
![](http://i.imgur.com/Dn4pmtf.png)

### 解决 ###
最后解决采用的是网上很多人建议的解决办法，顺利解决了。

	git pull origin master --allow-unrelated-histories

表示允许不相关的仓库合并。
