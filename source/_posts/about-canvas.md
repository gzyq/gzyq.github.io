---
title: canvas基础
date: 2016-10-28 20:28:48
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
	
fillStyle：

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

演示地址：

**.save()** 保存当前图形状态（包括所有状态）
**.restore()** 返回save节点时canvas所有的状态

在.save()和.restore()直接随意更改设置，不影响后面的绘制效果

### 图形变换 ###
1 .scale(sx,sy) 缩放
**注**：对绘图进行缩放，所有之后的绘图也会被缩放。定位也会被缩放。

如：scale(2,2)，那么绘图将定位于距离画布左上角两倍远的位置。
以下面代码为例，第一个矩形：边框2，从(5,5)开始绘制，长25宽15；放大2后，第二个，边框4，从(10,10)开始绘制，长50宽30；
	context.lineWidth=2；
	context.strokeRect(5,5,25,15);
	context.scale(2,2);
	context.strokeRect(5,5,25,15);

2 .rotate(deg)旋转当前的绘图
	
	context.rotate(20*Math.PI/180);
	context.fillRect(5,5,25,15);

3 .translate(x,y) 重新映射画布上的 (0,0) 位置
**注**：在 translate() 之后调用诸如 fillRect() 之类的方法时，值会添加到 x 和 y 坐标值上。
以下为例：在位置 (10,10) 处绘制一个矩形，将新的 (0,0) 位置设置为 (70,70)。再次绘制新的矩形（请注意现在矩形从位置 (80,80) 开始绘制）
	
	ctx.fillRect(10,10,100,50);
	ctx.translate(70,70);
	ctx.fillRect(10,10,100,50);

 
4 .transform(a,b,c,d,e,f) 替换当前的变换矩阵
**注**： 画布上的每个对象都拥有一个当前的变换矩阵；
	    transform() 允许缩放、旋转、移动并倾斜当前的环境；
		该变换只会影响 transform() 方法调用之后的绘图；
		调用多次效果是级联的。

	变换矩阵     其中：()为默认值
	a  c  e     a 水平缩放(1)  c 垂直倾斜(0)  e 水平位移(0)
	b  d  f     b 水平倾斜(0)  d 垂直缩放(1)  f 垂直位移(0)
	0  0  1

5 .setTransform()忽略掉之前所有的transform，将当前的变换矩阵设为单位矩阵，再进行后面。
**注**：setTransform() 方法把当前的变换矩阵重置为单位矩阵，然后以相同的参数运行 transform()；
setTransform() 允许您缩放、旋转、移动并倾斜当前的环境。
































### 参考 ###
[HTML 5 Canvas 参考手册](http://www.w3school.com.cn/tags/html_ref_canvas.asp)