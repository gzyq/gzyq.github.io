---
title: 理解$(function(){})与(function($){})(jQuery)区别
date: 2017-02-14 15:21:06
tags: [JS]
categories: note
---
本文主要是理解归纳$(function(){})与(function($){})(jQuery)的区别以及使用。
<!-- more -->
## $(function(){}) ##
$(function(){})写法与以下几种相同：
	
	$(function(){
		//简写版...
	}); 

	$(document).ready(function(){
		//...
	});

## (function($){})(jQuery) ##
### 理解 ###
可以理解为立即执行匿名函数(function(){})()，其中传递jQuery对象。
(function($){…})(jQuery)，是形参使用$(主要是为了不与其他库冲突)；而实参用jQuery。

	(function($){
		//...
	})(jQuery);
	
	var fn = function($){
			//...
		};
	fn(jQuery);
	
	function fn($){
		//...
	};
	fn(jQuery);
### 作用 ###
作用：形成闭包。
在(function($){…})(jQuery)内定义的函数和变量只能在此范围内有效。

## 使用 ##
### 执行顺序 ###
在以下几个都出现在js中时，执行先后顺序如下：
1. (function($){})(jQuery)  //最先
2. $(function(){});
3. window.onload=function(){}; 
4. $(window).load(function(){});
详细顺序请查阅另一篇相关文章 [JQuery的ready、JS的load、JQuery的load使用区别 ](https://gzyq.github.io/2016/12/09/The-difference-between-the-JQuery-s-ready-function-and-JS-onload/)

### 开发插件应用 ###
$(function(){});用于存放操作DOM对象的代码，执行代码时DOM对象已经存在，所以不能用于存放开发插件的代码。主要因为Jquery对象没有得到传递，外部通过jQuery.method也调用不了其中的方法函数。

(function($){…})(jQuery)；可用于存放开发插件的代码。其执行时DOM不一定存在，使用时要注意。


