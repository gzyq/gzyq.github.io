---
title: JQuery的ready函数与JS的onload的区别
date: 2016-12-09 13:59:34
tags: [note,JS,JQuery]
---

总体来说，window.onload必须等到页面包括图片的所有元素加载完毕后才能执行，$(document).ready()是DOM结构绘制完毕后就执行，不必等到加载完毕。