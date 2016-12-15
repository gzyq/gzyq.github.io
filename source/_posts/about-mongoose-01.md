---
title: mongoose使用疑惑总结
date: 2016-12-15 10:15:22
tags: [note,mongoose,数据库]
---

刚开始接触mongoose，在使用过程中遇到一些疑惑，网上大多解释的比较简单，所以把这些总结一下，都是自己实践操作后的一些记录，比较通俗，适合小白，后面会随时更新。
<!-- more --> 
### mongoose操作的是哪些document ###
使用mongoose常用数据库的增删改查，但刚开始使用时对具体操作的数据表是哪些有些不清楚，下面小总结一下。

	定义Schema：schema/demo.js：
	var mongoose = require("mongoose");
	var TestSchema = new mongoose.Schema({
		    name : { type:String },//属性name,类型为String
		    age  : { type:Number, default:0 },//属性age,类型为Number,默认为0 
		    time : { type:Date, default:Date.now },
		    email: { type:String,default:''} 
		});
	module.exports = TestSchema

	发布为Model：model/demo.js：
	var mongoose = require('mongoose');
	var TestSchema= require('../schemas/demo');
	var TestModel = mongoose.model("demoDb",TestSchema); //重点部分
	module.exports = TestModel;

	创建实体：app.js
	var TestModel = require('./models/demo');
	mongoose.connect('mongodb://localhost/demo');
	var TestEntity = new TestModel({
	        name : "gzyq",
	        age  : 26,
	        email: "gzyq@qq.com"
		});
	TestEntity.save();

这是一个简单的新增数据的操作，关于开始的疑问，重点看下面粗体部分（Model内）：
**var TestModel = mongoose.model("demoDb",TestSchema);**
其中，.model()里面参数很重要，第二个TestSchema是之前定义的Schema，重点是引号内第一个参数，此处为demoDb。
当用TestModel创建实体TestEntity后，需要实现上述增加数据操作时：
**情况一：数据库demo中不包含该表，会自动创建demodbs数据表(document)。**
注：名称 —> 数据表(document) 转换规则（其他情况暂时没有遇到）:
	以字母结尾，数据表名称会自动加s，如demodb —> demodbs；
	若包含大写，自动创建的数据表自动转换为小写,如demoDB —> demodbs；
	若以数字结尾，数据表名称不变，如demodb1 —> demodb1。
**情况二：数据库demo中包含该表，则直接在对应表中新增数据。**
注：此例中，若demo数据库中包含demodbs数据表，则可以新增数据；若只包含demodb数据表，则会视为情况一处理。

