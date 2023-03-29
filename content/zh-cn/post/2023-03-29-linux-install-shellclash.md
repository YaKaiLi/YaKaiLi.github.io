---
title: Linux安装shellclash
date: '2023-03-29'
slug: linux-install-shellclash
tags:
  - Misc
  - Software
---

## 使用curl安装：
```shell
#jsdelivrCDN源
export url='https://fastly.jsdelivr.net/gh/juewuy/ShellClash@master' && sh -c "$(curl -kfsSl $url/install.sh)" && source /etc/profile &> /dev/null
```

## 使用wget安装：
```shell
#Release版本-jsdelivrCDN源
export url='https://fastly.jsdelivr.net/gh/juewuy/ShellClash@master' && wget -q --no-check-certificate -O /tmp/install.sh $url/install.sh  && sh /tmp/install.sh && source /etc/profile &> /dev/null 
```