---
title: 《Interpreting Machine Learning Models》阅读笔记
date: '2023-02-21'
slug: build-latex-env-in-m1-macbook
tags:
  - Misc
  - Software
---

通过docker安装
```shell
docker run -itd --name chatgpt-web --restart=always \
 -e APIKEY=换成你的key \
 -e MODEL=gpt-3.5-turbo-0301 \
 -e MAX_TOKENS=512 \
 -e TEMPREATURE=0.9 \
 -e TOP_P=1 \
 -e FREQ=0.0 \
 -e PRES=0.6 \
 -p 8088:8088 \
 qingshui869413421/chatgpt-web:latest
 #这个不太行 https://github.com/869413421/chatgpt-web
```

这个不错：https://github.com/Chanzhaoyu/chatgpt-web

