---
layout: post
bg: 'photo05.jpg'
title: "GitHub Pages 搭建个人博客"
crawlertitle: "GitHub Pages Blog"
summary: "GitHub Pages Blog"
date: 2019-05-16 20:05:00 +0800
tags : "blog"
categories: "tech"
author: "vpromise"
---



*介绍如何利用GitHub Pages来搭建个人的博客，完全免费哦*

---
之前一直用简书来记录自己的想法，不得不说简书的Markdown支持对于写作还是很友好的，但是作为一个爱折腾的人，还是想搭建一个自己的博客，于是也便有了本文，基于GitHub Pages搭建自己的博客，GitHub建站十分方便而且免费，同时网上有大量的主题供你选择，你也可以修改定制自己的网站页面。可以说GitHub建站是初学者的首选，免费简单且好用，话不多说，让我们开始吧。

##  一、GitHub

### 1. 注册GitHub

首先自然是注册属于自己的GitHub账号，这个在此就不赘述了

### 2. 新建Repository

- 点击`New respository`新建一个**Repository**,此处注意在填`Repository name`时有特定的格式要求，为`Owner_name.github.io`,其中`Owner_name`保持和前面`Owner`一致就行了，见下图，例如我的Repository就是`vpromise.github.io`,其他的可以不用管了，点击`Create repository`完成

- 进入我们新建的**Repository**,点击上面的设置`Settings`,在设置页面下翻找到`GitHub Pages`，点击`Choose a theme`，选完后点击`Commit changes`退回到**Repository**页面，这时我们的**Repository**中就有两个文件了，同时，重点也来了，此时我们的博客就已经可以访问了，尝试访问`https://your_name.github.io`进入你自己的博客，是不是很惊喜，但这只是一个页面，如果你只想做一个页面展示自己的简历，这个页面就足够了，只需要修改`index.md`文件就好了
![Choose a theme](https://i.loli.net/2019/05/16/5cdd72e1e155297958.png)

- 自然这样还是不够的，接下来就是个性化自己的博客了

  

## 二、Jekyll Theme

### 2.1 选择Jekyll Theme

- 博客当然要好看才能赏心悦目，这里有三个网站提供了大量的主题供你选择<http://jekyllthemes.org/>、<https://jekyllthemes.io/>、<http://themes.jekyllrc.org/>，找到你喜欢的主题，进入它的`Home Page`，一般都是跳转到了项目的Github页面，点击`Clone or downlo`复制项目地址，然后打开你想在本地存放你项目的文件夹，进入终端，`git clone https://github.com/...`将项目克隆到本地文件夹，当然你也可以直接下载ZIP再解压
![Clong or download](https://i.loli.net/2019/05/16/5cdd72e21316790298.png)

- 紧接着就是将你自己的项目克隆到本地，克隆的方法一样，再将下载下来的主题文件全部复制到你自己项目的文件夹里，有同名的文件直接替换就好了，完了就是直接三连，`git add --all`、`git commit -m "UPDATA"`、`git push -u origin master`, 输入GitHub账号和密码等待完成就好了

- 进入我们的GitHub页面，就能看到我们的**Repository**下文件多了很多，这时候再进入我们的GitHub Pages页面就会看到主题应用成功了，至此，工作就算完成一半了

### 2.2 修改主题

- 接下来就是定制自己的主题了，一般模板的`README.md`文件都有写修改的提示，我们应当首先看一下了解一下，修改主题都是从`_config.yml`入手，修改博客名、描述等，还有就是添加一些个人信息，此部分较为灵活，不同主题的`_config.yml`内容也不尽相同，自己多改改看效果就好

- 还有一些页面的修改就稍显麻烦了，也都需要自己去摸索了，这里也无法展开讲，尽量就把每个文件都点开看看吧，一般能发现一些东西，我也是自己一个个看，慢慢试



## Blog
### 3.1 posts