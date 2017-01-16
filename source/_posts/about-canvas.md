---
title: canvas基础记录
date: 2016-10-24 17:20:35
tags: [html5,canvas]
categories: tools
---
本文主要记录canvas的基础知识和一些小例子，按自己的理解和学习记录，可能也一些凌乱，也在不断更新，希望在不断学习中能做出自己想要的效果。
<!-- more --> 

HTML5 canvas标签用于绘制图像（通过脚本，通常是 JavaScript）。
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
	
fillStyle：填充样式：
1、color
2、渐变色gradient
超过画布后，均是结尾色
线性渐变色： （定义在两点之间）
直线型
	var grd = context.createLinearGradient(xstart,ystart,xend,yend);//渐变线：定义方向和尺度
 	grd.addColorStop(stop,color); //(起始位置,颜色）；可添加无数个
	
	(0,0,0,200)竖直渐变 数值可为负值
	(0,0,200,0)水平渐变 修改查看效果

以下例子：从左上角（0，0）黑色到右下角（200,200）白色线性渐变
	var grd = context.createLinearGradient(0,0,200,200);
	grd.addColorStop(0.0,'#000');
	grd.addColorStop(1.0,'#fff');

	context.fillStyle= grd;
	context.fillRect(0,0,200,200);

作用：景深、
径向渐变色：（定义在同心园内）
放射型
	var grd = context.createRadialGradient(x0,y0,r0,x1,y1,r1); 
	grd.addColorStop(stop,color);
	
以下例子：以中心（100,100）半径0即黑色点到（100,100）半径100白色的向外放射渐变
	var grd = context.createRadialGradient(100,100,0,100,100,100);
	grd.addColorStop(0.0,'#000');
	grd.addColorStop(1.0,'#fff');
	
	context.fillStyle= grd;
	context.fillRect(0,0,200,200);
3、图片
	createPattern(img,repeat-style);
以下例子：以1.png重复铺满(200,200)的矩形
	bgImg.src='img/1.png';
	bgImg.onload = function(){
		var pattern = context.createPattern(bgImg,'repeat');
		context.fillStyle = pattern;
		context.fillRect(0,0,200,200);
	}
4、画布
	createPattern(canvas,repeat-style);

5、video
	createPattern(video,repeat-style);

#### 多边形 ####
	
	context.moveTo(100,100); 
    context.lineTo(700,700); 
    context.lineTo(100,700);
    context.lineTo(100,100); //首尾相连

    context.fillStyle ='rgb(2,100,30)';
   	context.fill();  //设置或返回用于填充绘画的颜色、渐变或模式

#### 弧线\圆形\曲线 ####
	context.arc(x,y,r,sAngle,eAngle,counterclockwise); //单位弧度
![](http://i.imgur.com/9EKJazN.png)
图片来源：[HTML5 canvas arc() 方法](http://www.w3school.com.cn/tags/canvas_arc.asp)


	arcTo() 创建两切线之间的弧/曲线
	context.moveTo(x0,y0);
	context.arcTo(x1,y1,x2,y2,r);
起始点（x0,y0）：之前线的终点，绘制起点，但不一定是切点，圆弧会找到切点开始绘制
结束点：x2y2是与x1y1组成一条切线（辅助线），最终圆弧结束于切点的位置
切点不一定在两条切线上

	quadraticCurveTo() 创建二次贝塞尔曲线 

	context.moveTo(x0,y0);
	context.quadraticCurveTo(x1,y1,x2,y2);
起点就是（x0，y0）,终点(x2,y2)同时也是切点;控制点(x1,y1)

![](http://i.imgur.com/z41db1X.png)
	
	bezierCurveTo() 创建三次方贝塞尔曲线
	
	context.moveTo(x0,y0);
	context.bezierCurveTo(x1,y1,x2,y2,x3,y3);

x1,y1,x2,y2 控制点 ；,x3,y3结束点

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

**.clearRect(x,y,width,height)**:清空给定矩形内的指定像素。。//通常用于动画

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

3 .translate(x,y) 重新映射画布上的 (0,0) 位置至（x,y）
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

### 文字 ###
	context.font = 'font-style font-variant font-weight font-size font-family'
	context.font ="20px sans-serif";//默认值
	context.textAlign = 'left center right'
	context.textBaseline = 'top middle bottom alphabetic(默认)'
	context.fillText(string,x,y,[maxlen]); //填充 (文字，位置,[最宽，强行压缩短])  
	
	context.strokeText(string,x,y,[maxlen]); //描边
	
	文本度量：
	context.measureText(string).width //返回渲染string的宽度

阴影

context.shadowColor  //阴影颜色
context.shadowOffsetX //可正可负
context.shadowOffsetY

context.shadowBlur //虚化模糊

context.globalAlpha //透明度，默认1，全局

context.globalCompositeOperation="source-over";

性设置或返回如何将一个源（新的）图像绘制到目标（已有）的图像上。
源图像 source-= 打算放置到画布上的绘图。
目标图像  destination = 已经放置在画布上的绘图。
source-over
source-atop
source-in
source-out

destination-over ：先绘制的在后绘制的上
destination-atop
destination-in ：只绘制先绘制图形，但
destination-out

lighter
copy
xor
**其他**
剪辑区域
context.clip()
提示：一旦剪切了某个区域，则所有之后的绘图都会被限制在被剪切的区域内（不能访问画布上的其他区域）。您也可以在使用 clip() 方法前通过使用 save() 方法对当前画布区域进行保存，并在以后的任意时间对其进行恢复（通过 restore() 方法）。

非零环绕原则
context.isPointInPath(x,y); 方法返回 true，如果指定的点位于当前路径中；否则返回 false。



### canvas图形库推荐 ###

### 参考 ###
[HTML 5 Canvas 参考手册](http://www.w3school.com.cn/tags/html_ref_canvas.asp)