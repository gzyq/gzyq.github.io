---
title: JS插件的写法总结
date: 2017-01-15 19:59:54
tags: [JS,插件]
categories: note
comments: true
---
大部分前端应该用过很多别人的插件，经常用到效果，可以自己尝试封装成插件，可以减少很多复制粘贴的工作，大家可以多查看一些网上插件的写法，总结一套适合自己的构建起来，尝试一下，收获很多。
<!-- more -->
### jQuery ###
为方便用户创建插件，jQuery提供了jQuery.extend()和jQuery.fn.extend()方法。
jQuery.extend和jQuery.fn.extend
#### jQuery.extend() ####
jQuery.extend()的调用并不会把方法扩展到对象的实例上，引用需通过jQuery类来实现，也就是说是用于扩展jQuery类本身，增加新的静态方法。使用时，使用类名.方法的调用方式。(可用jQuery.ajax()帮助理解)。

	jQuery.extend({
		max: function(a,b){
			return a>b?a:b;
		}
	});
	
	var maxN = $.max(2,3); //3

#### jQuery.extend()的重载 ####

	jQuery.extend([deep], target, object1, [objectN])

作用：主要是自定义插件参数去覆盖插件的默认参数。
参数：  deep   可选。如果设为true，则递归合并。
      target   待修改对象。
   	object1:   待合并到第一个对象的对象。
    objectN:   可选。待合并到第一个对象的对象。

eg： 
jQuery.extend(defaults, options); //合并defaults和options，修改并返回defaults

	var defaults = { validate: false, limit: 5, name: "foo" };
	var options = { validate: true, name: "bar" };
	jQuery.extend(defaults, options); // defaults == { validate: true, limit: 5, name: "bar" }

jQuery.extend(empty, defaults, options);//合并defaults和options，不修改defaults，待修改empty

	var empty = {};
	var defaults = { validate: false, limit: 5, name: "foo" };
	var options = { validate: true, name: "bar" };
	var settings = jQuery.extend(empty, defaults, options);
	
	结果：
	settings == { validate: true, limit: 5, name: "bar" } 
	empty == { validate: true, limit: 5, name: "bar" }


#### jQuery.fn.extend ####
jQuery.fn.extend()的调用把方法扩展到对象的prototype上，实例化一个jQuery对象时，它就有了这些方法。
jQuery.fn = jQuery.prototype ,即jQuery对象的原型，也就是说jQuery.fn.extend()方法是扩展jQuery对象的原型方法，相当于为jQuery类的实例添加成员函数。
	
	$.fn.extend({
		alertClick:function(){
			alert(1);
		}
	});
	
	$("div").alertClick(); //1

### 封装插件 ###
1、定义一个闭包区域，防止污染。

	(function($){})(jQuery);

2、jQuery.fn.extend()扩展jQuery方法，制作插件

	(function($){
		$.fn.extend({
			alertClick:function(options){
				alert(1);
			}
		});

	})(jQuery);

3、设置插件的默认参数

	(function($){
		$.fn.extend({      
			alertClick:function(options){
				var options =  $.extend(defaults, options);

				this.each(function(){  //此处this指jQuery对象
					//遍历，当调用此插件的是一个集合的时候。
        			var $this = $(this); //获取当前dom 的 jQuery对象，这里的this是当前循环的dom
        			//....
				});
			}
		});

		var defaults = {
			path: 'face/',
    		button: "moreblack"
        }

	})(jQuery);

4、支持链式调用
有些时候，需要在调用自定义插件方法之后，调用其他函数，需要将jQuery对象返回。
	
	return this.each(function(){ 
				//...
			});

5、扩展
公共方法

	$.fn.alertClick.format = function (str) {
	  return "<strong>" + str + "</strong>";
	}

### JS ###
#### 类方式 ####
面向对象的思想，用类方式

	//自定义类	
	function plugin(){}
	
	//提供默认参数
	plugin.prototype.str = "default";
	
	//提供方法（如果不传参，则使用默认参数）
	plugin.prototype.firstFun = function(str = this.str){
		//alert(str);
	}
	
	//创建“对象”
	var p = new plugin();
	
	//调用方法
	p.firstFunc("hello"); //hello
	p.firstFunc(); //default

#### 闭包 ####
使用自执行的匿名函数/闭包：

	(function($){})(jQuery);

好处：创建闭包避免全局依赖，兼容jQuery操作符$和jQuery,避免第三方破坏。

	 (function(){
	    //定义一些默认参数
	    var _options={
	        default_word:"default hello"               
	    }
	 
	    //定义一些api
	    var _plugin_api = {
	        firstFunc:function(str = _options.default_word){
	            alert(str);
	            return this;//返回当前方法
	        },
	        secondFunc:function(){
	            alert("secondFunc");
	            return this;//返回当前方法
	        }
	    }
	    //这里确定了插件的名称
	    this.CJPlugin = _plugin_api;
	})();
	 
	CJPlugin.firstFunc("hello");//hello
	CJPlugin.firstFunc();//default hello
	CJPlugin.secondFunc();//secondFunc

### 参考 ###
[jQuery插件编写步骤详解](http://www.jb51.net/article/85798.htm)





