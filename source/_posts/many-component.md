---
title: 项目如何进行组件化拆分
categories:
  - Others
date: 2018-03-05 14:58:38
tags: 组件拆分
cover_picture: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2904832717,3935119407&fm=15&gp=0.jpg
---

一个 React 项目都是由多个组件组成的。

所以可以把整个项目拆成一个个的小组件：

- 一个页面会拆分成多个组件
- 组件不一定非要复用
- 一个组件最好不要超过一百行代码
- 组件可以无限拆分
- 组件要放到 src/components/ 文件夹内
