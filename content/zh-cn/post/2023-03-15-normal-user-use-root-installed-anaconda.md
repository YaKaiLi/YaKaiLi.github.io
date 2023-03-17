---
title: 普通用户使用root用户安装的anaconda
date: "2023-03-15"
slug: normal-user-use-root-installed-anaconda
tags:
  - Misc
  - Software
---
首先，root用户安装anaconda的时候，需要安装在普通用户可以访问的目录下，比如/usr/local、/opt、/home之类的

其次，普通用户登陆后，需要执行一下conda init 使conda的路径等系统环境变量信息写入当前用户的bashrc下

