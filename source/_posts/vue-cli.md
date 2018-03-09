---
title: 安装 Vue 脚手架时遇到的问题
categories:
  - Vue
date: 2018-03-07 17:40:30
tags: [vue,vue-cli]
cover_picture: https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2064073397,779040426&fm=27&gp=0.jpg
---

### 安装Vue脚手架时遇到的管理员权限问题

➜  vue npm i -g vue-cli
~~~
npm WARN deprecated coffee-script@1.12.7: CoffeeScript on NPM has moved to "coffeescript" (no hyphen)
npm WARN checkPermissions Missing write access to /usr/local/lib/node_modules
npm ERR! path /usr/local/lib/node_modules
npm ERR! code EACCES
npm ERR! errno -13
npm ERR! syscall access
npm ERR! Error: EACCES: permission denied, access '/usr/local/lib/node_modules'
npm ERR!  { Error: EACCES: permission denied, access '/usr/local/lib/node_modules'
npm ERR!   stack: 'Error: EACCES: permission denied, access \'/usr/local/lib/node_modules\'',
npm ERR!   errno: -13,
npm ERR!   code: 'EACCES',
npm ERR!   syscall: 'access',
npm ERR!   path: '/usr/local/lib/node_modules' }
npm ERR!
npm ERR! Please try running this command again as root/Administrator.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/apple/.npm/_logs/2018-03-07T09_07_19_309Z-debug.log
~~~

### 解决方案

➜  vue sudo npm i -g vue-cli