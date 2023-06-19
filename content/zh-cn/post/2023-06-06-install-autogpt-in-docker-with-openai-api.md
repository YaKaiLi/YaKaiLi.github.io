---
title: 通过docker安装使用Openai API的LLM自主代理Auto-GPT
date: '2023-06-07'
slug: install-autogpt-in-docker-with-openai-api
tags:
  - LLMs
  - ChatGPT
  - Paper
---

## 下载并配置
自行构建镜像和使用官方镜像两种方式都可以。
### 自行构建镜像
#### 下载
参考官方文档：https://docs.agpt.co/setup/
```bash
git clone https://github.com/Significant-Gravitas/Auto-GPT.git git-Auto-GPT && cd git-Auto-GPT
```
切换到0.4.0版本分支（官方文档建议不要使用`master`分支）。
```bash
git checkout v0.4.0
```
#### 配置插件
```bash
curl -L -o ./plugins/Auto-GPT-Plugins.zip https://github.com/Significant-Gravitas/Auto-GPT-Plugins/archive/refs/heads/master.zip

```
#### 配置环境变量
```bash
cp .env.template .env
vim .env
```

配置OpenAI API密钥，不带任何引号或空格。
```bash
OPENAI_API_KEY=
``` 

配置谷歌搜索API，不带任何引号或空格。
```bash
GOOGLE_API_KEY=
CUSTOM_SEARCH_ENGINE_ID=
```

#### 运行
```bash 
docker-compose build auto-gpt

docker-compose run --rm auto-gpt
# or docker-compose run --rm auto-gpt --gpt3only --continuous
# 
 
```

### 使用官方镜像

#### 创建文件夹
```
mkdir Auto-GPT
cd Auto-GPT
```
#### 创建docker-compose.yml
```bash
vim docker-compose.yml
```
```yaml
version: "3.9"
services:
  auto-gpt:
    image: significantgravitas/auto-gpt
    env_file:
      - .env
    profiles: ["exclude-from-up"]
    volumes:
      - ./auto_gpt_workspace:/app/autogpt/auto_gpt_workspace
      - ./data:/app/data
      ## allow auto-gpt to write logs to disk
      - ./logs:/app/logs
      ## hot fix missing prompt_settings.yaml
      - ./prompt_settings.yaml:/app/prompt_settings.yaml
      ## uncomment following lines if you want to make use of these files
      ## you must have them existing in the same folder as this docker-compose.yml
      #- type: bind
      #  source: ./azure.yaml
      #  target: /app/azure.yaml
      #- type: bind
      #  source: ./ai_settings.yaml
      #  target: /app/ai_settings.yaml
```
#### 创建prompt_settings.yaml配置文件
官方文档里并没有这一步骤，但是我在运行时发现缺少这个文件会报错，所以需要创建这个文件。
```bash
vim prompt_settings.yaml
```
该文件内容与官方文档中的`prompt_settings.yaml`内容相同，即如下。

https://github.com/Significant-Gravitas/Auto-GPT/blob/master/prompt_settings.yaml
```yaml
constraints: [
  '~4000 word limit for short term memory. Your short term memory is short, so immediately save important information to files.',
  'If you are unsure how you previously did something or want to recall past events, thinking about similar events will help you remember.',
  'No user assistance',
  'Exclusively use the commands listed below e.g. command_name'
]
resources: [
  'Internet access for searches and information gathering.',
  'Long Term memory management.',
  'GPT-3.5 powered Agents for delegation of simple tasks.',
  'File output.'
]
performance_evaluations: [
  'Continuously review and analyze your actions to ensure you are performing to the best of your abilities.',
  'Constructively self-criticize your big-picture behavior constantly.',
  'Reflect on past decisions and strategies to refine your approach.',
  'Every command has a cost, so be smart and efficient. Aim to complete tasks in the least number of steps.',
  'Write all code to a file.'
]
```

#### 创建.env配置文件
```bash
vim .env
```
```conf
OPENAI_API_KEY=
GOOGLE_API_KEY=
CUSTOM_SEARCH_ENGINE_ID=
```
执行
```bash
docker pull significantgravitas/auto-gpt

docker-compose run --rm auto-gpt
# or docker-compose run --rm auto-gpt --gpt3only --continuous 
# gpt3only为仅使用GPT-3.5，continuous为自动持续运行。
```
