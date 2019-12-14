---
bg: "photo34.jpg"
layout: post
title: "Cross View Fusion for 3D Human Pose Estimation"
crawlertitle: "Cross View Fusion"
summary: "Cross View Fusion for 3D HPE"
date: 2019-12-04 15:00:00 +0800
categories: "paper"
tags: "HPE"
author: "vpromise"
---

*this paper present an approach to recover absolute 3D humanposes from multi-view images by incorporating multi-view geometric  priors*
*by USTC, MRA & TuSimple. [code](https://github.com/microsoft/multiview-human-pose-estimation-pytorch)*

---

- [Abstract](#abstract)
- [Introduction](#introduction)
  - [challenge](#challenge)
  - [Merits](#merits)
- [Cross View Fusion for 2D Pose Estimation](#cross-view-fusion-for-2d-pose-estimation)
- [RPSM for Multi-view 3D Pose Estimation](#rpsm-for-multi-view-3d-pose-estimation)
- [Experiments](#experiments)
- [Conclusion](#conclusion)

# Abstract

We present an approach to recover absolute3D humanposes from multi-view images by incorporating multi-view geometric  priors  in  our  model.   It  consists  of  two  separate steps: (1) estimating the2D poses in multi-view images and (2) recovering the3D poses from the multi-view 2D poses.  First, we introduce a cross-view fusion schemeinto CNN to jointly estimate2D poses for multiple views.Consequently,  the2D  pose  estimation  for  each  view  already benefits from other views.  Second, we present a recursive Pictorial Structure Model to recover the3D posefrom  the  multi-view 2D  poses. 

# Introduction

## challenge
Most works follow the pipeline of first estimating 2D poses and then recovering 3D posefromthem. However, the latter step usually depends on the performance of the first step which unfortunately often has large errors in practice especially when occlusion or motionblur occurs in images. This poses a big challenge for thefinal 3D estimation.

## Merits
- We obtain more accurate 2D poses by jointly estimating them from multiple views using a CNN based approach.
- We present Recursive Pictorial Structure Model(RPSM), to recover the3D pose from the estimated multi-view 2D pose heatmaps.

# Cross View Fusion for 2D Pose Estimation
2D pose estimator takes multi-view images as input,generates initial pose heatmaps respectively for each, andthen fuses the heatmaps across different views such that theheatmap of each view benefits from others. The processis accomplished in a single CNN and can be trained end-to-end. Figure1shows the pipeline for two-view fusion.

![fig 1](https://i.loli.net/2019/12/14/5ZLFzYCaWNSlubR.png)

# RPSM for Multi-view 3D Pose Estimation
The PSM model suffers from large quantization errorscaused by space discretization.Instead of using a largeNin one iteration, we proposeto recursively refine the joint locations through a multiplestage process and use a smallNin each stage. In thefirst stage (t=0), we discretize the 3D bounding vol-ume space around the triangulated root joint using a coarsegrid (N=16) and obtain an initial 3D pose estimation L=(L1,···,LM) using the PSM approach. For the following stages (t≥1), for each joint Ji, wediscretize the space around its current location Li into an 2×2×2 grid G(i). 

Instead of refining each joint independently, we simultaneously refine all joints considering their spatial relations.Recall that we know the center locations, sizes and the number of bins of the grids. So we can calculate the location ofevery bin in the grids with which we can compute the unaryand pairwise potentials. It is worth noting that the pairwise potentials should be computed on the fly because it dependson the previously estimated locations. However, because we set N to be a small number (two in our experiments),this computation is fast.

![fig 5](https://i.loli.net/2019/12/14/dGSmVuE7YTxsHjg.png)

# Experiments
Please read the paper for mopre detial information.

# Conclusion
We propose an approach to estimate 3D human poses from multiple calibrated cameras. The first contribution is a CNN based multi-view feature fusion approach which significantly improves the 2D pose estimation accuracy. Thesecond contribution is a recursive pictorial structure modelto estimate 3D poses from the multi-view 2D poses. It improves over the PSM by a large margin. The two contributions are independent and each can be combined with the existing methods.
