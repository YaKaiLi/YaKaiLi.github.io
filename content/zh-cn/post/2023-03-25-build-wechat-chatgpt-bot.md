---
title: 搭建chatgpt微信机器人
date: '2023-03-25'
slug: build-wechat-chatgpt-bot
tags:
  - Misc
  - Software
---
## 拉docker
```shell
# pull image
docker pull holegots/wechat-chatgpt
# run container
docker run -d --name wechat-chatgpt \
    -e OPENAI_API_KEY="" \
    -e MODEL="gpt-3.5-turbo" \
    -e DISABLE_GROUP_MESSAGE="false" \
    -e CHAT_PRIVATE_TRIGGER_KEYWORD="小助理" \
    -v $(pwd)/data:/app/data/wechat-assistant.memory-card.json \
    holegots/wechat-chatgpt:latest
        #

# View the QR code to log in to wechat
docker logs -f wechat-chatgpt
```

## compose自己构建
```shell
git clone https://ghproxy.com/https://github.com/fuergaosi233/wechat-chatgpt.git
# Copy the configuration file according to the template
cp .env.example .env
# Edit the configuration file
vim .env
# Start the container
docker-compose up -d
# View the QR code to log in to wechat
docker logs -f wechat-chatgpt
```

