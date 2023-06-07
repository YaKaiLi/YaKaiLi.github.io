---
title: 通过docker安装LLM自主代理AgentGPT
date: '2023-06-06'
slug: install-agentgpt-in-docker
tags:
  - LLMs
  - ChatGPT
  - Paper
---
<!-- ## 获取Websearch密钥

两种方式都可以。
### Google官方
每天100次搜索免费，之后5美元/1000次搜索。
https://developers.google.com/custom-search/v1/overview?hl=zh-cn

### 第三方
1000次搜索免费，之后0.3美元/1000次搜索。
https://serper.dev/

## 获取生成图像密钥
## DALL-E
不需配置，使用openai api即可。
## Replicate
https://replicate.com/account/api-tokens -->

## 下载并配置

下载：
```bash
git clone https://github.com/reworkd/AgentGPT.git && cd AgentGPT

```
切换到0.5版本分支。使用0.5版本，因为0.6版本和master分支部署完执行总会遇到各种各样的问题。
```bash
git checkout v.0.5.0-beta
```

然后执行。
```bash
./setup.sh --docker
```

之后会提示输入密钥，按照提示输入即可。
```bash
Enter your OpenAI Key (eg: sk...) or press enter to continue with no key:
```

等待完成后即可访问，默认使用3000端口，地址为：http://localhost:3000。
