---
title: Git和Github
date: 2018-03-06 15:24:27
tags: git
cover_picture: https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=1945343878,3655021699&fm=58
---

# git 命令(上传)

### 把网上仓库上传到本地，并对多个人写的内容的更新与自己写的同步

- git clone 克隆网上仓库到本地
- git diff 未添加到git缓存区之前详细修改
  查看做了哪些修改。按 q 退出。
- git add <文件名> 把项目的修改添加到缓存区
- git commit -m '名字' 更新版本
- git push 上传网上
- git pull 多个系统同时更新，先把网上修改的放到本地
- git log 查看当前版本信息
- git log --pretty=oneline 显示1行
- git reset --hard [版本号] 回退到该版本

### 把本地建的文件夹上传到网上

```
  1.先在网上创建仓库
  2.git init(将本地的文件夹变成仓库)
  3.git add README.md
  4.git commit -m "first commit"
  5.git remote add origin git@github.com:beginner-g/a.git
  6.git push -u origin master
```
