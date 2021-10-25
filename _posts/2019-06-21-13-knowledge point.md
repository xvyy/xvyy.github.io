---
bg: photo013.jpg
layout: post
title: 知识点记录
crawlertitle: 知识点记录
summary: 各种重要知识点记录，包括数学、深度学习及其他
date: 2019-06-21 10:00:00 +0800
tags : math
author: vpromise
categories: academic
---

*各种知识点记录备忘* 

---
## CRF
- [理解条件随机场](https://www.jianshu.com/p/55755fc649b1)
- [CRF HMM](https://www.zhihu.com/question/35866596/answer/236886066)
- [MRF在深度学习图像处理中的应用](https://zhuanlan.zhihu.com/p/38343732)

## GCN
- [如何理解GCN](https://www.zhihu.com/question/54504471/answer/630639025)

## DNN CNN RNN LSTM
- [DNN CNN RNN LSTM](https://www.zhihu.com/question/34681168)

## Transformer
- [Transformer](https://zhuanlan.zhihu.com/p/308301901)
- [Blog of 李宏毅 Transformer](https://hackmd.io/@shaoeChen/rJlRfP7mL)
- [李宏毅 Transformer Tutorial](https://www.youtube.com/watch?v=ugWDIIOHtPA)

## Semi-supervised Learning
- [半监督学习](https://www.cnblogs.com/wuliytTaotao/p/12825797.html)

## Capsule Network
- [Paper](https://arxiv.org/pdf/1710.09829.pdf )
- [Blog: Capsule Network](https://www.cnblogs.com/wangxiaocvpr/p/7884454.html)
- [李宏毅 Video Tutorial](www.youtube.com/watch?v=UhGWH3hb3Hk)

## Share weights on convs with different dilation rate
```python
# define self.conv3x3
branches_1=F.conv2d(x,self.conv3x3.weight,padding=2,dilation=2)#share weight
branches_2=self.bn[1](branches_1)
branches_3=F.conv2d(x,self.conv3x3.weight,padding=4,dilation=4)#share weight
branches_4=self.bn[2](branches_3)
```