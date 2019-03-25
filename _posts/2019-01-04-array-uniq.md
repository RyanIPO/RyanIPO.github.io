---
title: 数组去重
key: 20190104
tags: array
---

<!--more-->

**题目描述**

- 为 Array 对象添加一个去除重复项的方法

**示例:**

输入

> [false, true, undefined, null, NaN, 0, 1, {}, {}, 'a', 'a', NaN]

输出

> [false, true, undefined, null, NaN, 0, 1, {}, {}, 'a']

```javascript
Array.prototype.uniq = function() {
  var resArr = [];
  var flag = true;

  for (var i = 0; i < this.length; i++) {
    if (resArr.indexOf(this[i]) == -1) {
      if (this[i] != this[i]) {
        //排除 NaN
        if (flag) {
          resArr.push(this[i]);
          flag = false;
        }
      } else {
        resArr.push(this[i]);
      }
    }
  }
  return resArr;
};
```
