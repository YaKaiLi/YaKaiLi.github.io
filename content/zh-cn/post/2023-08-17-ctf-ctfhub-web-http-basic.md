---
title: CTF入门练习-CTFHUB-HTTP基础
date: '2023-07-31'
slug: ctf-ctfhub-web-http-basic
tags:
  - Ctfhub
  - CTF
  - Writeup
---

打开题目给出的网址过后，显示如下内容的网页：

```
HTTP Method is GET Use CTF**B Method, I will give you flag. 

Hint: If you got 「HTTP Method Not Allowed」 Error, you should request index.php.
```

简单思考一下，它想让我们使用CTFHUB的方式请求该网站，而不是默认的GET。

因此执行
```
curl -X CTFHUB http://challenge-33647dc8ad4fc041.sandbox.ctfhub.com:10800/index.php
```

获得flag

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8"/>
    <title>CTFHub HTTP Method</title>
</head>
<body>

good job! ctfhub{4c6095aa89b04ce531bab9**}

</body>
</html>
```

`该flag不通用，每个人的flag都不同。`