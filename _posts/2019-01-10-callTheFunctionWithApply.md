---
title: 使用 apply 调用函数
key: 20190110
tags: apply
---

<!--more-->

**题目描述**

- 实现函数 callIt，调用之后满足如下条件

1. 返回的结果为调用 fn 之后的结果
2. fn 的调用参数为 callIt 的第一个参数之后的全部参数

```javascript
function callIt(fn) {
  //将arguments转化为数组后，截取第一个元素之后的所有元素
  var args = Array.prototype.slice.call(arguments, 1);
  //调用fn
  var result = fn.apply(null, args);
  return result;
}
```

- 因为 arguments 并非真正的数组，因此要获得 callIt 的第一个参数之后的所有参数，不能直接使用 slice 方法截取，需要先将 arguments 转换为真正的数组才行。有两种常见的方法，

- 一是使用 slice 方法：var args = Array.prototype.slice.call( arguments );

- 二是循环遍历逐一填入新数组。

- 在获得了 args 之后，就可以调用 apply 来执行传入的函数参数。
