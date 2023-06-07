---
title: 通过docker安装LLM自主代理AutoGPT-Next-Web
date: '2023-06-06'
slug: install-autogpt-next-web-in-docker
tags:
  - LLMs
  - ChatGPT
  - Paper
---
## 获取Websearch密钥

两种方式都可以。
### Google官方
每天100次搜索免费，之后5美元/1000次搜索。
https://developers.google.com/custom-search/v1/overview?hl=zh-cn

### 第三方
1000次搜索免费，之后0.3美元/1000次搜索。
https://serper.dev/

## 下载并配置

```
git clone https://github.com/Dogtiti/AutoGPT-Next-Web.git && cd AutoGPT-Next-Web
```
选用`AutoGPT-Next-Web`项目，该项目可自定义`API_BASE_URL`，国内访问更流程。

下载完成后，配置.env文件。
```bash
cp .env.example .env

vim .env
```

```vim
#不要在密钥周围加引号。
OPENAI_API_KEY=
NEXT_PUBLIC_WEB_SEARCH_ENABLED=true # 设置启用Websearch。
SERP_API_KEY= # or GOOGLE_API_KEY=
```
然后执行
```
docker-compose -f docker-compose.dev.yml up -d --remove-orphans
```

等待完成后即可访问，默认使用3000端口，地址为：http://localhost:3000。
