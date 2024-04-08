---
title: Aidroid论文复现环境搭建
date: '2023-09-18'
slug: aidroid-paper-experiment-env
tags:
  - Hgnn
  - Malware
  - Paper
---

https://github.com/liangxun/AiDroid/tree/master

docker run --gpus all -it -d --name aidroid -v /home/star5o/dataset:/dataset nvidia/cuda:10.1-cudnn7-devel-ubuntu18.04 /bin/bash

conda create -n aidroid python=3.6

source activate aidroid

