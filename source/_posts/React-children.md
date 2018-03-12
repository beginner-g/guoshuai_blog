---
title: React 中的 children 是什么
categories:
  - React
date: 2017-09-11 14:47:03
cover_picture: https://ss0.bdstatic.com/70cFvHSh_Q1YnxGkpoWK1HF6hhy/it/u=2436513331,2729964507&fm=27&gp=0.jpg
tags: [react,children]
---

### React 中的 children 是什么？
子组件向父组件获取属性值的一种形式

向 React 组件内传数据，不仅仅有 props 这一种形式，还可以使用 children 。

### Children 的传入方式
```
<Button>登录</Button>
```
### 组件内获取

Button.js 中这样写
```
this.props.children
```
就可以取到“登录”这个字符串了。


