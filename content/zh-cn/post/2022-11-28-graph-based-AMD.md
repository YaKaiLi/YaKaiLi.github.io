---
title: 基于图的安卓恶意软件检测方法综述
date: '2022-11-28'
slug: graph-based-AMD
tags:
  - Graph_embedding
  - Android
  - Malware_detection
---
此篇文章只介绍已开源或能够找到复现源码的工作。

主要是图嵌入方法的区别。
# MalScan

# MamaDroid
阅读主要关注于算法如何实现的，分为四个阶段：调用图提取、序列提取、构建马尔可夫链和特征向量、分类器。

MaMaDROID不使用原始API调用序列，而是将每个调用抽象为其包或其族。

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2022/11/28/21-50-42-98fe24fe906cbdc4c9e1bb91275551b9-0e11e0.png)

## 调用图提取

Soot [52], to extract call graphs and FlowDroid [6] to ensure contexts and ﬂows are preserved.

## 序列提取

有了调用图之后从调用图中提取API调用序列。

首先，标识调用图中的一组入口节点，即没有传入边的节点（例如，如果app中没有来自任何其他调用的传入边，则图2中代码段中的执行方法是入口节点）。然后，它枚举从每个入口节点可以到达的路径。在此阶段确定的所有路径集构成API调用序列，用于构建马尔可夫链行为模型和提取特征（参见第II-D节）。

## 构建马尔可夫链和特征向量

## 分类器

随机森林、1近邻（1-NN）、3近邻（3-NN）和支持向量机（SVM）

