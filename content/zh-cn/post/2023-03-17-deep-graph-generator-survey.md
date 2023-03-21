---
title: 图生成方法综述
date: '2023-03-17'
slug: deep-graph-generator-survey
tags:
  - Misc
  - Deep-learning
  - Survey
---

# 基于自回归（AUTOREGRESSIVE）的图生成方法

| 方法  |  生成策略  | 特征类型 | 可附加生成条件 | 公开源码 |
| :---: | :--------: | :------: | :------------: | -------- |
| MolMP | 逐节点生成 | 节点/边  |      YES       |          |
|       | 逐节点生成 | 节点/边  |       NO       |          |
|       | 逐节点生成 |          |                |          |
|       | 逐节点生成 |          |                |          |

## 使用RNN的方法
### 逐节点生成图的方法
MolMP、MolRNN、GraphRNN、MolecularRNN
### 逐边生成图的方法
GraphGen

## 不使用RNN的
### 基于注意力机制的
### 其他方法


# 基于自编码器（AUTOENCODER）的图生成方法

## 一次生成整个图的方法
## 基于子结构（SUBSTRUCTURE）的方法
## 逐节点生成图的方法


# 基于强化学习的图生成方法


# 基于生成对抗网络的图生成方法
## 基于随机游走的方法
## 基于整个图的方法
### GENERAL GRAPH-BASED ADVERSARIAL DGGs
MolGAN
### GRAPH-TO-GRAPH TRANSLATORS

# 基于流的图生成方法


