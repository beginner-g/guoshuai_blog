---
title: Html5 元素与标签结构
categories:
  - Html5
date: 2018-03-28 16:34:58
tags: html5
---
### 一、HTML5语法
沿用了HTML的语法(已往过去的语法，是SGML语法的一个子集)，更简洁，更人性化。

1.DOCTYPE及字符编码
① DOCTYPE：<!doctype html>
② 字符编码：<meta charset="utf-8">
③ 给文档指定语言：<html lang="zh-CN">

2.大小写都可以
① 目的是为了兼容更多的文档，在HTML5里不区分大小写
建议：写代码最好规范，最好小写

3.布尔值
① <input type="checkbox" checked/>
在这里checked写上就表示true，如果不写就表示false。而不用像HTML4中要写成checked="checked"了。

4.省略引号
① <input type="text" />
② <input type='text'>
③ <input type=text>
上面三种写法都可以，当然如果属性值中出现空格，就必须写引号或双引号
建议：属性中，引号最好是双引号

1、不允许写结束符的标签：area , basebr , col， command , embed , hr , img , input , keygen , link , meta , param , source , track , wbr<xx/>
2、可以省略结束符的标签：li , dt , dd , p , rt , optgroup , colgroup , thread , tbody , tr , td , th省略</XXX>
3、可以完全省略的标签：html , head , body , colgroup , tbody
