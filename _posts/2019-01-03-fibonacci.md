---
title: 斐波那契数列
key: 20190103
tags: fibonacci
---

<!--more-->

```javascript
//一、递归解法
function fibonacci(n) {
  return n <= 2 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
}
```

```javascript
//二、循环解法
function fibonacci(n) {
  var num1 = 1;
  var num2 = 1;
  for (var i = 2; i < n; i++) {
    num2 += num1;
    num1 = num2 - num1;
  }
  return num2;
}
```
