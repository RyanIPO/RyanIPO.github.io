---
title: Github Pages 搭建流程
key: 20170202
tags: githubPages
---

github Pages可以被认为是用户编写的、托管在github上的静态网页。

<!--more-->

如果你对编程有所了解，就一定听说过github。它号称程序员的Facebook，有着极高的人气，许多重要的项目都托管在上面。
简单说，它是一个具有版本管理功能的代码仓库，每个项目都有一个主页，列出项目的源文件。
{:.info}

但是对于一个新手来说，看到一大堆源码，只会让人头晕脑涨，不知何处入手。他希望看到的是，一个简明易懂的网页，说明每一步应该怎么做。因此，github就设计了Pages功能，允许用户自定义项目首页，用来替代默认的源码列表。所以，github Pages可以被认为是用户编写的、托管在github上的静态网页。
{:.info}

github提供模板，允许站内生成网页，但也允许用户自己编写网页，然后上传。有意思的是，这种上传并不是单纯的上传，而是会经过Jekyll程序的再处理。
{:.info}

下面，我举一个实例，演示如何在github上搭建github Pages，你可以跟着一步步做。为了便于理解，这个github Pages只有最基本的功能。
在搭建之前，你必须已经安装了git，并且有github账户。
{:.warning}

**第一步，创建项目。**

在你的电脑上，建立一个目录，作为项目的主目录。我们假定，它的名称为Pages_demo。

```
　　$ mkdir Pages_demo
```

对该目录进行git初始化。

```
　　$ cd Pages_demo

　　$ git init
```

*然后，创建一个没有父节点的分支`gh-pages`。因为github规定，只有该分支中的页面，才会生成网页文件。*

```
　　$ git checkout --orphan gh-pages
```
    
以下所有动作，都在该分支下完成。


**第二步，创建 index.html 文件**

在 index.html 中写入以下内容：

```html
<!DOCTYPE html>
<html>
<head>　　　　
    <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <title>
        这是我自己创建的github Pages！
    </title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }

        body {
            width: 100%;
        }

        p {
            text-align: center;
            font-size: 50px;
            width: 50%;
            margin: 0 auto;
            font-weight: 700;
        }
    </style>
</head>
<body>
    <p>Hello World!</p>　　
</body>
</html>
```

**第三步，发布内容。**

现在，这个简单的github Pages就可以发布了。先把所有内容加入本地git库。
```
　　$ git add .

　　$ git commit -m "first post"
```
然后，前往github的网站，在网站上创建一个名为githubPages的库。接着，再将本地内容推送到github上你刚创建的库。注意，下面命令中的username，要替换成你的username。
```
　　$ git remote add origin https://github.com/username/githubPages.git

　　$ git push origin gh-pages
```
上传成功之后，等10分钟左右，访问 http://username.github.com/githubPages/ 就可以看到github Pages已经生成了（将username换成你的用户名）。

下面是我自己搭建的 GitHub pages。
![image](/assets/images/githubPages.png.jpg){:.rounded}

参考[github Pages和Jekyll入门--阮一峰的网络日志](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)