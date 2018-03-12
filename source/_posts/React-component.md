---
title: React 组件是什么
categories:
  - React
date: 2017-10-29 12:54:05
tags: [react,component]
cover_picture: http://s1.51cto.com/wyfs02/M01/88/7F/wKiom1f55HCSS-DrAACSkyHme8o914.png-wh_651x-s_1436211364.png
---
## React.Component是什么？

组件让你可以将用户界面分成独立的，可重复使用的部分，并且可以独立思考每个部分。React.Component由...提供React。

### 动手来写一个 React 组件

创建 src/App.js 文件（ React 组件文件一般都是首字母大写，例如这里的 App.js ）

首先导入必要的变量：
```
import React, { Component } from 'react'
```
一个 React 组件就是一个 class （另外一种形式是写成 function ），它的名字首字母必须大写，一般组件名就和它所在的文件名统一。

组件内部可以写很多东西，但是必须要写的一个就是 render 函数，所以一个最简单的 React 组件，就要写成下面这样：
```js
class App extends Component {
  render () {
    return (
      <div>
        Hello World
      </div>
    )
  }
}
```
这样，App.js 就是包含了组件的一个 JS 模块。所以如果想在其他文件中调用 App 组件，那么需要首先导出 App 。
```
export default App
```
至此，一个简单的 React 组件就完工了。

### 使用组件

create-react-app 默认的配置就会去 index.js 中找东西，所以，我们要创建

src/index.js
```js
import React from 'react'
import ReactDom from 'react-dom'
import App from './App'

ReactDom.render(<App />, document.getElementById('root'))
```
注意，组件在使用的时候要用尖括号括起来，而且要有斜杠。

上面 index.js 中提到的 id 为 root 的挂载点 需要由 public/index.html 来提供
```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
  <div id='root'></div>
</body>
</html>
```
这样，到 http://localhost:3000/ 程序运行正常。


