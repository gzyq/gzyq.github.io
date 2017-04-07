---
title: 原生JS动态加载外部css/js文件
date: 2017-03-18 19:59:54
tags: [JS]
categories: note
comments: true
---
一般css，js文件直接写好在了代码里面，当然也有一些情况，需要按需加载，这时候每次都去重新重写一个加载很麻烦，就直接封装成函数，使用时直接调用更加方便。
<!-- more -->
### 基础 ###
添加js需要先创建script标签，设置类型、地址，最后加入head中。

	var head = document.getElementsByTagName('HEAD')[0]; 
    var script= document.createElement("script"); 
    script.type = "text/javascript"; 
    script.src="test.js"; 
    head.appendChild(script); 


### 实现 ###

	function loadfile(filename, filetype) {
		if (filetype == "js") {
		    var fileref = document.createElement('script');
		    fileref.setAttribute("type", "text/javascript");
		    fileref.setAttribute("src", filename);
		}else if(filetype == "css") {
		    var fileref = document.createElement('link');
		    fileref.setAttribute("rel", "stylesheet");
		    fileref.setAttribute("type", "text/css");
		    fileref.setAttribute("href", filename);
		}
		if (typeof fileref != "undefined") {
		    document.getElementsByTagName("head")[0].appendChild(fileref);
		}
	}

### 使用 ###
	
	loadfile(filename, filetype);