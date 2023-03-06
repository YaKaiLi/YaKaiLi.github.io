---
title: 《Interpreting Machine Learning Models》阅读笔记
date: '2023-02-21'
slug: build-latex-env-in-m1-macbook
tags:
  - Misc
  - Software
---

# 方案一
来源于https://github.com/869413421/chatgpt-web

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
```

# 方案二
来源：https://github.com/Chanzhaoyu/chatgpt-web

通过Docker安装
```shell
git clone https://github.com/Chanzhaoyu/chatgpt-web.git

docker build -t chatgpt-web .

# 前台运行
docker run --name chatgpt-web --rm -it -p 3002:3002 --env OPENAI_API_KEY=your_api_key chatgpt-web

# 后台运行
docker run --name chatgpt-web -d -p 3002:3002 --env OPENAI_API_KEY=your_api_key chatgpt-web

# 运行地址
http://localhost:3002/

```

# 服务器位置
使用国外的容器托管平台：Railway或Vercel等。
