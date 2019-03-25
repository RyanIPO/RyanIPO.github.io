---
title: 二进制转换
key: 20190113
tags: Binary
---

<!--more-->

**题目描述**

- 获取数字 num 二进制形式第 bit 位的值。注意：

1. bit 从 1 开始
2. 返回 0 或 1
3. 举例：2 的二进制为 10，第 1 位为 0，第 2 位为 1

**示例:**

输入

> 128, 8

输出

> 1

```javascript
//使用按位操作符
function valueAtBit(num, bit) {
  return (num >> (bit - 1)) & 1;
}

//使用num.toString(2)
function valueAtBit(num, bit) {
  var s = num.toString(2);
     return s[s.length - bit];
 }
```

- 有关按位操作符可以参考官方文档[按位操作符](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)

- 通过num.toString(2)能直接将num转换为2进制数格式的字符串，利用下标就能将对应值取出来。题目返回的数字是从右往左，因此下标为倒数。

