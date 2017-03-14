---
title: JQuery的ready、JS的load、JQuery的load使用区别
date: 2016-12-09 13:59:34
tags: [JS]
categories: note
---
平时在使用JS或者Jquery过程中，通常都会遇到ready、load这些加载，特别是和其他项目人员整合代码过程中，用于用的不一，导致很多不必要的错误出现，现在主要整理出来JQuery的ready、JS的load、JQuery的load这些的区别和注意点，以便后面参考，会不断更新，希望大家指正。
<!-- more -->
## JQuery的ready函数与JS的load的区别 ##
总体来说，window.onload必须等到页面包括图片的所有元素加载完毕后才能执行，$(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。ready（）执行时间早于onload。
### 写法 ###

	window.onload = function(){}

	$(document).ready(function(){}) 
	$(function(){});

### 个数 ### 
onload 不能同时写多个，多个情况下，只会执行最后定义的一个（最后一个会覆盖之前定义的）
ready方法，可以编写多个，并且都会执行（顺序执行）

### 执行时间 ###
onload必须等到页面包括图片的所有元素加载完毕后才能执行，
ready是DOM结构绘制完毕后就执行，不必等到加载完毕。

## JQuery的ready与load的区别 ##
load同js只中的load。
一般推荐使用写法如下：(不推荐使用body.onload())

	$(window).load(function(){})
	$(ele).load(function(){})

与原生js中执行一个不同，Jquery同时定义多个，顺序执行。

## JQuery load与JS的load ##
执行顺序：
情况一：若先遇到$(window).load(),则会一次性顺序执行完定义的所有$(window).load()事件，再执行window.onload。

情况二：若先遇到window.onload，则执行最后一个定义的window.onload事件，再顺序执行后面的所有$(window).load()事件。

## 注意 ##
当然，实际使用过程中需要结合具体情况做具体分析选择，下面是开发中遇到过的一些情况，需要注意。
（1）当在一个js里面，定义了onload和ready方法时，两者均有效，ready会先执行，onload后执行。

（2）当需要页面所有东西都加载完毕后再执行想调用的函数的时候，应该使用load()。

（3）在ready里面注册的事件，只要DOM就绪就会执行，此时可能元素的关联文件并未下载完成，比如，img的html已经下载完解析为DOM树，但img还未加载完毕，此时img的width或者height可能就为0。

(4)有些情况下，可能需要DOM元素加载前执行Jquery代码

	(function(){
		//do something
	})(jQuery)
注：详细可参考另一篇文章 [理解$(function(){})与(function($){})(jQuery)区别](https://gzyq.github.io/2017/02/14/jquery-001/)

## 其他 ##
浏览器渲染顺序：
1、解析html
2、加载解析外部css和style文件
3、解析并执行js脚本代码
4、构造html dom模型（标签加载完毕，标签内部如链接资源、大图未加载完的情况则忽略）   （**ready**）
5、加载图片、video、flash等外部文件  
6、页面加载完毕  （**load**）

