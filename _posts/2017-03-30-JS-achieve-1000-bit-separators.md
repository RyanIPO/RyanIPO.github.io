---
title: JavaScript实现千位分隔符
key: 20160520
tags: JavaScript 千位分隔符
---

将普通的数字转换为带千位分隔符格式的数字字符串是一个非常常见的问题，千位分隔符格式的规则是数字的整数部分每三位一组以“，”分节。小数部分不分节 。示例：`19,351,235.235767` 这里有几个常见的实现方法。

<!--more-->

## 1. 方法一

实现思路是将数字转换为字符数组，再循环整个数组， 每三位添加一个分隔逗号，最后再合并成字符串。因为分隔符在顺序上是往 前添加的：比如 `1234567`添加后是`1,234,567` 而不是 `123,456,7` ，所以方便起见可以先把数组倒序，添加完之后再倒序来就是  正常的顺序了。要注意的是如果数字带小数的话，要把小数部分分开处理。

```javascript
function numFormat(num){
    num=num.toString().split(".");  // 分隔小数点
    var arr=num[0].split("").reverse();  // 转换成字符数组并且倒序排列
    var res=[];
    for(var i=0,len=arr.length;i<len;i++){
      if(i%3===0&&i!==0){
         res.push(",");   // 添加分隔符
      }
      res.push(arr[i]);
    }
    res.reverse(); // 再次倒序成为正确的顺序
    if(num[1]){  // 如果有小数的话添加小数部分
      res=res.join("").concat("."+num[1]);
    }else{
      res=res.join("");
    }
    return res;
}

var a=1234567894532;
var b=673439.4542;
console.log(numFormat(a)); // "1,234,567,894,532"
console.log(numFormat(b)); // "673,439.4542"
```

## 2. 方法二

使用JS自带的函数 [`toLocaleString`](https://link.jianshu.com/?t=https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/toLocaleString)

>语法: `numObj.toLocaleString([locales [, options]])`

`toLocaleString()` 方法返回这个数字在特定语言环境下的表示字符串。

```javascript
var a=1234567894532;
var b=673439.4542;

console.log(a.toLocaleString());  // "1,234,567,894,532"
console.log(b.toLocaleString());  // "673,439.454"  （小数部分四舍五入了）
```
要注意的是这个函数在没有指定区域的基本使用时，返回使用默认的语言环境和默认选项格式化的字符串，所以不同地区数字格式可能会有一定的差异。最好确保使用 `locales` 参数指定了使用的语言。
注：我测试的环境下小数部分会根据四舍五入只留下三位。

## 3. 方法三

使用[`正则表达式`](https://link.jianshu.com/?t=https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)和[`replace`](https://link.jianshu.com/?t=https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)函数，相对前两种我更喜欢这种方法，虽然正则有点难以理解。

>replace 语法：`str.replace(regexp|substr, newSubStr|function)`

其中第一个 `RegExp`
对象或者其字面量所匹配的内容会被第二个参数的返回值替换。

```javascript
function numFormat(num){
  var res=num.toString().replace(/\d+/, function(n){ // 先提取整数部分
       return n.replace(/(\d)(?=(\d{3})+$)/g,function(m){
          return m + ",";
        });
  })
  return res;
}

var a=1234567894532;
var b=673439.4542;
console.log(numFormat(a)); // "1,234,567,894,532"
console.log(numFormat(b)); // "673,439.4542"
```

参考阅读：
1. [正则表达式30分钟入门教程](https://link.jianshu.com/?t=http://deerchao.net/tutorials/regex/regex.htm)

2. [String.prototype.replace()](https://link.jianshu.com/?t=https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)