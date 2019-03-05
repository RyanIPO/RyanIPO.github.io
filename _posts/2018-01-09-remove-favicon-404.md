---
title: 去除Chrome页面中GET favicon.ico 404 (Not Found)
key: 2018-01-09
tags: Chrome
---

html5页面中经常会遇见以下问题，总是看着碍眼，那么怎么解决呢？
GET http://localhost:8080/favicon.ico 404 (Not Found)

<!--more-->

解决的方法：

1、做个`favicon.ico`文件放在根目录下，在`head`标签引入favicon.ico文件即可
```
<link href="favicon.ico" rel="shortcut icon">
```
或者

2、在`Stack Overflow`搜索到的，直接在`head`标签插入以下代码也OK
```
 <link rel="shortcut icon" href="#" />
 ```