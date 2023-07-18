---
title: 一个公钥
date: '2023-07-13'
slug: gen-key-for-ssh-and-git
tags:
  - ChatGPT
  - Paper
---
## 生成密钥
先通过运行以下代码来生成一个默认 `~/.ssh/id_rsa`的密钥：
```shell
ssh-keygen -t rsa 
```
对于保存密钥的位置，按回车键接受默认位置。一个私钥`~/.ssh/id_rsa`和公钥 `~/.ssh/id_rsa.pub` 将在默认的 `SSH` 位置 `~/.ssh/` 创建。

## 将公钥添加到服务器中

将`~/.ssh/id_rsa.pub`的内容复制到服务器的`~/.ssh/authorized_keys`文件中：

如此即可免密登陆ssh。

## 将公钥添加到git中

### Github

进入`https://github.com/settings/keys`，将`~/.ssh/id_rsa.pub`的内容添加进SSH keys中。

