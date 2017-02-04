---
title: ejs使用语法
date: 2017-01-04 23:26:59
tags: [ejs]
categories: note
comments: true
---

准备
<!-- more -->
### 安装 ###
$ npm install ejs --save-dev
### 使用 ###
<% %> 用于控制流
<%= %> 用于转义的输出
<%- %> 用于非转义的输出

<% 'Scriptlet' 标签, 用于控制流，没有输出
<%= 向模板输出值（带有转义）
<%- 向模板输出没有转义的值
<%# 注释标签，不执行，也没有输出
<%% 输出字面的 '<%'
%> 普通的结束标签
-%> Trim-mode ('newline slurp') 标签, 移除随后的换行符
包含