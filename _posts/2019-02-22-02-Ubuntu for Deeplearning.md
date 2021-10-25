---
bg: photo002.jpg
layout: post
title: Ubuntu搭建深度学习环境
crawlertitle: Ubuntu搭建深度学习环境
summary: 通过Anaconda搭建Ubuntu的深度学习环境
date: 2019-02-22 17:00:00 +0800
tags : linux
author: vpromise
categories: tech
---

*前一篇博客介绍了Ubuntu系统安装，系统只是一个载体，使用Linux系统主要还是为了方便Coding，现在进入主题，基于Ubuntu搭建深度学习环境，最方便的方法就是通过Anaconda来创建环境了*

**基于Ubuntu搭建深度学习环境，我的机器配置如下：**
* System：Ubuntu 18.04
* Graphics： Dual NVIDIA GeForce GTX 1080 Ti
* Processor: Intel Core i7-6850K
* Memory: 32GiB


- [一、安装显卡驱动](#一安装显卡驱动)
    - [1. 添加Graphic Drivers PPA](#1-添加graphic-drivers-ppa)
    - [2. 安装驱动](#2-安装驱动)
- [二、安装Anaconda](#二安装anaconda)
    - [1.  下载Ananconda](#1--下载ananconda)
    - [2. 创建虚拟环境](#2-创建虚拟环境)
    - [3. 配置深度学习环境](#3-配置深度学习环境)
    - [4. 停用 anaconda](#4-停用-anaconda)
    - [5. 卸载 anaconda](#5-卸载-anaconda)
- [三、IDE](#三ide)


# 一、安装显卡驱动
网上关于安装Nvidia驱动的教程有很多，有些考虑到还有安装cuda的版本，驱动版本还有要求，其次还要求禁用nouveau驱动，关闭图形界面等操作，但下面的操作通过添加源就能实现安装最新驱动，最为方便
### 1. 添加Graphic Drivers PPA
```
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```
### 2. 安装驱动
打开Software & Updates，选择Additional Drivers，一般需要加载一定时间，会出现多个驱动，选择最新的也就是版本号最大的NVIDIA-Driver，点击应用，需要等待一点时间生成应用，完成便成功安装了驱动![Nvidia显卡驱动](https://i.loli.net/2019/09/20/ioujLSWd8U6yvKM.png)

# 二、安装Anaconda
对于Anaconda就不做过多介绍，下面直接来安装
### 1.  下载Ananconda
去[Anaconda](https://www.anaconda.com/distribution/#download-section)官网下载相应的安装包，以Ubuntu18.04为例，下载Anaconda3-2018.12-Linux-x86_64.sh， 打开终端安装
```
# 进入下载目录
~$ cd Downloads/
# 执行安装
~/Downloads$ bash Anaconda3-2018.12-Linux-x86_64.sh 
```
### 2. 创建虚拟环境
```
# 通过conda创建虚拟环境，命名为deepl
conda create -n deepl python=3.6
```
以上命令则创建了名为`deepl`的虚拟环境，我们可以打开和关闭环境
```
# 打开环境
source activate deepl 
# 关闭环境
source deactivate deepl
```
### 3. 配置深度学习环境

[Anaconda Cloud](https://anaconda.org/)官网提供了各种包的安装命令，可以搜索并安装到我们创建的虚拟环境中，例如搜索`tensorflow`，执行便可安装![tensorflow](https://i.loli.net/2019/09/20/i16do5cWAHIC43q.png)

```
# 激活虚拟环境
source activate deepl 
# 安装tensorflow
conda install -c anaconda tensorflow-base 
```
安装过成完全自动，conda会自动解决环境和依赖的问题，安装完成后，便可执行查看
```
$ source activate tf
(tf) usr:~$ python
Python 3.6.7 | packaged by conda-forge | (default, Nov 21 2018, 03:09:43) 
[GCC 7.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow as tf
>>> tf.__version__
'1.10.0'
```
其他包的安装类似，比如`pytorch`、`opencv`等

### 4. 停用 anaconda
若要停用`anaconda`,操作如下

```
 vim ~/.bashrc
```
在.bashrc文件末尾用#号注释掉之前添加ananconda路径：
```
# export PATH=/your/path/to/anaconda3/bin:$PATH
```
使其立即生效，在终端执行：
```
source ~/.bashrc
```

### 5. 卸载 anaconda
完全卸载`ananconda`方法如下
```
 vim ~/.bashrc
```
在.bashrc文件末尾删除掉之前添加ananconda路径

由于Anaconda的安装文件都包含在一个目录中，所以直接将该目录删除即可。
```
rm -rf anaconda3
```


# 三、IDE
推荐[Visual Studio Code](https://code.visualstudio.com/Download)，轻量快速，在终端激活环境，便可直接运行程序
![Visual Studio Code](https://i.loli.net/2019/09/20/rwh8AUDXsuzJCtp.png)

---
```
> update at 20190509_1614
> update at 20190822_1039
> update at 20190920_1000 : Change Image Hosting Service
```
