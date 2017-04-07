---
title: JS滑动条、进度条、拖拽
date: 2017-04-06 19:55:33
tags: [JS]
categories: note
comments: true
---
HTML5中新增了进度条标签progress，但还是有一定的局限性也不美观。本文主要记录用原生JS实现进度条、滑动条、拖拽移动的具体思路及实现，也顺便复习下鼠标事件的用法，有兴趣的小伙伴可以看下，多提宝贵意见。
<!-- more -->
## 基础须知 ##
### HTML5 progress ###
HTML5中新增的进度条和度量的用法，只想使用这个功能的表示，不需要拖动等的可以直接使用这个标签，方便快捷。

	 <progress value="33" max="100"></progress>

### JS clientX相关 ###
这次的效果涉及到clientX、offsetLeft、offsetWidth三个距离概念，需要知道，下图小做了解。
详细更多解读，请参考另一篇文章《[JS clientX\offsetLeft\scrollHeight等相关解读](https://gzyq.github.io/2017/04/09/JS-clientX/)》。
![](http://i.imgur.com/y5OrpmL.jpg)
#### JS 鼠标事件 ####
滑动条、拖拽等涉及鼠标事件主要是：mousedown、mousemove、mouseup，所以应对这三个事件有一定的了解，不清楚的请先阅读相关文章[《JS鼠标事件总汇》](https://gzyq.github.io/2016/07/20/mouse-event/)。
## 实现 ##
不管是进度条、滑动条还是拖拽，最终改变的就是元素的位置坐标或者是长宽，这一点要时刻记得。下面我们来依次看看具体实现。
### 进度条 ###
进度条属于最简单的了，只涉及到width值，当然也可以使用left值来做，我们主要看width方法。

**在线观看**：[JS进度条demo](http://gzyq.github.io/DEMOs/slide-progress-drag/progress.html)
### 滑动条 ###

**在线观看**：[JS滚动条demo](http://gzyq.github.io/DEMOs/slide-progress-drag/slide.html)

### 拖拽 ###

**在线观看**：[JS拖拽demo](http://gzyq.github.io/DEMOs/slide-progress-drag/drag.html)