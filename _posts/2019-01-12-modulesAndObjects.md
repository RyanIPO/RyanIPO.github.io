---
title: 模块与对象
key: 20190112
tags: object
---

<!--more-->

**题目描述**

- 完成函数 createModule，调用之后满足如下要求：

1. 返回一个对象
2. 对象的 greeting 属性值等于 str1， name 属性值等于 str2
3. 对象存在一个 sayIt 方法，该方法返回的字符串为 greeting 属性值 + ', ' + name 属性值

**声明对象有两种常见的方式：`var obj = {}`;和 `var obj = new Object()`;。前面一种可以直接在括号中以 `key:value` 的方式定义属性，后一种采用`点运算符`给对象添加属性**

```javascript
//原型模式：
function createModule(str1, str2) {
  function Obj() {
    this.greeting = str1;
    this.name = str2;
  }
  Obj.prototype.sayIt = function() {
    return this.greeting + ", " + this.name;
  };
  return new Obj();
}
//构造函数模式：
function createModule(str1, str2) {
  function Obj() {
    this.greeting = str1;
    this.name = str2;
    this.sayIt = function() {
      return this.greeting + ", " + this.name;
    };
  }
  return new Obj();
}
//创建对象模式：
function createModule(str1, str2) {
  function CreateObj() {
    obj = new Object();
    obj.greeting = str1;
    obj.name = str2;
    obj.sayIt = function() {
      return this.greeting + ", " + this.name;
    };
    return obj;
  }
  return CreateObj();
}
//字面量模式：
function createModule(str1, str2) {
  var obj = {
    greeting: str1,
    name: str2,
    sayIt: function() {
      return this.greeting + ", " + this.name;
    }
  };
  return obj;
}
```

