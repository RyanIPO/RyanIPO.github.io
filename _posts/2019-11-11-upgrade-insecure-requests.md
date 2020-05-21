---
title: upgrade-insecure-requests
key: 20191111
tags: csp http https xss
---

今天产品在线上 chrome 浏览器里面抛出了这样两条警告

:warning: Mixed Content: The page at 'https://somesite.com' was loaded over HTTPS, but requested an insecure audio file 'http://m8.music.126.net/20200521183517/ef8894b3fddff45c1436b51923856135/ymusic/8a5a/b457/1f24/510fed872bac7ef4ff07e8c8ebbfc303.mp3'. This content should also be served over HTTPS, For more information see https://blog.chromium.org/2019/10/no-more-mixed-messages-about-https.html

:warning: Mixed Content: The page at 'https://somesite.com' was loaded over HTTPS, but requested an insecure audio file 'http://m8.music.126.net/20200521183517/ef8894b3fddff45c1436b51923856135/ymusic/8a5a/b457/1f24/510fed872bac7ef4ff07e8c8ebbfc303.mp3'. This content should also be served over HTTPS.

查了相关资料发现这是 "网页安全政策"（Content Security Policy，缩写 CSP）,这是为了防止 跨域脚本攻击 （Cross Site Scripting，缩写 XSS ）。

<!--more-->

## 正文

查阅资料时还发现请求头中有时还会有 `Upgrade-Insecure-Requests: 1` 这个参数。它表示，在 https 页面中，如果调用了 http 资源，那么浏览器就会抛出一些警告或错误。为了改变成这一状况，chrome(谷歌浏览器)会在 http 请求中加入 ‘Upgrade-Insecure-Requests: 1’ ，服务器收到请求后会返回 “Content-Security-Policy: upgrade-insecure-requests” 头（如果后端设置过这个），告诉浏览器，可以把所属本站的所有 http 连接升级为 https 连接。

而上面抛出的两个警告，是告诉我们在 HTTPS 承载的页面上不允许出现 http 请求，查阅资料发现解决这个问题也很简单。两种解决办法：

1. 后端解决(服务器响应头中加入)

   ```php
   header("Content-Security-Policy: upgrade-insecure-requests");
   ```

2. 前端解决(head 标签中加入)

   ```html
   <meta
     http-equiv="Content-Security-Policy"
     content="upgrade-insecure-requests"
   />
   ```

3. 注意：

   - 升级后的链接在服务器端必需有对应的资源。

   - 只会升级网站内部的链接，对于不属于网站同部的链接，则保持默认状态。

   - 并不是所以的浏览器兼容此请求头，兼容表如下
     ![upgrade-insecure-requests.png](https://wx2.sbimg.cn/2020/05/21/upgrade-insecure-requests.png)
     （ps:万恶的 ie。。。）

## 参考

1. [Content Security Policy 入门教程](http://www.ruanyifeng.com/blog/2016/09/csp.html)

2. [CSP: upgrade-insecure-requests](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/upgrade-insecure-requests)

3. [Upgrade Insecure Requests Sample](https://googlechrome.github.io/samples/csp-upgrade-insecure-requests/index.html)

4. [让浏览器不再显示 https 页面中的 http 请求警报](https://www.cnblogs.com/hustskyking/p/upgrade-insecure-requests.html)
