---
title: 国内使用ChatGPT
date: '2023-01-22'
slug: use-chatgpt-in-china
tags:
  - Misc
---

OpenAI有地区限制，第一次登陆`ChatGPT`时使用的香港IP，注册然后登陆进去直接提示`OpenAI's services are not available in your country`，之后更换使用的IP（包括美国）和邮箱依旧提示。解决方法如下：

首先切换到美国IP。然后在`OpenAI's services are not available in your country`提示页按F12打开开发者工具，到【应用-存储-本地存储空间】页把`@@authOspajs`开头的这个密钥删除，再刷新页面，没有 `OpenAI's services are not available in your country`提示了。

根据[这篇](https://readdevdocs.com/blog/makemoney/%E4%B8%AD%E5%9B%BD%E5%8C%BA%E6%B3%A8%E5%86%8COpenAI%E8%B4%A6%E5%8F%B7%E8%AF%95%E7%94%A8ChatGPT%E6%8C%87%E5%8D%97.html)文章注册国外接码平台，充值0.2美元使用印度号码就行。

接下来可以愉快的使用ChatGPT啦。

![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/star5o/Desktop/2023/01/30/13-42-02-32dd6d57c43d1076a0f60197d9f98cfd-9be825.png)