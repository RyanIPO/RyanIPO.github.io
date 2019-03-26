---
title: 使用闭包
key: 20190108
tags: this
---

<!--more-->

**题目描述**

- 实现函数 makeClosures，调用之后满足如下条件：

1. 返回一个函数数组 result，长度与 arr 相同
2. 运行 result 中第 i 个函数，即 result[i]()，结果与 fn(arr[i]) 相同

**示例:**

- 输入

> [1, 2, 3], function (x) {return x \* x;}

- 输出

> (3) [ƒ, ƒ, ƒ] //result

> `result[0]`() //1

> `result[1]`() //4

> `result[2]`() //9

```javascript
//使用的是forEach循环
function makeClosures(arr, fn) {
  var result = [];

  arr.forEach(function(e) {
    result.push(
      (function(num) {
        return function() {
          return fn(num);
        };
      })(e)
    );
  });

  return result;
}
```

- 简单的描述闭包：如果在函数 func 内部声明函数 inner，然后在函数外部调用 inner，这个过程即产生了一个闭包。

- 题目要求的是返回一个函数数组，如果在循环中直接像写下面

```javascript
result[i] = function() {
  return fn(arr[i]);
};
//或者
result.push(function() {
  return fn(arr[i]);
});
```

- 那么最终的结果是不正确的，因为在每次迭代的时候，那样的语句后面的方法并没有执行，只是创建了一个函数体为“return fn(arr[i]);”的函数对象而已，当迭代停止时，i 为最终迭代停止的值，在函数被调用时，i 依旧为最终迭代停止的值，因此无法返回正确的结果。

- 为了解决这个问题，需要声明一个匿名函数，并立即执行它。

```javascript
 function(num){
   return function(){
     return fn(arr[num]);
     };
  }(i)
```

- 上面的函数执行后，i 立即传入并被内部函数访问到，因此就能得到正确的结果。闭包允许你引用存在于外部函数中的变量。

- 刚开始看 ES6 直接用 let

```javascript
function makeClosures(arr, fn) {
  var result = new Array();
  for (let i = 0; i < arr.length; i++) {
    result[i] = function() {
      return fn(arr[i]); //let声明的变量只在let所在代码块内有效，因此每次循环的i都是一个新的变量
    };
  }
  return result;
}
```

- 下面是 ES5 的

- 看到题目我首先想到的是使用闭包时因为作用域链引来的副作用，（闭包只能得到包含函数中变量的最后一个值）如果直接用下面第一种写法会导致 result 中每个函数的参数都是 arr[arr.length],在《JavaScript 高级程序设计》书中提到的最典型的解决此问题的方法就是用一个立即执行的匿名函数代替闭包赋值给数组，这个匿名函数有一个参数 num，因为函数参数是按值传递的所以传递给 num 的就是当前 for 循环的值。

- 此外 ES5 提供了 bind 方法，apply(),call(),bind()方法在使用时已经对参数进行了定义

- 又因为在此问题中用的是数组并且需要的是 arr[i]所以用 forEach()方法就不用考虑第一段中提到的问题

```javascript
//这种是错误的写法会导致result中每个函数的参数都是arr[arr.length]
function makeClosures(arr, fn) {
  var result = new Array();
  for (var i = 0; i < arr.length; i++) {
    result[i] = function() {
      return fn(arr[i]);
    };
  }
  return result;
}

//参考《JavaScript高级程序设计》的典型方法
function makeClosures(arr, fn) {
  var result = new Array();
  for (var i = 0; i < arr.length; i++) {
    result[i] = (function(num) {
      return function() {
        return fn(num);
      };
    })(arr[i]);
  }
  return result;
}

//使用ES5的bind()方法
function makeClosures(arr, fn) {
  var result = new Array();
  for (var i = 0; i < arr.length; i++) {
    result[i] = fn.bind(null, arr[i]);
  }
  return result;
}

//使用forEach()
function makeClosures(arr, fn) {
  var result = new Array();
  arr.forEach(function(curr) {
    result.push(function() {
      return fn(curr);
    });
  });
  return result;
}
```
