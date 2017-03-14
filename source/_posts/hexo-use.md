---
title: Hexo日常使用
date: 2016/7/14 22:28:42 
updated: 2017/3/13 20:11:29 
tags: [hexo]
categories: hexo
comments: true
---
Hexo next使日常使用中一些命令及理解，供大家参考。
<!-- more -->
### 阅读全文图标 ###
有些文章的内容较多，在首页展示时只想展示部分内容，其余部分隐藏，当点击阅读全文时调转至完整部分，在部分展示内容结尾处，增加以下代码即可。
	
	 <!-- more -->

### 更换网站ico图标 ###
将网站图标命名favicon.ico，放至根目录/source下， 在_config.yml中新增 **favicon: /favicon.ico **即可。

	favicon: /favicon.ico

### 更换主题 ###
在网上下载更多主题（如：hexo-theme-next-master）后，需要将下载的主题放在themes文件夹下，通过修改根目录下_config.yml文件即可：

	theme: hexo-theme-next-master

### 新建 ###

	hexo new 'postName'	新建文章
	hexo new page 'pageName'	新建页面（如关于页，标签页）

### 文章属性 ###
可以根据自己的需要，选择下面属性。

	title: Hexo日常使用        //标题
	date: 2016/7/14 22:28:42  //创建时间
	tags: [hexo]              //标签,必须写在[]内，多个用,隔开
	categories: hexo          //分类
	comments: true            //是否允许评论
	description: Hexo日常使用Hexo日常使用  //描述

### 部署 ###
   
	hexo generate 生成静态页面至public目录下
	hexo deploy 将.deploy目录部署到github 

### 本地预览 ###
	hexo server  开启预览访问（默认端口4000）

### 更新流程 ###
平时使用最多的就是修改和新增文章，以下是我自己使用hexo的理解，以我的博客为例：
1、按上面所说的hexo new即可，再选择平时常用的编辑器进行文章编辑，如Markdown。

2、对新建文章进行部署（deploy的过程，实际上更新了master分支的内容，一旦进行deploy，在网站上（或本地运行hexo server，通过http://localhost:4000/ ）就可以看见修改后的效果了）。
**注**：部署的过程，实际上远程仓库的master分支同步更新。

3、如果是修改文章，在修改时可以利用编辑器的浏览器预览功能或者直接通过开启本地预览访问，通过访问本地端口，实时刷新查看修改效果至编辑满意为止。

4、因为日常使用，不一样一直是在一个电脑中操作，所以需要实时将网站源码保存到远程仓库，以防意外。在网站更新部署完成后，通常，会将blog分支下内容进行更新。
具体操作为：通过git status，git add，git commit，git push origin blog同步更新变化。


