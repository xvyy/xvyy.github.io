---
bg: "photo30.jpg"
layout: post
title: "Common Evaluation Metrics for HPE"
crawlertitle: "Evaluation Metrics for HPE"
summary: "Common Evaluation Metrics for Human Pose Estimation"
date: 2019-10-09 10:00:00 +0800
categories: "paper"
tags: "HPE"
author: "vpromise"
---

# Common Evaluation Metrics for HPE

Evaluation metrics are needed to measure the performance of human pose estimation models.

## Percentage of Correct Parts - PCP: 
A limb is considered detected  (a correct part) if the distance between the two predicted joint locations and the true limb joint locations is less than half of the limb length (Commonly denoted as PCP@0.5).

- It measures the detection rate of limbs. The con is that it penalizes shorter limbs more since shorter limbs have smaller thresholds.
- Higher the PCP, better the model.

## Percentage of Correct Key-points - PCK: 
A detected joint is considered correct if the distance between the predicted and the true joint is within a certain threshold. The threshold can either be:

- PCKh@0.5 is when the threshold = 50% of the head bone link
- PCK@0.2 == Distance between predicted and true joint < 0.2 * torso diameter
- Sometimes 150 mm is taken as the threshold.
- Alleviates the shorter limb problem since shorter limbs have smaller torsos and head bone links.
- PCK is used for 2D and 3D (PCK3D). Again, the higher the better.

## Percentage of Detected Joints - PDJ: 
A detected joint is considered correct if the distance between the predicted and the true joint is within a certain fraction of the torso diameter. PDJ@0.2 = distance between predicted and true joint < 0.2 * torso diameter.

## Object Keypoint Similarity (OKS) based mAP:
- Commonly used in the COCO keypoints challenge.
- OKS = 
  ![oks.png](https://i.loli.net/2019/10/09/9TYMhCZsPjm37rX.png)

  <!-- $$\frac{\sum_iexp(-d^2_i/2s^2k^2_i)\delta(v_i>0)}{\sum_i\delta(v_i>0)}$$ -->

- Where di is the Euclidean distance between the detected keypoint and the corresponding ground truth, vi is the visibility flag of the ground truth, s is the object scale, and ki s a per-keypoint constant that controls falloff.

- To put it simply, OKS plays the same role that IoU plays in object detection. It is calculated from the distance between predicted points and ground truth points normalized by the scale of the person. More info Typically, standard average precision and recall scores are reported in papers: AP50 (AP at OKS = 0.50) AP75 , AP (the mean of AP scores at 10 positions, OKS = 0.50, 0.55, . . . , 0.90, 0.95; APM for medium objects, APL for large objects, and AR (Average recall) at OKS = 0.50, 0.55, . . . , 0.90, 0.955.

> thanks to [Nanonets](https://nanonets.com/blog/human-pose-estimation-2d-guide/?utm_source=reddit&utm_medium=social&utm_campaign=pose&utm_content=GROUP_NAME)