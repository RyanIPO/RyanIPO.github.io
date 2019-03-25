---
title: 属性遍历
key: 2019011302
tags: for-in
---

<!--more-->

**题目描述**

- 找出对象 obj 不在原型链上的属性(注意这题测试例子的冒号后面也有一个空格~)

1. 返回数组，格式为 key: value
2. 结果数组不要求顺序

**示例:**

输入

> var C = function() {this.foo = 'bar'; this.baz = 'bim';};

> C.prototype.bop = 'bip';

> iterate(new C());

输出

> ["foo: bar", "baz: bim"]

**可以使用 for-in 来遍历对象中的属性，hasOwnproperty 方法能返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性，该属性必须为对象本身的属性。**

```javascript
function iterate(obj) {
  var arr = [];
  //使用for-in遍历对象属性
  for (var key in obj) {
    //判断key是否为对象本身的属性
    if (obj.hasOwnProperty(key)) {
      //将属性和值按格式存入数组
      arr.push(key + ": " + obj[key]);
    }
  }
  return arr;
}
```


