---
bg: "photo19.jpg"
layout: post
title: "Jupyter Notebook配置"
crawlertitle: Jupyter Notebook
summary: Jupyter Notebook配置
date: 2019-07-28 14:00:00 +0800
categories: "Tech"
tags: "Jupyter"
author: "vpromise"
---

*Jupyter Notebook的一些配置，包括主题和内核切换等高阶拓展*

---

Jupyter Notebook 可以说是目前最流行的 Python 编程环境，尤其是对从事机器学习和数据科学的人而言。Jupyter Notebook 可以在浏览器中运行，可以方便地调试，便于我们测试一些简单的想法和代码。当然，Jupyter Notebook 也有一些不足，接下来就让我们增强我们的 Jupyter Notebook。

**教程包括但不限于：**
- Dark配色，拯救眼睛
- 动态切换多个 Conda 环境，无需重启 Jupyter Notebook
- 一键点击生成目录
- 弹出式便签，无需改变原始笔记本中任何地方就可以测试你的代码
- 代码单元内的代码折叠
- 一键代码单元隐藏
- 变量检查器。
- 用于 Markdown 单元的拼写检查器
- 用于深夜编码会话的禅意黑模式（ZenMode）

---

## 1. Dark主题
#### 1.1 安装`jupyterthemes`
首先安装`jupyterthemes`
```
# Kill and exit the Notebook server
# Make sure you are in the base conda environment
conda activate base
# install jupyterthemes
pip install jupyterthemes
# upgrade to latest version
pip install --upgrade jupyterthemes
```
查看所有主题
```
jt -t ls
```
可以看到包含主题如下
```
Available Themes: 
chesterish
grade3
gruvboxd
gruvboxl
monokai
oceans16
onedork
solarizedd
solarizedl
```
#### 1.2 应用主题
选择合适的主题并应用，例如
```
jt -t oceans16
```
`oceans16`是我喜欢的主题,显示如下
![osceans16](https://i.loli.net/2019/07/28/5d3d4be758d0d22152.png)
如果想切换成默认主题，只需
```
jt -r
```

## Conda 环境自由切换
我的 Conda 下创建了多个虚拟环境，包含不同的包来适配不同的任务需要，这也就造成了每次在 Jupyter 中调用不同的环境需要关闭再重开，操作很麻烦，而且在不同虚拟环境中都需要装Jupyter Notebook。

其实，只需要把 Anaconda 中创建的所有定制环境作为核心添加在了 Jupyter Notebook 中。这样我们就能简单地利用 Kernel 按钮切换环境。换核的时候不需要重启Jupyter Notebook。
#### 2.1 添加到 Kernal
我的虚拟环境有`deep`和`cv`，添加到 Jupyter Notebook 中
```
# Stop and exit your Jupyter Notebook server first
# Activate your environment in the terminal 
conda activate deep
# Install the IPython Kernel 
pip install ipykernel
# Link your environment with Jupyter 
python -m ipykernel install --user --name=deep
```
其他环境重复操作就好
```
# Rrepeat steps for the other environment: cv
conda activate gym
pip install ipykernel 
python -m ipykernel install --user --name=cv
```
#### 2.2 切换 Kernal
完成后在`base`中启动 Jupyter Notebook，便可通过`Kernal`-->`Change Kernal`来切换不同的内核了，而不用关闭 Jupyter Notebook 再重开。
![kernel](https://i.loli.net/2019/07/28/5d3d4be75ce5840151.png)







---

**thanks to:**
- [机器之心](https://www.jiqizhixin.com/articles/2019-07-23-5?from=synced&keyword=jupyter%20notebook)
- [Pranjal Chaubey](https://towardsdatascience.com/supercharging-jupyter-notebooks-e22f5ad7ca18)

