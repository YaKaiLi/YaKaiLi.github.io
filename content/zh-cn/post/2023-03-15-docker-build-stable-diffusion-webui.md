---
title: docker搭建stable diffusion webui
date: "2023-03-15"
slug: docker-build-stable-diffusion-webui
tags:
  - Misc
  - Software
---

docker pull nvidia/cuda:11.7.0-devel-ubuntu22.04

docker run --gpus all -it -d --name sd -v /home/star5o/software/stable-diffusion-webui:/stable-diffusion-webui -v /home/star5o/dataset:/dataset -p 7860:7860 nvidia/cuda:11.7.0-devel-ubuntu22.04 /bin/bash

apt update
apt install sudo wget git vim

adduser sd 
adduser sd sudo

apt install software-properties-common -y
add-apt-repository ppa:deadsnakes/ppa
apt update
sudo apt install python3.10
sudo apt install python3.10-venv

vim ~/.bashrc
```
export PATH=/usr/local/cuda/bin:$PATH
export PATH=/home/sd/.local/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

## 方案1:使用Anaconda
conda create --name sd python=3.10.6

git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
cd stable-diffusion-webui
python launch.py

## 方案2:直接安装python


