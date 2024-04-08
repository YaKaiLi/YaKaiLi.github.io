---
title: Hawk论文复现环境搭建
date: '2023-09-18'
slug: hawk-paper-experiment-env
tags:
  - Hgnn
  - Malware
  - Paper
---

https://github.com/RingBDStack/HAWK

docker pull tensorflow/tensorflow:1.12.0-devel-gpu-py3

docker run --gpus all -it -d --name hawk -v /home/star5o/dataset:/dataset tensorflow/tensorflow:1.12.0-devel-gpu-py3 

docker exec -it hawk bash

pip install scikit-learn

运行后发现项目中核心的models文件夹确实，遂作罢。

