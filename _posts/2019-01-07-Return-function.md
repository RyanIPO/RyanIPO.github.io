---
title: 返回函数
key: 20190107
tags: this
---

<!--more-->

**题目描述**

- 实现函数 functionFunction，调用之后满足如下条件：

1. 返回值为一个函数 f
2. 调用返回的函数 f，返回值为按照调用顺序的参数拼接，拼接字符为英文逗号加一个空格，即 ', '
3. 所有函数的参数数量为 1，且均为 String 类型

**示例:**

输入

> functionFunction('Hello')('world')

输出

> Hello, world

```javascript
function functionFunction(str) {
  var f = function(s) {
    return str + ", " + s;
  };
  return f;
}
```

```javascript
//执行过程
//functionFunction('Hello')('world')

//functionFunction('Hello') ---->  f

f = function(s) {
  return "Hello" + ", " + s;
};

f("world"); //Hello, world
```

**首先执行 functionFunction('Hello')，传入参数 str，然后返回函数 f，f 与('world')组合，执行 f('world')，传入参数 s，f 返回 str+", "+s，即 Hello, world。注意中间的逗号后面有一个空格。**
