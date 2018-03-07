---
title: 创建 Hello react 项目
date: 2018-03-06 15:02:58
tags: react
cover_picture: https://ss0.bdstatic.com/70cFuHSh_Q1YnxGkpoWK1HF6hhy/it/u=384169016,987997010&fm=27&gp=0.jpg
---
在 create-react-app 环境下，我们来写一个 react 的 Hello World 。

### 运行项目

到 create-react-app 帮我们生成的项目中，运行
```
npm start
```
就可以启动这个项目了。

### 一个 Hello World

一个最简单的 React 项目，包含下面几个文件

src/App.js
```js
import React, { Component } from 'react'

class App extends Component {
  render () {
    return (
      <div>
        Hello World
      </div>
    )
  }
}

export default App
```
src/index.js
```js
import React from 'react'
import ReactDOM from 'react-dom'
import App from './App'

ReactDOM.render(<App />, document.getElementById('root'))
```
public/index.html
```html
<!doctype html>
<html>
  <body>
    <div id="root"></div>
  </body>
</html>
```

### 介绍一下上面三个文件的作用

index.html 文件中基本就是空的，关键就是保留一个 div ，目的是用来挂载 React 组件。

App.js 文件是一个 React 组件 （ component ）。未来会成为整个程序的主体。

index.js 中主要是使用 ReactDom 这个包，作用就是把 App.js 中的 react 组件，挂到 index.html 中的那个唯一的 div 之上。
