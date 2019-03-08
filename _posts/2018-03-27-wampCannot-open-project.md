---
title: Wamp项目打不开
key: 20180327
tags: wamp
---

使用wampserver能启动localhost但不能打开自己的本地项目，这是因为它推荐你使用虚拟主机来运行本地项目，不过如果你不想添加虚拟主机，也可以解决。

<!--more-->

在wamp下的www目录下找到 `index.php` ，修改如下代码： 

`修改前：`{:.error}

```php
while (($file = readdir($handle))!==false)
{
    if (is_dir($file) && !in_array($file,$projectsListIgnore))
    {
        $projectContents .= '<li><a href="';
        if($suppress_localhost)
            $projectContents .= 'http://'.$file.$UrlPort.'/"';  //需要改动的地方
        else
            $projectContents .= 'http://localhost'.$UrlPort.'/'.$file.'/"';//需要改动的地方
        $projectContents .= '>'.$file.'</a></li>';
    }
}
```

`修改后：`{:.success}

```php
while (($file = readdir($handle))!==false)
{
    if (is_dir($file) && !in_array($file,$projectsListIgnore))
    {
        $projectContents .= '<li><a href="';
        if($suppress_localhost)
            $projectContents .= 'http://localhost/'.$file.$UrlPort.'/"';  //改动后的
        else
            $projectContents .= 'http://localhost/'.$UrlPort.'/'.$file.'/"';//改动后的
        $projectContents .= '>'.$file.'</a></li>';
    }
}
```

重新启动wampserver即可打开。

注意：它会提示使用这种方法是不好的，它更推荐使用虚拟主机来运行项目。
{:.warning}

我也推荐使用虚拟主机，毕竟开箱即用。
{:.info}
