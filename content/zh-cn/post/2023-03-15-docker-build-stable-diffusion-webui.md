---
title: Docker搭建Stable Diffusion Webui
date: "2023-03-15"
slug: docker-build-stable-diffusion-webui
tags:
  - Misc
  - Software
---
## 环境要求
Docker及docker-compose

docker-compose安装命令：
```shell
apt install docker-compose-plugin
```

## 搭建

```shell
git clone https://github.com/AbdBarho/stable-diffusion-webui-docker.git

cd stable-diffusion-webui-docker

docker compose --profile download up --build # 下载模型文件

docker compose --profile [ui] up --build # 启动服务
```

### ui选择项
- `invoke`: One of the earliest forks, stunning UI Repo by InvokeAI
- `auto`: The most popular fork, many features with neat UI, Repo by AUTOMATIC1111
- `auto-cpu`: for users without a GPU.
- `sygil`: Another great fork Repo by Sygil-Dev
- `sygil-sl`: A second version of the above using streamlit (still in development, has bugs)

