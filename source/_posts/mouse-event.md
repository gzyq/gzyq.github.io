---
title: JS鼠标事件总汇
date: 2016-07-20 21:00:41
tags: [JS]
categories: note
---
鼠标事件是网页中常用的事件之一了，清楚了解鼠标事件对网站交互等起到重要作用，本文主要记录鼠标事件以及产生的坐标信息，希望有助于小伙伴理解。
<!-- more -->
## 事件 ##
click：在单击鼠标左键或右键时发生。  
doubleclick：在双击鼠标左键时发生。 
  
mousedown：在单击鼠标按钮（左键、右键或中键）并且尚未松开时发生。  
mouseup：在松开鼠标按钮（左键、右键或中键）时发生。

mousemove：在鼠标光标移动时发生。
mouseout：在鼠标光标离开对象时发生。   
mouseover：在鼠标光标移动到对象上时发生。

mouseenter： 鼠标移动到元元素对象范围内时触发。 
mouseleave： 鼠标移动到元元素对象范围外时触发。 
 
mousewheel：在移动鼠标滚轮时发生。  
## 顺序 ##
click顺序事件执行顺序：mousedown mouseup click

## 坐标信息 ##

## 注意 ##
#### mousemove ####
当鼠标指针在指定的元素中移动时，就会发生 mousemove 事件。mousemove事件独立于mousedown事件，并不是mousedown以后才会产生，需要注意。


## demo ##
[**水印位置设定**](http://gzyq.github.io/DEMOs/setImgPositon/)
滑动条