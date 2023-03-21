---
title: 使用 Cloudflare Workers 解决 OpenAI 和 ChatGPT 的 API 无法访问的问题
date: "2023-03-16"
slug: use-cloudflare-workers-for-openai-api-in-china
tags:
  - Misc
  - Software
---
参考：
https://github.com/noobnooc/noobnooc/discussions/9

主要流程（步骤3和4可省略）：

1、新建一个 Cloudflare Worker

2、将 https://gist.github.com/noobnooc/d0407b5fb81cff9d36f981170b99d4e6 里的代码粘贴到 Worker 中并部署

3、给 Worker 绑定一个域名

4、使用自己的域名代替 api.openai.com

## 域名托管转到Cloudflare
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_ixpjzt/2023/03/16/21-18-33-6ee6a9f8538bfb65ab6a4a18afaac7fe-a3b82d.png)
Websites->Add Site
接下来输入需要转入的域名，点击Add Site
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_iYBytI/2023/03/16/21-19-35-e01e0d43d9e3873e31441edc950a5861-9036c9.png)
选择free套餐。
根据 Cloudflare 的提示，在域名注册商处将 NS 修改到 Cloudflare 指定的地址，等待域名解析成功后，即可进行后续操作。

## 创建一个Worker
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_b6yMwo/2023/03/16/21-33-15-f7f9fd81cfdff09ffc50710ff6ae0984-3ff856.png)
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_xkOd55/2023/03/16/21-35-12-a3fc8af1b3d55d4736f00a2981c54806-60a891.png)

### 修改 Cloudflare Worker 的代码

```js
const TELEGRAPH_URL = 'https://api.openai.com';

addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url);
  url.host = TELEGRAPH_URL.replace(/^https?:\/\//, '');

  const modifiedRequest = new Request(url.toString(), {
    headers: request.headers,
    method: request.method,
    body: request.body,
    redirect: 'follow'
  });

  const response = await fetch(modifiedRequest);
  const modifiedResponse = new Response(response.body, response);

  // 添加允许跨域访问的响应头
  modifiedResponse.headers.set('Access-Control-Allow-Origin', '*');

  return modifiedResponse;
}

```
或
```
https://gist.github.com/YaKaiLi/3106669ded79d4918a6f51f8fd322c2e
```



## 绑定自定义域名
![](https://blog-oss-1252232218.cos.ap-beijing.myqcloud.com/fix-dir/TemporaryItems/NSIRD_screencaptureui_427ZgX/2023/03/16/21-50-11-87105f65bd8e4f8eaeb8e5af5139889f-d2ae1a.png)

至此便大功告成。