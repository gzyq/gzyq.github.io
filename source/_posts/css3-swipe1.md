---
title: H5滑屏
date: 2016-07-18 20:26:44  
tags: [note,css3,动画,H5]
categories: note
comments: false
---

swiper插件：[http://www.swiper.com.cn/](http://www.swiper.com.cn/)  
slides插件：[http://slidesjs.com/](http://slidesjs.com/)
slip插件： https://github.com/binnng/slip.js  
<!-- more -->
 
- 拖拽翻屏：页面随手指拖动而移动，手指松开（touchend）后翻页  
- 滑动翻屏：页面不随手指拖动而移动，手指松开（touchend）后翻页    

 通过touchstart、touchmove、touchend 三个事件加上css3的3d变化效果配合，实现滑动切换图片  

 拖拽翻屏：通过touch事件来设置transform：translate3d（x，y，z）的参数，并在滑动结束（touchend）设置一个最小滑动距离minRange，该距离范围内的滑动，translate3d的参数等于touchmove的滑动距离，当大于minRange时， 则触发下一页（或上一页）的整体滑动，translate3d的X或Y的参数也就是视窗的宽（横向滑动时）或者高（纵向滑动时）  
translate3d可以主动开启手机GPU加速渲染，页面滑动更流畅
 
ontouchend:手指离开屏幕时，计算屏幕最终停留在哪一页。


参考：  
[H5单页面手势滑屏切换原理](http://www.cnblogs.com/onepixel/p/5300445.html?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)  
http://tid.tenpay.com/labs/dikamon/dikamon.html   
