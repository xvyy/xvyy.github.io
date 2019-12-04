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
*by USTC. MRA. TuSimple*

---

# Abstract

We present an approach to recover absolute3D humanposes from multi-view images by incorporating multi-view geometric  priors  in  our  model.   It  consists  of  two  separate steps: (1) estimating the2D poses in multi-view images and (2) recovering the3D poses from the multi-view 2D poses.  First, we introduce a cross-view fusion schemeinto CNN to jointly estimate2D poses for multiple views.Consequently,  the2D  pose  estimation  for  each  view  already benefits from other views.  Second, we present a recursive Pictorial Structure Model to recover the3D posefrom  the  multi-view 2D  poses. 

# Introduction

## challenge
Most works follow the pipeline of first estimating 2D poses and then recovering 3D posefromthem. However, the latter step usually depends on the performance of the first step which unfortunately often has large errors in practice especially when occlusion or motionblur occurs in images. This poses a big challenge for thefinal 3D estimation.

## Merits
- We obtain more accurate 2D poses by jointly estimating them from multiple views using a CNN based approach.
- We present Recursive Pictorial Structure Model(RPSM), to recover the3D pose from the estimated multi-view 2D pose heatmaps.

# Cross View Fusion for2D Pose Estimation