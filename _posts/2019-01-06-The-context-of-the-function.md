---
title: 函数的上下文
key: 20190106
tags: this
---

<!--more-->

**题目描述**

- 将函数 fn 的执行上下文改为 obj 对象

**示例:**

输入

> function () {return this.greeting + ', ' + this.name + '!!!';}, {greeting: 'Hello', name: 'Rebecca'}

输出

> Hello, Rebecca!!!

```javascript
//三种方案
//apply
function speak(fn, obj) {
  return fn.apply(obj);
}
//call
function speak(fn, obj) {
  return fn.call(obj);
}
//bind
function speak(fn, obj) {
  return fn.bind(obj)();
}
```

**在 JavaScript 中，函数是一种对象，其上下文是可以变化的，对应的，函数内的 this 也是可以变化的，函数可以作为一个对象的方法，也可以同时作为另一个对象的方法，可以通过 Function 对象中的 call 或者 apply 方法来修改函数的上下文，函数中的 this 指针将被替换为 call 或者 apply 的第一个参数。将函数 fn 的执行上下文改为 obj 对象，只需要将 obj 作为 call 或者 apply 的第一个参数传入即可。**
