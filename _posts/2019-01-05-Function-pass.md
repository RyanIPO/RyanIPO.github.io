---
title: 函数传参
key: 20190105
tags: 传参
---

<!--more-->

**题目描述**

- 将数组 arr 中的元素作为调用函数 fn 的参数

**示例:**

输入

> `function (greeting, name, punctuation) {return greeting + ', ' + name + (punctuation || '!');}, ['Hello', 'Ellie', '!']`

输出

> `Hello, Ellie!`

```javascript
//用apply
function argsAsArray(fn, arr) {
  return fn.apply(fn, arr);
}
//或者
function argsAsArray(fn, arr) {
  return fn.apply(this, arr);
}
```

```javascript
//用call
function argsAsArray(fn, arr) {
  return fn.call(fn, arr[0], arr[1], arr[2]);
}
//或者
function argsAsArray(fn, arr) {
  return fn.call(this, arr[0], arr[1], arr[2]);
}
```

```javascript
//笨办法
function argsAsArray(fn, arr) {
  return fn(arr[0], arr[1], arr[2]);
}
//ES 6
function argsAsArray(fn, arr) {
  return fn(...arr);
}
```

_调用函数可以使用 call 或者 apply 这两个方法，区别在于 call 需要将传递给函数的参数明确写出来，是多少参数就需要写多少参数。而 apply 则将传递给函数的参数放入一个数组中，传入参数数组即可。_

_思路：每个函数都包含两个非继承而来的方法：apply（）he call（），这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内 this 对象的值。首先，apply（）方法接收两个参数：一个是在其中运行函数的作用域，另一个是参数数组。_
