---
title: 深入理解JS 严格模式
date: 2017-03-22 19:44:11
tags: [JS]
categories: note
comments: true
---
今天在调试程序时，不小心使用了console.log(000000)输出，报了错“Octal literals are not allowed in strict mode”，即strict模式下不支持数字的八进制表示，也就是说log(000000)情况下，会将第一位数字默认为八进制，而js严格模式不支持所以报错。查了这个错以后，发现自己对严格模式每次只是机械的使用，理解甚少，所以准备深入总结学习一下，有不对的地方，望大神指正。
<!-- more -->
### 概念 ###
