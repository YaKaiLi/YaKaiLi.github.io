---
title: 通过docker安装使用LLaMA的LLM自主代理babyagi
date: '2023-06-06'
slug: install-babyagi-in-docker-with-llama
tags:
  - LLMs
  - LLaMA
  - Paper
---
## 编译LLaMa-cpp
参考：https://mikespook.com/2023/03/%E5%9C%A8-ubuntu-2204-%E4%B8%8A%E8%BF%90%E8%A1%8C-llama-cpp/

## 下载babyagi并配置

参考：https://www.wbolt.com/babyagi.html
git clone https://github.com/yoheinakajima/babyagi.git && cd babyagi

cp .env.example .env

输入Pinecone API密钥和Pinecone环境变量。不要在密钥周围加引号。
```
# Pinecone config
# Uncomment and fill these to switch from local ChromaDB to Pinecone
PINECONE_API_KEY=
PINECONE_ENVIRONMENT=

# API CONFIG
# OPENAI_API_MODEL can be used instead
# Special values:
# human - use human as intermediary with custom LLMs
# llama - use llama.cpp with Llama, Alpaca, Vicuna, GPT4All, etc
LLM_MODEL=llama# alternatively, gpt-4, text-davinci-003, etc
LLAMA_MODEL_PATH=models/llama-13B/ggml-model.bin # ex. models/llama-13B/ggml-model.bin

从Pinecone获得一个API密钥
Pinecone是一个用于存储AI数据的矢量数据库。你可以获得一个免费账户，尽管可能有一个等待名单。你可以通过点击API密钥标签，点击复制按钮或 “Create API Key” 来获得API密钥。另外，注意 “Environment” 的位置（例如：us-central1-gcp）。


docker-compose up
