---
title: 图生成方法综述
date: '2023-03-17'
slug: deep-graph-generator-survey
tags:
  - Deep-learning
  - Survey
---
我想寻找一个能够生成多维节点特征，且特征向量中每一位都是整数，并且支持添加生成约束条件的图生成方法。因此进行了一系列调研，总结如下。

主要参考了文章《Deep Graph Generators: A Survey》[^DGGsSurvey]

[^DGGsSurvey]: Faez F, Ommi Y, Baghshah M S, et al. Deep graph generators: A survey[J]. IEEE Access, 2021, 9: 106675-106702.

## 基于自回归（Autoregressive）的图生成方法

|               方法               |  生成策略  | 特征类型 | 多维节点特征 | 可附加生成条件 | 公开源码 |
| :------------------------------: | :--------: | :------: | :----------: | :------------: | :------: |
|         MolMP[^MolMPRNN]         | 逐节点生成 | 节点/边  |              |      YES       |   Yes    |
|        MolRNN[^MolMPRNN]         | 逐节点生成 | 节点/边  |              |      YES       |   Yes    |
|       GraphRNN[^GraphRNN]        | 逐节点生成 |    -     |      -       |       No       |   Yes    |
|   MolecularRNN[^MolecularRNN]    | 逐节点生成 | 节点/边  |              |       No       |    No    |
| D.Bacciu等人[^Bacciu1][^Bacciu2] |  逐边生成  |    -     |      -       |       No       |   Yes    |
|       GraphGen[^GraphGen]        |  逐边生成  | 节点/边  |              |       No       |   Yes    |
|           GRAN[^GRAN]            | 逐子图生成 |    -     |      -       |       No       |   Yes    |
|           GRAM[^GRAM]            | 逐节点生成 | 节点/边  |              |       No       |   Yes    |
|            AGE[^AGE]             | 逐节点生成 |   节点   |              |      Yes       |   Yes    |
|        DeepGMG[^DeepGMG]         | 逐节点生成 | 节点/边  |              |      Yes       |    No    |
|          BigGG[^BigGG]           | 逐节点生成 |    -     |      -       |       No       |   Yes    |

[^MolMPRNN]: Li Y, Zhang L, Liu Z. Multi-objective de novo drug design with conditional graph generative model[J]. Journal of cheminformatics, 2018, 10: 1-24.
[^GraphRNN]: You J, Ying R, Ren X, et al. Graphrnn: Generating realistic graphs with deep auto-regressive models[C]//International conference on machine learning. PMLR, 2018: 5708-5717.
[^MolecularRNN]: Popova M, Shvets M, Oliva J, et al. MolecularRNN: Generating realistic molecular graphs with optimized properties[J]. arXiv preprint arXiv:1905.13372, 2019.
[^Bacciu1]: Bacciu D, Micheli A, Podda M. Graph generation by sequential edge prediction[C]//ESANN. 2019, 2019: 95-100. 
[^Bacciu2]: Bacciu D, Micheli A, Podda M. Edge-based sequential graph generation with recurrent neural networks[J]. Neurocomputing, 2020, 416: 177-189.
[^GraphGen]: Goyal N, Jain H V, Ranu S. GraphGen: a scalable approach to domain-agnostic labeled graph generation[C]//Proceedings of The Web Conference 2020. 2020: 1253-1263.
[^GRAN]: Liao R, Li Y, Song Y, et al. Efficient graph generation with graph recurrent attention networks[J]. Advances in neural information processing systems, 2019, 32.
[^GRAM]: Kawai W, Mukuta Y, Harada T. Scalable generative models for graphs with graph attention mechanism[J]. arXiv preprint arXiv:1906.01861, 2019.
[^AGE]: Fan S, Huang B. Attention-based graph evolution[C]//Advances in Knowledge Discovery and Data Mining: 24th Pacific-Asia Conference, PAKDD 2020, Singapore, May 11–14, 2020, Proceedings, Part I 24. Springer International Publishing, 2020: 436-447.
[^DeepGMG]: Li Y, Vinyals O, Dyer C, et al. Learning deep generative models of graphs[J]. arXiv preprint arXiv:1803.03324, 2018.
[^BigGG]: Dai H, Nazi A, Li Y, et al. Scalable deep generative modeling for sparse graphs[C]//International conference on machine learning. PMLR, 2020: 2302-2312.



### 使用RNN的方法
#### 逐节点生成图的方法
MolMP、MolRNN、GraphRNN、MolecularRNN
#### 逐边生成图的方法
GraphGen、D.Bacciu等人[^Bacciu1][^Bacciu2]、

GraphGen:
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_S0DirU/2023/03/22/16-43-52-8b674f03711941e861995a97b7cb8184-58a19a.png)
### 不使用RNN的
#### 基于注意力机制的
GRAN、GRAM、AGE
#### 其他方法
DeepGMG、DeepGG

## 基于自编码器（Autoencoder）的图生成方法
|       方法        |    输入    |      生成方式      |  特征类型   | 多维节点特征 |        公开源码        | 可附加生成条件 |
| :---------------: | :--------: | :----------------: | :---------: | :----------: | :--------------------: | :------------: |
|     VGAE [50]     |   单个图   |   一次生成整个图   |    节点     |      -       |          Yes           |       No       |
| **GraphVAE** [⑤1] | **数据集** | **一次生成整个图** | **节点/边** |      -       | **Yes**[^GraphVAECode] |    **Yes**     |
|  **MPGVAE** [52]  | **数据集** | **一次生成整个图** | **节点/边** |      -       |         **No**         |    **Yes**     |
|    RGVAE [53]     |   数据集   |   一次生成整个图   |   节点/边   |      -       |           No           |       No       |
|   Graphite [54]   |   单个图   |   一次生成整个图   |    节点     |      -       |          Yes           |       No       |
|   NED-VAE [55]    |   数据集   |   一次生成整个图   |   节点/边   |      -       |          Yes           |       No       |
|    DGVAE [56]     |   数据集   |   一次生成整个图   |    节点     |      -       |          Yes           |       No       |
|    JTVAE [57]     |   数据集   |    生成子图结构    |   节点/边   |      -       |          Yes           |       No       |
| **HierVAE** [37]  | **数据集** |  **生成子图结构**  | **节点/边** |      -       | **Yes**[^HierVAECode]  |    **Yes**     |
|   MHG-VAE [58]    |   数据集   |    生成子图结构    |   节点/边   |      -       |          Yes           |       No       |
| MoleculeChef [38] |   数据集   |    生成子图结构    |   节点/边   |      -       |          Yes           |       No       |
|    CGVAE [39]     |   数据集   |     逐节点生成     |   节点/边   |      -       |          Yes           |       No       |
|   DEFactor [40]   |   数据集   |     逐节点生成     |   节点/边   |      -       |           No           |      Yes       |
|    NeVAE [59]     |   数据集   |     逐节点生成     |   节点/边   |      -       |          Yes           |       No       |
|  GraphVRNN [41]   |   数据集   |     逐节点生成     |    节点     |      -       |           No           |       No       |
|  Lim et al. [42]  |   数据集   |     逐节点生成     |   节点/边   |      -       |          Yes           |      Yes       |

[^HierVAECode]: HierVAE Code. https://github.com/wengong-jin/hgraph2graph
[^GraphVAECode]: GraphVAE Code. https://github.com/JiaxuanYou/graph-generation/tree/master/baselines/graphvae

HierVAE对于较大的分子，性能会显著降低。

### 一次生成整个图的方法
### 基于子结构（Substructure）的方法
### 逐节点生成图的方法


## 基于强化学习的图生成方法
|         方法         | 特征类型 | 多维节点特征 | 公开源码 | 可附加生成条件 |
| :------------------: | :------: | :----------: | :------: | :------------: |
|      GCPN [43]       | 节点/边  |              |   Yes    |       No       |
|   Shi et al. [44]    | 节点/边  |              |   Yes    |       No       |
|  Karimi et al. [45]  | 节点/边  |              |   Yes    |      Yes       |
| DeepGraphMolGen [46] | 节点/边  |              |   Yes    |       No       |
|    GraphOpt [47]     | 节点/边  |              |   Yes    |       No       |
|     MNCE-RL [48]     | 节点/边  |              |   Yes    |       No       |
|      GEGL [49]       | 节点/边  |              |   Yes    |       No       |

## 基于生成对抗网络的图生成方法
|        方法         |    输入    |      生成方式      |   特征   | 多维节点特征 |       公开源码        | 可附加生成条件 |
| :-----------------: | :--------: | :----------------: | :------: | :----------: | :-------------------: | :------------: |
|     NetGAN [65]     |   单个图   |        序列        |    -     |              |          Yes          |       No       |
|     MMGAN [66]      |   单个图   |        序列        |    -     |              |          No           |       No       |
| **SHADOWCAST** [67] | **单个图** |      **序列**      | **节点** |              |        **No**         |    **Yes**     |
|     MolGAN [63]     |   数据集   |   一次生成整个图   | 节点/边  |              |          Yes          |       No       |
|  **CONDGEN** [61]   | **数据集** | **一次生成整个图** |    -     |              | **Yes**[^CondGenCode] |    **Yes**     |
|  **TSGG-GAN** [68]  | **数据集** | **一次生成整个图** | **节点** |              |        **No**         |    **Yes**     |
|  VJTNN + GAN [62]   |   数据集   |        序列        | 节点/边  |              |          Yes          |       No       |
| Mol- CycleGAN [69]  |   数据集   |        序列        | 节点/边  |              |          Yes          |       No       |
|   Misc- GAN [70]    |   单个图   |         -          |    -     |              |          Yes          |       No       |


[^CondGenCode]: CondGen Code. https://github.com/KelestZ/CondGen

### 基于随机游走的方法
### 基于整个图的方法
#### GENERAL GRAPH-BASED ADVERSARIAL DGGs
MolGAN
#### GRAPH-TO-GRAPH TRANSLATORS

## 基于流的图生成方法
| 方法          | 生成策略       | 特征类型 | 可附加生成条件 |
| ------------- | -------------- | -------- | -------------- |
| GNF [60]      | 一次生成整个图 | 节点/边  | No             |
| GraphNVP [71] | 一次生成整个图 | 节点/边  | No             |
| GraphAF [35]  | 逐节点生成     | 节点/边  | No             |
| GrAD [36]     | 生成子图结构   | -        | No             |

## 参考文献
