---
title: "linux-Python3-UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)"
date: '2022-11-27'
slug: python3-UnicodeEncodeError
tags:
  - Misc
  - Troubleshooting
  - Python
---

### 错误说明
今天在服务器上使用python3执行python文件时报错。
报错所在行语句：
``` bash
print("读取图片文件耗费时间：%d秒" % time_elapsed)
```
报错信息：
``` bash
UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)
```
### 问题分析
1、是否是文件自身的编码问题
	文件头部存在编码格式说明，并且在我的本机上执行没有问题。所以排除文件自身的问题
2、是否是系统的字符输出编码问题
	执行以下程序检测系统的输出编码
``` bash
>>>import sys
>>>sys.stdout.encoding
'ANSI_X3.4-1968'
```
结果是ANSI_X3.4-1968任何中文都会报错，所以确定是系统的问题
### 解决方法
1、运行python的时候加上PYTHONIOENCODING=utf-8：
``` bash
PYTHONIOENCODING=utf-8 python3 myPythonFile.py
```
2、重新定义标准输出
在文件中加上以下语句：
``` bash
import sys
sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach())
```