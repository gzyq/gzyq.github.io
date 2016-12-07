---
title: mongoDB常用命令行操作
date: 2016-12-06 10:25:32
tags: 
---

在MongoDB数据库中，collection(集合)即为通常所说的数据库中的表，文档（document）即数据库中的行,一个database中可以有多个collection（一个数据库可以有多个表），一个collection中又可以有多个document（一个表可以有多行数据）。
MongoDB不需要严格遵守先建库，建表等以后再进行各种操作。
<!-- more -->
### 库操作 ###
查看所有数据库(会显示当前所有数据库的名字和内存大小)：`show dbs`
![](http://i.imgur.com/SBgUba7.png)
**说明：**默认存在两个数据库：admin（存放管理员信息的数据库），local（存放replication相关的数据）;其实数据库大小只是粗略情况，不准确，数据很少情况下显示0.000G。
新建数据库：`use <newdbname>`（如果数据库不存在，则创建，否则切换至指定数据库）
查看当前数据库名称：`db`
![](http://i.imgur.com/pjHVQ6F.png)
可以看到，在新建chat数据库后，再一次使用 show dbs查看所有数据库时，并没有我们新建的chat数据库，此时，需要向里面插入一些数据（后面会说到插入），再次查看时就有了新建的chat数据库了。
删除数据库：`db.dropDatabase()`
新建表：`db.createCollection('collection')`
![](http://i.imgur.com/TBCRVi8.png)
### 插入操作 ###
注：col为此处的集合名称，即通常说的表名
1、`db.col.insert(data)`;
![](http://i.imgur.com/xuMdd36.png)
2、`db.col.save(data)`;
![](http://i.imgur.com/EKoLbua.png)
**说明：**_id，是默认生成，每行数据都存在，默认为ObjectID
区别：db.col.insert()方法指定_id字段值，会报错；db.col.save()可以指定_id字段的值，若存在更新相应数据。在不指定_id字段时，两者相同。
### 删除 ###
删除数据：`db.col.remove(条件)`
![](http://i.imgur.com/UlNdVUM.png)
删除所有数据：`db.col.remove({})`
删除某个集合：`db.<collectionName>.drop()`
### 查询 ###
查询表中的数据(非结构化的方式显示所有文档)：`db.col.find(条件)`
查询表中的数据(格式化的方式显示所有文档,易读)：`db.col.find().pretty()`
查询表中的一条数据（返回第一个文档）：`db.col.findOne(条件)`
![](http://i.imgur.com/ksaRDO8.png)
读取指定数量的数据记录：``db.col.find().limit(数量)`
跳过指定数量的数据记录：db.col.find().skip(数量)`
**查询条件：{key：{$op:value}}**
比较查询：
`等于：{<key>:<value>}
小于：{<key>:{$lt：<value>}}
小于等于：{<key>:{$lte:<value>}}
大于：{<key>:{$gt:<value>}}
大于等于：{<key>:{$gte:<value>}}
不等于：{<key>:{$ne:<value>}}`

实例：
获取col集合中"likes"大于100的数据 `db.col.find({likes:{$gt:100}})`
注：类似于SQL：Select * from col where likes>100

获取集合col集合中"likes"大于100，小于200的数据 `db.col.find({likes:{$lt:200,$gt:100}})`
注：类似于SQL：Select * from col where likes>100 AND likes<200

多条件查询：可以传入多个键（key），每个键（key）以逗号隔开。
{key1:value1,key:value2,...}
选择查询：{$or:[{key1:value1},{key2:value2}]}
其他：
$type操作符：{key:{$type:number}}
常用：Double(1),String(2),Object(3),Array(4),Date(9),Null(10)等
实例：
查询col集合中title为String类型的数据：
db.col.find({"title":{$type:2}})
### 修改 ###
语法格式：db.col.update(<query>,<update>,{upsert:<boolean>,multi:<boolean>,writeConcern:<document>});
参数说明：
query : update的查询条件，类似sql update查询内where后面的。
update : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
upsert : 可选，默认false（不插入）。表示如果不存在update的记录，是否插入objNew,true为插入，
multi : 可选，默认false，表示只更新找到的第一条记录，true表示把按条件查出来多条记录全部更新。
writeConcern :可选，抛出异常的级别。

常用：按指定条件修改：db.col.update({"条件字段名"："字段值"},{$set:{"要修改的字段名":"修改后的字段值"}});
![](http://i.imgur.com/vj4W3b2.png)

实例：
只更新第一条记录：db.col.update({"count":{$gt:1}},{$set:{"test2":"OK"}});
全部更新：db.col.update({"count":{$gt:3}},{$set:{"test2":"OK"}},false,true);
只添加第一条：db.col.update({"count":{$gt:4}},{$set:{"test5":"OK"}},true,false);
全部添加进去：db.col.update({"count":{$gt:5}},{$set:{"test5":"OK"}},true,true);
全部更新：db.col.update({"count":{$gt:15}},{$inc:{"count":1}},false,true);
值更新第一条记录：db.col.update({"count":{$gt:10}},{$inc:{"count":1}},false,false);

### 排序 ###
sort()排序，通过参数指定排序方式：1(升序,默认)，-1(降序)
db.col.find().sort({key:1})
### 索引 ###
ensureIndex()方法创建索引，key为要创建的索引字段，1(升序),-1(降序)  `db.col.ensureIndex({key:1})`
实例：
db.col.ensureIndex({"title":1})
### 聚合 ###
aggregate(),主要用于处理数据，如统计平均值，求和等，并返回计算后的结果。类似SQL中count(*)。（后期使用时再详细学习）

### 其他 ###
查看数据库具体情况：db.stats();
![](http://i.imgur.com/W1w1mKv.png)
查看各collection的状态：db.printCollectionStats()