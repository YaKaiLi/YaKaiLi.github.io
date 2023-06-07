---
title: 通过docker安装使用LLaMA的LLM自主代理babyagi
date: '2023-06-06'
slug: install-babyagi-in-docker-with-llama
tags:
  - LLMs
  - LLaMA
  - Paper
---
## 获取Pinecone API密钥
Pinecone是一个用于存储AI数据的矢量数据库。通过点击API密钥标签，点击复制按钮或 “Create API Key” 来获得API密钥。另外，注意 “Environment” 的位置（例如：us-central1-gcp）。

## 使用GPT
### 下载babyagi并配置

#### 下载

```bash
git clone https://github.com/yoheinakajima/babyagi.git && cd babyagi
```
#### 配置

```bash
cp .env.example .env
vim .env
```
##### 配置密钥
输入Pinecone API密钥和Pinecone环境变量。不要在密钥周围加引号。
```
PINECONE_API_KEY=
PINECONE_ENVIRONMENT=

LLM_MODEL=gpt-3.5-turbo # 默认值，不需修改。
```
##### 配置目标任务
设置OBJECTIVE和INITIAL_TASK，不要把它们放在引号里，但要使用自然语言。OBJECTIVE应该是你想要完成的事情，INITIAL_TASK应该是第一个开始的任务。
```bash
# RUN CONFIG
OBJECTIVE=Solve world hunger
# For backwards compatibility
INITIAL_TASK=Write some code to make a platformer game
```

### 运行
```bash
docker-compose up
```

## 使用LLaMA
### 编译LLaMa-cpp
参考：https://mikespook.com/2023/03/%E5%9C%A8-ubuntu-2204-%E4%B8%8A%E8%BF%90%E8%A1%8C-llama-cpp/

### 配置babyagi

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


docker-compose up
