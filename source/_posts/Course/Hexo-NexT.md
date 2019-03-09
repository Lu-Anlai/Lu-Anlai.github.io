---
title: Hexo+NexT主题搭建博客教程（Windows）
date: 2019-02-05 16:20:28
categories: Course
tags:
- 教程
- Hexo
- NexT主题
---

网上的教程都不够详细，本人自己写一篇。

<!-- more -->

# 前期准备

## 注册$\text{GitHub}$账号；

先注册一个$\text{GitHub}$账号，官网传送门：[$\text{GitHub}$](https://github.com/)；

## 安装$\text{Git}$；

下载$\text{Git}$到本地并安装，你可以到官网：[$\text{Git}$](https://git-scm.com/)处下载安装包。

安装时全程按`Next`即可。

## 安装$\text{Node.js}$；

下载$\text{Node.js}$到本地并安装，你可以到官网：[$\text{Node.js}$](https://nodejs.org/en/)处下载安装包（推荐选择$\text{LTS}$版）。

安装时全程按`Next`即可。

## 配置本地$\text{Git}$；

未完待续。

## 在$\text{GitHub}$中新建一个`Repository`；

未完待续。

# 搭建博客

## 安装并配置$\text{Hexo}$

新建一个文件夹，**作为根目录**用来存放博客文件（文件夹名任意，推荐命名成`<username>.github.io`，其中`<username>`是你$\text{GitHub}$的$\text{ID}$）。

然后在根目录中右键，选择`Git Bash Here`，然后在弹出来的窗口里输入命令`npm install -g hexo`（后文所说的输入命令都在此窗口输入），然后耐心等待。

注：等待时间从$2 \text{s} $到$30 \text{min}$不等，请耐心等待，中途不要进行任何操作。

如果出现了一长串代码，又没有`ERROR`提示出现的话，就是安装$\text{Hexo}$成功了。

接着输入：`hexo init`和`npm install`，如果弄完之后文件夹变成了这样：

![1](https://wzs666233.github.io/2019/02/01/how/p4.webp)

那就没问题了。

## 预览博客

在`Git Bash`窗口中输入`hexo s`，预览博客。

如果窗口中出现效果如下图，表明进行预览成功：

![预览博客效果](预览博客效果.png)

再打开网址[`http://localhost:4000/`](http://localhost:4000/)，即可对博客进行预览。

预览结束后一定要按`Ctrl+C`关闭预览。

至此博客搭建完成，但仍无法在公网上查看。

# 部署博客至$\text{GitHub}$

输入命令`npm install hexo-deployer-git --save`安装`deployer`。

打开根目录下的`_config.yml`，按`Ctrl+F`搜索关键词`deploy`，找到形如下面的内容：

```
deploy:
  type: git
  repository: 
  branch: 
```

改成：

```
deploy:
  type: git
  repository: https://github.com/<username>/<username>.github.io.git
  branch: master
```

依次然后输入命令：

```
hexo clean
hexo g
hexo d
```

如果没有出错的话，等几分钟，再用浏览器打开`<username>.github.io`，就可以看到你的博客了。（此时别人也可以通过这个网址看到你的博客）

## 常见问题

问题：输入`hexo d`后显示`deployer not found:git`；

解决办法：

1. 修改根目录名称为`<username>.github.io`，某些时候有玄学问题，不是你仓库对应的名称部署不上去；
2. 检查`_config.yml`文件内容是否完整，注意每一个`:`后面都有且只有一个空格；
3. 输入命令`npm install hexo-deployer-git --save`；
4. 再次尝试部署至$\text{GitHub}$。

# 美化博客

博客主题作者推荐使用$\text{NexT}$主题。

未完待续。

