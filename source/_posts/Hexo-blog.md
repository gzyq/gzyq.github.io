---
title: Hexo Blog搭建流程
date: 2016-07-11 19:37:30
tags: [hexo,note]
categories: note
comments: true
---
初次使用hexo搭建博客，因为对github也不是很熟，网上找了不少资料，花了一个星期才把整个流程，包括后续更新修改搞明白，记录下来，方便查阅，后续有新的经验再更新。
<!-- more -->
# Git #
下载并安装Git，设置用户名邮件地址。  
已初始化过的忽略此处
# Github #
要使用[GitHub Pages](https://github.com/) + [Hexo](https://hexo.io/zh-cn/)搭建免费的博客,需要在自己的Github账号下创建一个新的仓库，且命名为 username.github.io（username是你的账号名)。  
注：网上很多文章里面，直接写在GitHub账号下创建一个新的仓库即可，最终就可以通过 http(s)://username.github.io 方式访问，这种方法是不正确的，详细区别请了解GitHub Pages的两种类型，User/Organization Pages 和 Project Pages。
# Hexo #
1. 保证电脑中已经安装Node.js和Git  
2. 开始Hexo安装，找到安装的Git，点击Git Bash，输入`$ npm install -g hexo-cli`。此时，安装完后可以在对应目录下找到安装的程序
3. 在想放置该博客目标的文件夹下，右击选择 Git Bash here,输入 `$ hexo init`，此处也可以在任意地方键入`$ hexo init <folder>`,此处<folder>指放置代码的位置，不输入默认为当前文件夹下。
4. 接着，键入`$ npm install`  ，此处是安装依赖包。
5. 此时，键入`$ hexo server`,即可在浏览器中通过[http://localhost:4000/](http://localhost:4000/)看到初始化效果了。
至此，就搭建好了最基础的本地的Hexo网站了。
# Github+Hexo #
最终目标是要通过Hexo搭建一个别人可以看到的网站，所以需要和之前的Github一起，修改安装其他内容。
找到刚刚文件夹下面的 _config.yml 文件，该文件是网站的基本配置，包括标题，副标题，作者，语言等信息，可以根据自己需求修改。此处重点是要修改deploy处，找到deploy：，修改为下面这样：

	deploy:
		type： git 
		repository: git@github.com:username/username.github.io.git  
	    branch: master

因为需要把Hexo部署到GitHub上，需要安装一个插件：
  ` $ npm install hexo-deployer-git --save `  
安装完成后，可以执行 $ hexo generate ,此时会生成一个public文件夹，里面是编译后的网站页面。  
再输入` $ hexo deploy` ，即可完成在Github上部署。  
此时，通过浏览器键入：username.github.io就可以看到效果了。
注：
1. 在配置deploy时注意，冒号：后面都有空格；
2. 再向Github提交过程中，可能出现没有SSH key的情况，重新按步骤设置[SSH key](https://help.github.com/articles/generating-an-ssh-key/) 即可；
3. 此时，在Github中看到是public文件下的内容，如果想在Github上部署前的源代码，即hexo其他内容，需要通过git add，commit等步骤提交。

# Hexo日常使用 #
参考网上多数教程里面优化部署，在hexo使用过程中，我是在github里面建立了两个分支，master和blog，master主要安置的内容是public，即网站及时更新后的内容，blog里面是源码，比较方便。  
在日常修改或者添加文章等操作后，通过git status查找文件变化，git add，git commit以及git push origin blog后，再在blog分支下，进行hexo generate，hexo deploy操作以更新master里面的内容，再刷新username.github.io即可看到修改效果，同时也保证了再github中记录了文件变化更新。
如果更换电脑后，需要git clone 源代码到本地后再进行其他操作。  
# 参考 #
[Hexo在github上构建免费的Web应用](http://blog.fens.me/hexo-blog-github/)  
[GitHub Pages + Hexo搭建博客](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/#more)

