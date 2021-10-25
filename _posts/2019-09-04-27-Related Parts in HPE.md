---
bg: photo027.jpg
layout: post
title: Related Parts Help HPE
crawlertitle: PBN for HPE
summary: Learning Specific Features for Related Parts Help HPE
date: 2019-09-04 16:00:00 +0800
categories: academic
tags: HPE
author: vpromise
---

*Paper Reading: Does Learning Specific Features for Related Parts Help Human Pose Estimation?*

---

- [Does Learning Specific Features for Related Parts Help Human Pose Estimation?](#does-learning-specific-features-for-related-parts-help-human-pose-estimation)
  - [介绍](#介绍)
  - [贡献](#贡献)
  - [方法](#方法)
    - [相关身体部位](#相关身体部位)
    - [基于部分的分支网络(PBN)](#基于部分的分支网络pbn)
  - [实验](#实验)
    - [基准数据集结果](#基准数据集结果)
    - [Ablation study](#ablation-study)
  - [总结](#总结)

# Does Learning Specific Features for Related Parts Help Human Pose Estimation?

本文是西北大学提出的在人体姿态估计任务中，学习相关部位的特定特征能提高人体姿态估计的精度。

## 介绍
人体姿态估计(HPE)本质上是一个同质多任务学习问题，每个身体部位的定位是一个不同的任务。最近的HPE方法普遍学习所有身体部位的共享表示，从该表示中它们的位置被线性回归。统计分析表明，并非所有部分都相互关联。结果，这种共享机制会导致负迁移并降低性能。基于此，本文提出一个有趣的问题。能否通过识别相关部位并学习它们的具体特征来提高姿态估计吗？由于不相关的任务不再共享高层次的表达，希望能避免负迁移的反作用。

本文首先提出了一种数据驱动的方法，根据相关部位共享的信息量对它们进行分组。然后引入基于部件的分支网络(PBN)来学习每个部位组特有的表示。再进一步提出了该网络的多阶段版本，以反复改进中间特征和姿态估计。实验表明，学习特定特征显著改善了遮挡部位的定位，从而有利于HPE。在两个基准数据集上达到了最先进的方法，在发生遮挡时具有突出的优势。

## 贡献
本文的贡献总结为以下几点：
1. 本文是第一个发现所有身体部位的特征应该完全共享是存在问题的，并通过简单有效的基于部位的分支网络来解决这个问题
2. 本文首次尝试利用身体部位位置的概率分布及其相互信息来对相关部位进行分组，并证明比基于人体结构的方法更有效
3. 本文的模型在定位遮挡部位方面具有突出的优势

## 方法
论文首先介绍两种识别相关身体部位的策略。然后提出一个基于部分的分支网络来学习它们的特定特征。最后，提出了该网络的多阶段版本，以重复地改进中间特征和身体部位定位。

### 相关身体部位
**基于人体身体结构**
识别相关部位最直接的方法是利用人体结构，直觉上，自然界中相连的部分是相关的，如图1所示，展示了相关部位的分组。
![图1 基于身体结构分组](https://i.loli.net/2019/09/04/Twm4fk3dQbxOovL.png)
<center>图1 基于身体结构分组</center>

**基于数据驱动**
将每个部位的位置视为随机变量，由此计算两者之间的相关性，公式如下：
![1](https://i.loli.net/2019/09/04/jSW4eTxFwnEKfC9.png)
I值越高表示与部位m密切相关的特征也为部位n提供了信息线索，反之亦然。

### 基于部分的分支网络(PBN)
基于部分的分支网络(PBN)是一个 CNN 网络结构，由两阶段组成，一个学习对所有身体部分通用的共享表示的阶段，另一个学习对每组相关部分专用的高级特征的阶段，整体结构如图2所示。
![图2 PBN 网络结构](https://i.loli.net/2019/09/04/9SakNlOFY8wTbcu.png)
<center>图2 PBN 网络结构</center>

## 实验
### 基准数据集结果
论文在MPII和LSP数据集上进行了实验，均取得了较好的结果，具体实验结果如下表1、2、3所示：
![表1 Comparisons of PCKh@0.5 scores on the invisible parts in the MPII validation set](https://i.loli.net/2019/09/04/nVqh6ugxeoQ71D3.png)
<center>表1 Comparisons of PCKh@0.5 scores on the invisible parts in the MPII validation set</center>

![表2 Comparisons of PCK@0.2 scores on the LSP testing set](https://i.loli.net/2019/09/04/bgBi9eNcC4hGksj.png)
<center>表2 Comparisons of PCK@0.2 scores on the LSP testing set</center>

![表3 Comparisons of PCK@0.2 scores on the corrected LSP testing set](https://i.loli.net/2019/09/04/xUuLWRMQ1rjdlN4.png)
<center>表3 Comparisons of PCK@0.2 scores on the corrected LSP testing set</center>

### Ablation study
论文还做了大量实验，分析了特定的feature层的深度和宽度选取多少合适，讨论了身体部位分组的策略以及分组中存在部位重叠的效果等等大量的实验内容，更多的实验内容可以参考论文。
![Ablation study using variants of three-stack PBNs](https://i.loli.net/2019/09/04/SreOqp2TU6gBi35.png)
<center>Ablation study using variants of three-stack PBNs</center>

## 总结
论文通过大量的基准数据集实验和消融研究，得出结论，学习相关身体部位的特定特征可以显著改善遮挡部位的定位，从而有利于人体姿态估计。

似乎这是一个很自然的想法，但先前的工作的都是对各个部位共享参数来定位的，但论文中做　Ablation study　时，证明对不同身体部位分组有重叠的情况下，反而对最后结果没有提升帮助，个人认为此部分可以再去做更多实验来验证。而且多个分组得到的结果直接取均值来算最后结果并不是一个可靠的方法，也许不同的部位的权重也需要考虑，注意力机制也许是一个很好的方法，可以应用到本文中。