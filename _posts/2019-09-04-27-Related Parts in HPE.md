---
bg: "photo26.jpg"
layout: post
title: "Related Parts in HPE"
crawlertitle: Related Parts in HPE
summary: Related Parts in HPE
date: 2019-09-04 12:00:00 +0800
categories: "paper"
tags: "HPE"
author: "vpromise"
---

*Paper Reading: Does Learning Specific Features for Related Parts Help Human Pose Estimation?*

---

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
