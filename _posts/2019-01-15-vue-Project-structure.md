---
title: vue项目结构
key: 20190115
tags: vue-cli vue vue-router webpack
---

我在前面已经学习过了如何用 vue-cli 初始化一个 vue 项目，现在详细了解一下一个 vue 项目的项目结构。

<!--more-->

## 项目目录和文件结构

![项目目录和文件结构](https://ws1.sinaimg.cn/large/a5caea9fgy1g1746ordilj20820aw74h.jpg)

如上图所示，我们的目录结构就是这样的了。

<div class="table-box"><table>
<thead>
<tr>
  <th>目录/文件</th>
  <th>说明</th>
</tr>
</thead>
<tbody><tr>
  <td>build</td>
  <td>这个是我们最终发布的时候会把代码发布在这里，在开发阶段，我们基本不用管。</td>
</tr>
<tr>
  <td>config</td>
  <td>配置目录，默认配置没有问题，所以我们也不用管</td>
</tr>
<tr>
  <td>node_modules</td>
  <td>这个目录是存放我们项目开发依赖的一些模块，这里面有很多很多内容，不过高兴的是，我们也不用管</td>
</tr>
<tr>
  <td>src</td>
  <td>我们的开发目录，基本上绝大多数工作都是在这里开展的</td>
</tr>
<tr>
  <td>static</td>
  <td>资源目录，我们可以把一些图片啊，字体啊，放在这里。</td>
</tr>
<tr>
  <td>test</td>
  <td>初始测试目录，没用，删除即可</td>
</tr>
<tr>
  <td>.xxxx文件</td>
  <td>这些是一些配置文件，包括语法配置，git配置等。基本不用管，放着就是了</td>
</tr>
<tr>
  <td>index.html</td>
  <td>首页入口文件，基本不用管，如果是开发移动端项目，可以在<code>head</code>区域加上你合适的<code>meta</code>头</td>
</tr>
<tr>
  <td>package.json</td>
  <td>项目配置文件。前期基本不用管，但是你可以找一下相关的资料，学习一下里面的各项配置。至少，要知道分别是干嘛的。初期就不管了。</td>
</tr>
<tr>
  <td>README.md</td>
  <td>不用管</td>
</tr>
</tbody>
</table>
</div>

如上，基本上就是这么个情况。重要的，还是src文件夹。

## SRC文件夹的情况

![SRC文件夹的情况](https://ws1.sinaimg.cn/large/a5caea9fgy1g174d9xhxyj208g05raa1.jpg)

如上图所示，这是src文件夹下面的初始情况，里面有一些示例代码之类的。比如，它吧logo放在assets文件夹里面。我个人很不喜欢这么做，因为代码是代码，资源是资源，各归其位比较好。

commponents目录里面放了一个演示的组件文件，你可以打开看下。当然，也可以直接删除，然后根据我的博文往下走。

App.vue是项目入口文件。当然，我们需要改造，改造成我们可以使用的样子的。后面的博文会说。

main.js这是项目的核心文件。全局的配置都在这个文件里面配置，我后面会详细的讲这里怎么搞。

## 整理目录

上面只是让大家了解一下具体是什么情况，下面，我们开始动手，把不想管的干掉，然后把src变成这个样子:

![整理目录](https://ws1.sinaimg.cn/large/a5caea9fgy1g174nwvbxsj208j0cv3yq.jpg)

如上图所示，把文件夹和文件都新建好，后面的博文我会详细给出每个文件的代码的。这里，都新建空文件即可。注意，我是用scss来写css文件的。所以看官你最好也学习一下scss的相关内容，我的博客里面有，搜索也是一大把。

<div class="table-box"><table>
<thead>
<tr>
  <th>文件\目录</th>
  <th>说明</th>
</tr>
</thead>
<tbody><tr>
  <td>component</td>
  <td>组件文件夹我们写的一些公用的内容可以放在这里的。</td>
</tr>
<tr>
  <td>config</td>
  <td>核心配置文件夹</td>
</tr>
<tr>
  <td>frame</td>
  <td>存放自路由的文件夹</td>
</tr>
<tr>
  <td>page</td>
  <td>项目模板文件夹,所有的页面文件全部存放与此，后面会根据需要来建立各种子目录</td>
</tr>
<tr>
  <td>style</td>
  <td>样式存放目录</td>
</tr>
</tbody>
</table>
</div>

>vue支持每一个模板里面写css，这样可以做到随用随取。但是，我个人不太喜欢这样，我还是喜欢吧css给单独放出来，因为这样便于整理，另外，使用scss的朋友都知道，我们会预设大量的变量，代码片供我们在写css的时候使用，如果每个模板文件里面都需要引用一次那是及其操蛋的。

参考:[Vue2+VueRouter2+webpack 构建项目实战（二）目录以及文件结构](http://blog.csdn.net/fungleo/article/details/53171614)