---
title: canvas基础
date: 2016-10-28 20:28:48
updated: 2017-01-12 14:28:48
tags: [html5,canvas]
categories: html5
comments:true
---
本文主要记录canvas的基础知识和一些小例子，按自己的理解和学习记录，可能也一些凌乱，也在不断更新，希望在不断学习中能做出自己想要的效果。
<!-- more --> 
HTML5 <canvas> 标签用于绘制图像（通过脚本，通常是 JavaScript）。
canvas是基于状态的绘图，先有状态，后有绘制(先准备要画什么)。

canvas直接给宽高，和js给宽高区别：
不建议给css指定，css指定的是画布的显示的大小
而canvas还包括里面显示分辨率的大小

也可以在js中设置宽高（后面会写到）

### 初始化 ###

	JS：
	var canvas = document.getElementById('canvas');
	var context = canvas.getContext('2d'); //使用context进行绘制

### 画线 ###
**.lineWidth**：设置或返回画笔粗细
**.strokeStyle**:设置或返回用于笔触的颜色、渐变或模式
**.lineCap**:设置或返回线条的结束端点样式
——butt(默认，平直边缘)，round(末端为圆形)，square(正方形)
**.lineJoin** 属性设置或返回所创建边角的类型，当两条线交汇时。
——miter(默认，创建尖角)，round(圆角)，bevel(斜角)
**miterLimit**：只有当 lineJoin 属性为 "miter" 时，miterLimit 才有效

**.beginPath()**：开始一个全新的绘制,即起始一条路径，或重置当前路径 
**.moveTo()**:不从任何点开始，直接指定一个新的坐标点
**.lineTo()**:从上一个坐标点一直画到当前lineTo表示的坐标点
**.stroke()**:绘制已定义的路径
**.closePath()**：创建从当前点到开始点的路径

	context.lineWidth =5 ; //粗细
    context.strokeStyle = '#005588';//颜色
	ctx.lineCap="round";

	context.moveTo(100,100); //笔尖放在（100,100）
    context.lineTo(700,700); //从（100,100）绘制到（700,700），以上操作，都为意图绘制并未开始画

    context.stroke(); //绘制线条

### 填充 ###
**.fillStyle**="color" 设置或返回用于填充绘画的颜色、渐变或模式
**.fill()**; //填充

	context.fillStyle = "#ffccff"; 
    context.fill();

#### 多边形 ####
	
	context.moveTo(100,100); 
    context.lineTo(700,700); 
    context.lineTo(100,700);
    context.lineTo(100,100); //首尾相连

    context.fillStyle ='rgb(2,100,30)';
   	context.fill();  //设置或返回用于填充绘画的颜色、渐变或模式

#### 弧线\圆形 ####


### 实例 ###
#### 七巧板demo ####
源码地址：[https://github.com/gzyq/html5-canvas/tree/master/canvas-demo-1](https://github.com/gzyq/html5-canvas/tree/master/canvas-demo-1)
#### 时钟demo #### 
源码地址：[https://github.com/gzyq/html5-canvas/tree/master/canvas-demo-2](https://github.com/gzyq/html5-canvas/tree/master/canvas-demo-1)


绘制矩形：
方法一：
cxt.moveTo(x,y);
cxt.lineTo(x+width,y);
cxt.lineTo(x+width,y+height);
cxt.lineTo(x,y+height);

方法二：
**cxt.rect(x,y,width,height)**; //矩形路径

**cxt.fillRect()**：直接用fillStyle绘制填充的矩形
**cxt.strokeRect()**：//直接用strokeStyle绘制带框的矩形

**.clearRect(x,y,width,height)**:清空给定矩形内的指定像素。

	ctx.beginPath();
	ctx.lineWidth="6";
	ctx.strokeStyle="red";
	ctx.rect(5,5,290,140);
	ctx.stroke();

绘制五角星：
	
	<canvas id="canvas" width="200" height="200">
		当前浏览器不支持canvas，请更换浏览器后再试。
	</canvas>
	
	var canvas = document.getElementById('canvas');
	var context = canvas.getContext('2d');
	var R1 = 90;  //可更改看不同效果
	var R2 = 50;

	context.lineWidth = 3;
	context.beginPath();
	for(var i=0;i<5;i++){
		context.lineTo( Math.cos((18+i*72)/180*Math.PI)*R1+100,
					    -Math.sin((18+i*72)/180*Math.PI)*R1+100); //外侧

		context.lineTo( Math.cos((54+i*72)/180*Math.PI)*R2+100,
					    -Math.sin((54+i*72)/180*Math.PI)*R2+100); //内侧
		//()/180*Math.PI 将角度转换为弧度
		//+100:将中点挪到（100,100）画布中间
	}

	context.closePath();
	context.stroke();

