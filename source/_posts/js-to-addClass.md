---
title: 原生JS实现addClass、removeClass功能
date: 2017-01-02 19:59:54
tags: [JS]
categories: note
comments: true
---
在jQuery中通常给元素添加class使用addClass()方法，移出使用removeClass()方法，很方便，但在原生JS中没有这样的方法，需要我们自己定义方便使用。
<!-- more -->
### 基础 ###
该部分主要是归纳在JS中常用的设置style和class的方法。

	<div id="demo"></div>
		
#### JS设置style ####
	
	document.getElementById("demo").style.color = "#000";
	

#### JS设置class方法 ####
**方法一：**

	el.setAttribute('class','demo');
	document.getElementById("demo").setAttribute("class", "demo");  

问题：IE6/7不支持setAttribute('class',xxx)方式设置元素的class。
**方法二：**

	el.setAttribute('className', 'demo');
	document.getElementById("demo").setAttribute("className", "demo");
	
问题：IE8/9/10/Firefox/Safari/Chrome/Opera不支持setAttribute('className',xxx)方式设置元素的class。
**方法三：**

	el.className = 'demo';
	document.getElementById("demo").className("demo");
最完美：所有浏览器都支持。

注：‘demo’为要添加的class的值。

### 实现 ###
该部分主要实现addClass和removeClass的功能。

	function hasClass( elements,cName ){    
		return !!elements.className.match( new RegExp( "(\\s|^)" + cName + "(\\s|$)") );   
	};    
	function addClass( elements,cName ){    
		if( !hasClass( elements,cName ) ){    
			elements.className += " " + cName;    
	  	};    
	};    
	function removeClass( elements,cName ){    
	    if( hasClass( elements,cName ) ){    
	        elements.className = elements.className.replace( new RegExp( "(\\s|^)" + cName + "(\\s|$)" ), " " );  
	    };    
	}; 

### 使用 ###

	<script type="text/javascript">
		var demo = document.getElementById("demo");
		addClass(demo,"class1");  //给demo元素添加class1
		removeClass(demo,"class1");  //demo元素移出class1
	</script>