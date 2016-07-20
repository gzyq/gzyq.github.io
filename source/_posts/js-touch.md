---
title: 移动端JS触摸事件
date: 2016-07-18 21:20:09 
tags: [note,JS,移动端]
categories: note
comments: false
--- 

## 触摸事件：   
 （都会冒泡，也可以取消）  
- touchstart——当手指触碰屏幕时候发生。不管当前有多少只手指
- touchmove——当手指在屏幕上滑动时连续触发。通常我们再滑屏页面，会调用event的preventDefault()可以阻止默认情况的发生：阻止页面滚动  
- touchend——当手指离开屏幕时触发  
- touchcancel——当系统停止跟踪触摸时候会触发。例如在触摸过程中突然页面alert()一个提示框，此时会触发该事件，这个事件比较少用（例如电话接入或者弹出信息。一般用在游戏：玩着的时候，突然来电话了，就触发touchcancel事件暂停游戏、存档等操作。）
<!-- more -->
## 跟踪触摸的属性 ：   
- touches：当前跟踪的触摸操作的Touch对象的数组，即屏幕上所有手指的信息  
- targetTouches：特定于事件目标的Touch对象的数组，即手指在目标区域的手指信息  
- changedTouches：自上次触摸以来发生了什么改变的Touch对象的数组，即最近一次触发该事件的手指信息   

注：touchend时，touches与targetTouches信息会被删除，changedTouches保存的最后一次的信息，最好用于计算手指信息  

## 每个Touch对象的属性 ： 
-  target：触摸的DOM节点目标 
-  identifier：表示触摸的唯一ID   
-  clientX：触摸目标在<b style='color:red;'>视口</b>中的X坐标  （触摸点相对浏览器窗口的位置，client不包含滚动距离）
-  clientY：触摸目标在<b style='color:red;'>视口</b>中的Y坐标   
-  pageX：触摸目标在<b style='color:red;'>页面</b>中的X坐标  （触摸点相对于页面的位置，包含滚动距离） 
-  pageY：触摸目标在<b style='color:red;'>页面</b>中的Y坐标  
-  screenX：触摸目标在<b style='color:red;'>屏幕</b>中的X坐标  （触摸点相对于屏幕的位置）
-  screenY：触摸目标在<b style='color:red;'>屏幕</b>中的Y坐标
-  radiusX：画出大约相当于手指形状的椭圆形，椭圆形的两个半径中x
-  radiusY：画出大约相当于手指形状的椭圆形，椭圆形的两个半径中y
-  rotationAngle：画出大约相当于手指形状的椭圆形，旋转角度。
  

        e.target;   //触摸元素为p，则返回[object HTMLParagraphElemet]，目标内容
    			    //触摸元素为div,则返回[object HTMLDivElemet]

## 触摸事件的响应顺序   
1. ontouchstart   
2. ontouchmove   
3. ontouchend   
4. onclick    
  
## 移动端click屏幕产生200-300 ms的延迟响应  

## 注意： 

手指在滑动整个屏幕时，会影响浏览器的行为，比如滚动和缩放。所以在调用touch事件时，要注意禁止缩放和滚动。

**1.禁止缩放**

通过meta元标签来设置。

<meta name="viewport" content="target-densitydpi=320,width=640,user-scalable=no">

**2.禁止滚动**

preventDefault是阻止默认行为，touch事件的默认行为就是滚动。

event.preventDefault();    

## DEMO： ##
	
	<div id='demo'></div>
	<div class='slide'>
		<ul>
			<li>2</li>
			<li>3</li>
			<li>4</li>
		</ul>
	</div>

    var moveX = 0,px = 0;			
    document.getElementsByClassName('slide')[0].addEventListener('touchstart', function(e) {
    					
   		console.log(e.target); //[object HTMLDivElemet]			
		console.log(e.changedTouches[0]); //包含所有信息
		
		document.getElementById("demo").innerHTML = '触摸开始';
		
		var cx = e.touches[0].clientX;
		console.log('touchstart' + cx);

		px = e.touches[0].pageX;
		console.log(px);

		var sx = e.touches[0].screenX;
		console.log(sx);
	});
	
	document.getElementsByClassName('slide')[0].addEventListener('touchmove', function(e) {
		e.preventDefault();

		console.log(e.changedTouches[0]);
		document.getElementById("demo").innerHTML = '触摸移动中';

		moveX = e.touches[0].pageX - px;
		console.log(movex);

		if(moveX > 50) {
			console.log('触摸移动过程中，此刻大于50');
		} else {
			console.log('触摸移动过程中，此刻小于50');
		}
	});

	document.getElementsByClassName('slide')[0].addEventListener('touchend', function(e) {
		document.getElementById("demo").innerHTML = '结束' + 'end';
		console.log(moveX);

		if(moveX > 20) {
			console.log('结束时大于20');
		} else {
			console.log('结束时小于20');
		}
	});




