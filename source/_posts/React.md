---
title: React 是什么
categories:
  - Others
date: 2018-03-06 15:03:28
tags: [react,Webpack,Babel]
cover_picture: http://www.chuanke.com/upload/courseware/f/31/3312428/image/09c68fe797fa58d78a1de4f34e0ea40f.gif
---

官网在 https://github.com/facebookincubator/create-react-app 。

简称 cra 。cra 的主要作者就是目前 react 项目的老大 Dan ，以及 facebook 公司的其他一些员工。

cra 是一个开发 React 项目的环境，无需配置直接使用。

### 开发 React 项目曾经很麻烦

没有 cra 之前，开发 React 需要自己搭建下面的环境：

- 需要配置 Webpack ，来把多个 JS 源文件打包成一个文件
- 需要配置 Babel，来编译 ES6
- 需要配置 Babel，来编译 JSX
- 另外还有很多 webpack 配置要来自己做，以便能够处理 svg/css/html 等各种文件类型

总是是非常麻烦。而 cra 就包含 Webpack+Babel ，而且其中的配置都是顶级高手帮我们精心配置好的。

### 有了 cra ，我们开发就省心了

基本上就是，运行下面的命令来创建一个新的 React 项目
```
create-react-app react-demo
```
生成的脚手架项目，也就是 react-demo ，它首先是一个 nodejs 项目，而且其中 package.json 和 node_modules 中已经为我们安装好了，开发 React 的常用的包。另外就是还有一个很小的 react 的程序，我们可以在上面继续开发了。

### 使用淘宝镜像

用本来的国外镜像，有时候会创建失败，这时候就先运行
```
npm config set registry https://registry.npm.taobao.org
```

### 文件介绍

生成的代码中，会有

- yarn.lock，这个如果你的系统上装了 yarn 就会有，yarn 是跟 npm 类似的一个东西，也是用来装 npm 包的。

- public 文件夹，放 html 和图标的

-   src 文件夹，所有 js 代码都放到这里

