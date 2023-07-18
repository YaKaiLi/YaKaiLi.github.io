---
title: 通过docker安装使用GPT学术优化
date: '2023-07-13'
slug: build-academic-gpt-in-docker
tags:
  - ChatGPT
  - Paper
---


```shell
git clone https://github.com/binary-husky/gpt_academic.git

cd gpt_academic

vim config.py

docker build -t gpt-academic .

docker run -d -it -p 50923:50923 -v ~/LLMs:/LLMs gpt-academic
```