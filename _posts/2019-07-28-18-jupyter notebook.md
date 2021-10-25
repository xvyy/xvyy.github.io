---
bg: photo018.jpg
layout: post
title: Jupyter Notebook配置
crawlertitle: Jupyter Notebook
summary: Jupyter Notebook配置
date: 2019-07-28 14:00:00 +0800
categories: technology
tags: jupyter
author: vpromise
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

## 2. Conda 环境自由切换
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

#### 2.3 移除 Jupyter 关联环境
查看 Jupyter 关联的内核环境
```
jupyter kernelspec list
```
移除 Jupyter 关联环境
```
jupyter kernelspec uninstall unwanted-kernel
```

## 3. 更多炫酷功能
开始提及的其他炫酷功能，需要安装一些叫做 `nbextensions for Jupyter Notebooks` 的东西。
安装地址：https://jupyter-contrib-nbextensions.readthedocs.io/en/latest/install.html
#### 3.1 安装 nbextensions 
安装 `nbextensions` 是很容易的，简单地遵循下面的步骤就行：
```
# Stop and exit your Jupyter Notebook server 
# Make sure you are in the base environment
conda activate base

# Install the nbextensions 
pip install jupyter_contrib_nbextensions
# 或者
conda install -c conda-forge jupyter_contrib_nbextensions

# Install the necessary JS and CSS files 
jupyter contrib nbextension install --user
# 或者
jupyter contrib nbextension install --system
```
启动 Jupyter notebook 服务，你可以在起始页看到第四个叫做`Nbextensions`的选项。点击这个选项，然后就可以看到极妙的功能集，这些都是你一直希望在 Jupyter Notebooks 中拥有的。
![Nbextensions](https://i.loli.net/2019/07/28/5d3d64662f11d45523.png)

#### 3.2 Nbextensions！

正如你在上面看到的，这个扩展列表十分庞大，甚至第一眼看上去有些吓人。但并不是所有的都有用，下面是常用到的一些功能：
- Table of Contents(2)：单击生成整个笔记本的目录，不同的 section 都有对应的超链接。
- Scratchpad：在我看来绝对是最好的扩展了。这是一个你可以在里面做代码实验的独立空间，不会干扰笔记本中的其他部分。
- Codefolding ：代码折叠，这个不需要做过多的解释。
- Hide Input All：隐藏所有的代码单元，同时保持所有的输出和 markdown 单元可见。如果你要向非技术人员解释你的结果，那么这就会是一个很有用的功能。
- Variable Inspector：将你从调试的忧伤中拯救出来，这与 Spyder IDE 中的变量检查窗口有些类似。
- Spellchecker：对 markdown 单元中的内容进行拼写检查。
- Zenmode：移除掉屏幕中杂乱无关的内容，以便你能够聚焦于重要的东西上，例如代码。
- Snippets Menu：从 list comprehension 到 pandas 以及它们之间的所有常用代码片段的一个很酷的集合。这是最好的部分？你可以修改窗口的小部件来添加你自己的定制片段。


---

**thanks to:**
- [机器之心](https://www.jiqizhixin.com/articles/2019-07-23-5?from=synced&keyword=jupyter%20notebook)
- [Pranjal Chaubey](https://towardsdatascience.com/supercharging-jupyter-notebooks-e22f5ad7ca18)