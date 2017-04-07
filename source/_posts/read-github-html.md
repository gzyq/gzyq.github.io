---
title: 如何预览GitHub项目里面的网页或Demo
date: 2017-04-07 12:40:42
tags: [GitHub]
categories: tools
comments: true
---
最近在更新hexo博客时，发现如果有直接的通过地址访问html网页的话，有一些概念或者效果更佳直观，但是自己没有服务器，不是很方便，好在GitHub可以预览存放在它里面的项目的网页或Demo，很方便的。
<!-- more -->
## 准备 ##
要访问GitHub项目里面的网页，最主要的是要把项目上传到自己对应的github仓库中，小伙伴应该都会的啦，初次尝试的可以百度下，很多教程。下面以我的一个项目DEMOs为例来说明。
准备工作完成后效果：
![](http://i.imgur.com/fLMrSUQ.png)
此时，若打开其中的html，如打开demo.html,会看到下面的效果，全是代码，相信这不是大家想要的效果，我们要做得是，通过地址栏直接访问到页面呈现效果。
![](http://i.imgur.com/dBQ4XbM.png)
## 访问 ##
准备工作做完后，就回归正题了，下面跟着指南做就可以达到想要效果了。
#### 设置Settings ####
找到Settings选项，点击进入。
![](http://i.imgur.com/I0qXUpB.png)
#### 设置GitHub Pages ####
在settings页面，找到**GitHub Pages**选项，点击 **Source** 下面的 **None** 选项，如下图示，选择**master branch**，最后点击 **Save** 按钮。
![](http://i.imgur.com/tVsFKPz.png)

设置完成后，会出现访问地址[http://gzyq.github.io/DEMOs/](http://gzyq.github.io/DEMOs/)，如下图所示：
![](http://i.imgur.com/8tiOg1A.png)
#### 地址 ####
如果直接打开上面的地址是仓库下面，README的内容，如果想访问仓库下面具体的html，需要在地址后面加上要访问的文件。
**访问根目录demo.html**  [http://gzyq.github.io/DEMOs/demo.html](http://gzyq.github.io/DEMOs/demo.html)
![](http://i.imgur.com/0A0bBfv.png)
**访问setImgPositon文件夹下index.html文件** [http://gzyq.github.io/DEMOs/setImgPositon/](http://gzyq.github.io/DEMOs/setImgPositon/)
![](http://i.imgur.com/Yhhq1FJ.png)
## 后记 ##
按上面的方法就可以很方便的通过地址给别人看你的网页demo了，也不用部署服务器，对小白来说很便捷，当然缺点就是只能看一些静态网页，小遗憾。