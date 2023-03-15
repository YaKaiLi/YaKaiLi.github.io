---
title: iterm2+xquartz x11转发
date: "2023-03-15"
slug: iterm2-x11-forwarding
tags:
  - Misc
  - Software
---
## 安装xquartz
https://www.xquartz.org/

## 在linux服务器端打开X11转发
```shell
sudo vim /etc/ssh/sshd_config
```
配置转发参数为yes 
```
X11Forwarding yes
X11DisplayOffset 10
```
然后重启ssh服务
```shell
service ssh restart 
```
## 在Mac本地设置


```shell
sudo vim /etc/ssh/ssh_config
```
配置转发参数为yes 
```
ForwardAgent yes
ForwardX11 yes
ForwardX11Trusted yes
XAuthLocation /opt/X11/bin/xauth
```

## 使用
ssh -X username@host
ssh -X nickname