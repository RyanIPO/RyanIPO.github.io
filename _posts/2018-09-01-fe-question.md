---
title: fe
key: 20180901
tags: fe
---

## javascript:

### JavaScript 中如何检测一个变量是一个 String 类型？请写出函数实现

```javascript
typeof obj === "string";
typeof obj === "string";
obj.constructor === String;

// constructor判断对象的类型，会比typeof更精确，constructor能获取一些复杂对象的类型，typeof做不到。
```

### 请用 js 去除字符串空格？

#### 方法一：使用 replace 正则匹配的方法

去除所有空格: str = str.replace(/\s\*/g,"");

// replace() 方法返回一个由替换值（replacement）替换一些或所有匹配的模式（pattern）后的新字符串。模式可以是一个字符串或者一个正则表达式，替换值可以是一个字符串或者一个每次匹配都要调用的回调函数。原字符串不会改变。
// \s 匹配一个空白符，包括空格、制表符、换页符、换行符和其他 Unicode 空格。
// \s\* 匹配前面的模式 \s 0 或 多次。
// g 全局匹配

去除两头空格: str = str.replace(/^\s*|\s*\$/g,"");

// ^ 开头 \$ 结尾 | 或

去除左空格： str = str.replace( /^\s\*/, “”);

去除右空格： str = str.replace(/(\s\*\$)/g, "");

#### 方法二：使用 str.trim()方法

str.trim()局限性：无法去除中间的空格

// trim() 方法会从一个字符串的两端删除空白字符。在这个上下文中的空白字符是所有的空白字符 (space, tab, no-break space 等) 以及所有行终止符字符（如 LF，CR）。
// trim() 方法并不影响原字符串本身，它返回的是一个新的字符串。

同理，str.trimLeft()，str.trimRight()分别用于去除字符串左右空格。

#### 方法三：使用 jquery,\$.trim(str)方法

\$.trim(str)局限性：无法去除中间的空格

### 你如何获取浏览器 URL 中查询字符串中的参数？

测试地址为：http://www.runoob.com/jquery/misc-trim.html?channelid=12333&name=xiaoming&age=23

实例如下：

```javascript
function showWindowHref() {
  var sHref = window.location.href;
  // location.href 属性返回当前页面的 URL。
  var args = sHref.split("?");
  // split() 方法使用指定的分隔符字符串将一个String对象分割成字符串数组，以将字符串分隔为子字符串，以确定每个拆分的位置。
  if (args[0] == sHref) {
    // 没有参数，返回空
    return "";
  }
  // 有参数，要问号后面的
  var arr = args[1].split("&");
  // 参数分割
  var obj = {};
  for (var i = 0; i < arr.length; i++) {
    var arg = arr[i].split("=");
    // 分割
    obj[arg[0]] = arg[1];
    // 对象设置键值对
  }
  return obj;
}
var herf = showWindowHref(); // obj
console.log(herf["name"]); //xiaoming
```

### js 字符串操作函数

concat() – 将两个或多个字符的文本组合起来，返回一个新的字符串。

indexOf() – 返回字符串中一个子串第一处出现的索引。如果没有匹配项，返回 -1 。

charAt() – 返回指定位置的字符。

lastIndexOf() – 返回字符串中一个子串最后一处出现的索引，如果没有匹配项，返回 -1 。

match() – 检查一个字符串是否匹配一个正则表达式。

substr() 函数 -- 返回从 string 的 startPos 位置，长度为 length 的字符串

substring() – 返回字符串的一个子串。传入参数是起始位置和结束位置。

slice() – 提取字符串的一部分，并返回一个新字符串。

replace() – 用来查找匹配一个正则表达式的字符串，然后使用新字符串代替匹配的字符串。

search() – 执行一个正则表达式匹配查找。如果查找成功，返回字符串中匹配的索引值。否则返回 -1 。

split() – 通过将字符串划分成子串，将一个字符串做成一个字符串数组。

length – 返回字符串的长度，所谓字符串的长度是指其包含的字符的个数。

toLowerCase() – 将整个字符串转成小写字母。

toUpperCase() – 将整个字符串转成大写字母。

### 怎样添加、移除、移动、复制、创建和查找节点？

1）创建新节点
createDocumentFragment() //创建一个 DOM 片段
createElement() //创建一个具体的元素
createTextNode() //创建一个文本节点

2）添加、移除、替换、插入
appendChild() //添加
removeChild() //移除
replaceChild() //替换
insertBefore() //插入

3）查找
getElementsByTagName()//通过标签名
getELementsByName()//通过元素的 name 属性的值
getElementsByClassName()//
querySelector()//querySelector() 方法返回文档中匹配指定 CSS 选择器的一个元素。比如获取文档中 id="demo" 的元素：document.querySelector("#demo");
querySelectorAll()//注意： querySelector() 方法仅仅返回匹配指定选择器的第一个元素。如果你需要返回所有的元素，请使用 querySelectorAll() 方法替代。
getElementById()//通过元素 id，唯一性

### 写出 3 个使用 this 的典型应用

#### （1）、在 html 元素事件属性中使用，如：

```html
<input type="”button”" onclick="”showInfo(this);”" value="”点击一下”" />
```

#### （2）、构造函数

```javascript
function Animal(name, color) {
  this.name = name;
  this.color = color;
}
```

#### （3）、input 点击，获取值

```html
<input type="button" id="text" value="点击一下" />
<script type="text/javascript">
  var btn = document.getElementById("text");
  btn.onclick = function() {
    alert(this.value); //此处的this是按钮元素
  };
</script>
```

#### （4）、apply()/call()求数组最值

```JavaScript
var  numbers = [5, 458 , 120 , -215 ];
var  maxInNumbers = Math.max.apply(this, numbers);//apply 数组
console.log(maxInNumbers);  // 458
var maxInNumbers = Math.max.call(this,5, 458 , 120 , -215);//call 一个一个参数
console.log(maxInNumbers);  // 458
```

### 比较 typeof 与 instanceof？

相同点：JavaScript 中 typeof 和 instanceof 常用来判断一个变量是否为空，或者是什么类型的。

typeof 的定义和用法：返回值是一个字符串，用来说明变量的数据类型。

细节：

(1)、typeof 一般只能返回如下几个结果：number,boolean,string,function,object,undefined。

(2)、typeof 来获取一个变量是否存在，如 if(typeof a!="undefined"){alert("ok")}，而不要去使用 if(a) 因为如果 a 不存在（未声明）则会出错。

(3)、对于 Array,Null 等特殊对象使用 typeof 一律返回 object，这正是 typeof 的局限性。

Instanceof 定义和用法：instanceof 用于判断一个变量是否属于某个对象的实例。

实例演示：

```javascript
a instanceof b ? alert("true") : alert("false"); //a是b的实例？真:假

var a = new Array();
alert(a instanceof Array); // true
alert(a instanceof Object); // true

// 如上，会返回 true，同时 alert(a instanceof Object) 也会返回 true;这是因为 Array 是 object 的子类。

function test() {}
var a = new test();
alert(a instanceof test); // true

// 细节：
// (1)、如下，得到的结果为‘N’,这里的 instanceof 测试的 object 是指 js 语法中的 object，不是指 dom 模型对象。

if (window instanceof Object) {
  alert("Y");
} else {
  alert("N");
} // 'N'
```

### 如何理解闭包？

1、定义和用法：当一个函数的返回值是另外一个函数，而返回的那个函数如果调用了其父函数内部的其它变量，如果返回的这个函数在外部被执行，就产生了闭包。

2、表现形式：使函数外部能够调用函数内部定义的变量。

3、实例如下：

(1)、根据作用域链的规则，底层作用域没有声明的变量，会向上一级找，找到就返回，没找到就一直找，直到 window 的变量，没有就返回 undefined。这里明显 count 是函数内部的 flag2 的那个 count 。

```js
var count = 10; //全局作用域 标记为flag1
function add() {
  var count = 0; //函数全局作用域 标记为flag2
  return function() {
    count += 1; //函数的内部作用域
    alert(count);
  };
}
var s = add();
s(); //输出1
s(); //输出2
```

4、变量的作用域

要理解闭包，首先必须理解 Javascript 特殊的变量作用域。

变量的作用域分类：全局变量和局部变量。

特点：

1、函数内部可以读取函数外部的全局变量；在函数外部无法读取函数内的局部变量。

2、函数内部声明变量的时候，一定要使用 var 命令。如果不用的话，你实际上声明了一个全局变量！

5、使用闭包的注意点

1）滥用闭包，会造成内存泄漏：由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在 IE 中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。

2）会改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

### 什么是跨域？跨域请求资源的方法有哪些？

#### 1、什么是跨域？

由于浏览器同源策略，凡是发送请求 url 的协议、域名、端口三者之间任意一与当前页面地址不同即为跨域。存在跨域的情况：

网络协议不同，如 http 协议访问 https 协议。

端口不同，如 80 端口访问 8080 端口。

域名不同，如 qianduanblog.com 访问 baidu.com。

子域名不同，如 abc.qianduanblog.com 访问 def.qianduanblog.com。

域名和域名对应 ip,如 www.a.com 访问 20.205.28.90.

#### 2、跨域请求资源的方法：

https://ryanipo.github.io/2019/03/15/Cross-domain.html

### 谈谈垃圾回收机制方式及内存管理

#### 回收机制方式

1、定义和用法：垃圾回收机制(GC:Garbage Collection),执行环境负责管理代码执行过程中使用的内存。

2、原理：垃圾收集器会定期（周期性）找出那些不在继续使用的变量，然后释放其内存。但是这个过程不是实时的，因为其开销比较大，所以垃圾回收器会按照固定的时间间隔周期性的执行。

3、实例如下：

```js
function fn1() {
  var obj = { name: "hanzichi", age: 10 };
}
function fn2() {
  var obj = { name: "hanzichi", age: 10 };
  return obj;
}
var a = fn1();
var b = fn2();

// fn1中定义的obj为局部变量，而当调用结束后，出了fn1的环境，那么该块内存会被js引擎中的垃圾回收器自动释放；在fn2被调用的过程中，返回的对象被全局变量b所指向，所以该块内存并不会被释放。
```

4、垃圾回收策略：标记清除(较为常用)和引用计数。
标记清除：

定义和用法：当变量进入环境时，将变量标记"进入环境"，当变量离开环境时，标记为："离开环境"。某一个时刻，垃圾回收器会过滤掉环境中的变量，以及被环境变量引用的变量，剩下的就是被视为准备回收的变量。

到目前为止，IE、Firefox、Opera、Chrome、Safari 的 js 实现使用的都是标记清除的垃圾回收策略或类似的策略，只不过垃圾收集的时间间隔互不相同。

引用计数：

定义和用法：引用计数是跟踪记录每个值被引用的次数。

基本原理：就是变量的引用次数，被引用一次则加 1，当这个引用计数为 0 时，被视为准备回收的对象。

内存管理

1、什么时候触发垃圾回收？

垃圾回收器周期性运行，如果分配的内存非常多，那么回收工作也会很艰巨，确定垃圾回收时间间隔就变成了一个值得思考的问题。

IE6 的垃圾回收是根据内存分配量运行的，当环境中的变量，对象，字符串达到一定数量时触发垃圾回收。垃圾回收器一直处于工作状态，严重影响浏览器性能。

IE7 中，垃圾回收器会根据内存分配量与程序占用内存的比例进行动态调整，开始回收工作。

2、合理的 GC 方案：(1)、遍历所有可访问的对象; (2)、回收已不可访问的对象。

3、GC 缺陷：(1)、停止响应其他操作；

4、GC 优化策略：(1)、分代回收（Generation GC）;(2)、增量 GC

### 开发过程中遇到的内存泄露情况，如何解决的？

#### 1、定义和用法：

内存泄露是指一块被分配的内存既不能使用，又不能回收，直到浏览器进程结束。C#和 Java 等语言采用了自动垃圾回收方法管理内存，几乎不会发生内存泄露。我们知道，浏览器中也是采用自动垃圾回收方法管理内存，但由于浏览器垃圾回收方法有 bug，会产生内存泄露。

#### 2、内存泄露的几种情况:

(1)、当页面中元素被移除或替换时，若元素绑定的事件仍没被移除，在 IE 中不会作出恰当处理，此时要先手工移除事件，不然会存在内存泄露。

实例如下:

```html
<div id="myDiv">
  <input type="button" value="Click me" id="myBtn" />
</div>
<script type="text/javascript">
  var btn = document.getElementById("myBtn");
  btn.onclick = function() {
    document.getElementById("myDiv").innerHTML = "Processing...";
  };
</script>
```

解决方法如下：

```html
<div id="myDiv">
  <input type="button" value="Click me" id="myBtn" />
</div>
<script type="text/javascript">
  var btn = document.getElementById("myBtn");
  btn.onclick = function() {
    btn.onclick = null;
    document.getElementById("myDiv").innerHTML = "Processing...";
  };
</script>
```

(2)、由于是函数内定义函数，并且内部函数--事件回调的引用外暴了，形成了闭包。闭包可以维持函数内局部变量，使其得不到释放。
实例如下：

```js
function bindEvent() {
  var obj = document.createElement("XXX");
  obj.onclick = function() {
    //Even if it's a empty function
  };
}
```

解决方法如下：

```js
function bindEvent() {
  var obj = document.createElement("XXX");
  obj.onclick = function() {
    //Even if it's a empty function
  };
  obj = null;
}
```

### javascript 面向对象中继承实现？

面向对象的基本特征有：封闭、继承、多态。

在 JavaScript 中实现继承的方法：

1. 原型链（prototype chaining）

2. call()/apply()

3. 混合方式(prototype 和 call()/apply()结合)

4. 对象冒充

继承的方法如下：

1、prototype 原型链方式：

```js
function teacher(name) {
  this.name = name;
}
teacher.prototype.sayName = function() {
  console.log("name is " + this.name);
};
var teacher1 = new teacher("xiaoming");
teacher1.sayName();

function student(name) {
  this.name = name;
}
student.prototype = new teacher();
var student1 = new student("xiaolan");
student1.sayName();
//  name is xiaoming
//  name is xiaolan
```

2、call()/apply()方法

```js
function teacher(name, age) {
  this.name = name;
  this.age = age;
  this.sayhi = function() {
    alert("name:" + name + ", age:" + age);
  };
}
function student() {
  var args = arguments;
  teacher.call(this, args[0], args[1]);
  // teacher.apply(this,arguments);
}
var teacher1 = new teacher("xiaoming", 23);
teacher1.sayhi();

var student1 = new student("xiaolan", 12);
student1.sayhi();

// alert: name:xiaoming, age:23
// alert: name:xiaolan, age:12
```

3、混合方法【prototype,call/apply】

```js
function teacher(name, age) {
  this.name = name;
  this.age = age;
}
teacher.prototype.sayName = function() {
  console.log("name:" + this.name);
};
teacher.prototype.sayAge = function() {
  console.log("age:" + this.age);
};

function student() {
  var args = arguments;
  teacher.call(this, args[0], args[1]);
}
student.prototype = new teacher();

var student1 = new student("xiaolin", 23);
student1.sayName();
student1.sayAge();
// name:xiaolin
// age:23
```

4、对象冒充

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.show = function() {
    console.log(this.name + ", " + this.age);
  };
}

function Student(name, age) {
  this.student = Person; //将Person类的构造函数赋值给this.student
  this.student(name, age); //js中实际上是通过对象冒充来实现继承的
  delete this.student; //移除对Person的引用
}

var s = new Student("小明", 17);
s.show();

var p = new Person("小花", 18);
p.show();
// 小明, 17
// 小花, 18
```

### 1、Array 相关的属性和方法

Array 对象属性
constructor 返回对创建此对象的数组函数的引用。

length 设置或返回数组中元素的数目。

prototype 使您有能力向对象添加属性和方法。

Array 对象方法
concat() 连接两个或更多的数组，并返回结果。

join() 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。

pop() 删除并返回数组的最后一个元素。

shift() 删除并返回数组的第一个元素

push() 向数组的末尾添加一个或更多元素，并返回新的长度。

unshift() 向数组的开头添加一个或更多元素，并返回新的长度。

reverse() 颠倒数组中元素的顺序。

slice() 从某个已有的数组返回选定的元素

sort() 对数组的元素进行排序

splice() 删除元素，并向数组添加新元素。

toSource() 返回该对象的源代码。

toString() 把数组转换为字符串，并返回结果。

toLocaleString() 把数组转换为本地数组，并返回结果。

valueOf() 返回数组对象的原始值

### 2、编写一个方法 去掉一个数组的重复元素

#### 方法一：

```js
var arr = [0, 2, 3, 4, 4, 0, 2];
var obj = {};
var tmp = [];
for (var i = 0; i < arr.length; i++) {
  if (!obj[arr[i]]) {
    obj[arr[i]] = 1;
    tmp.push(arr[i]);
  }
}
console.log(tmp); // [0, 2, 3, 4]
```

#### 方法二：

```js
var arr = [2, 3, 4, 4, 5, 2, 3, 6];
var arr2 = [];
for (var i = 0; i < arr.length; i++) {
  if (arr2.indexOf(arr[i]) < 0) {
    arr2.push(arr[i]);
  }
}
console.log(arr2); //[2, 3, 4, 5, 6]
```

#### 方法三：

```js
var arr = [2, 3, 4, 4, 5, 2, 3, 6];
var arr2 = arr.filter(function(element, index, self) {
  return self.indexOf(element) === index;
});
console.log(arr2); //[2, 3, 4, 5, 6]
```

## jquery 相关

### 1、 jQuery 库中的 \$() 是什么？

$() 函数是 jQuery() 函数的别称。$() 函数用于将任何对象包裹成 jQuery 对象，接着你就被允许调用定义在 jQuery 对象上的多个不同方法。你可以将一个选择器字符串传入 \$() 函数，它会返回一个包含所有匹配的 DOM 元素数组的 jQuery 对象。

### 2、如何找到所有 HTML select 标签的选中项？

`$('[name=selectname] :selected')`

### 3、\$(this) 和 this 关键字在 jQuery 中有何不同？

\$(this) 返回一个 jQuery 对象，你可以对它调用多个 jQuery 方法，比如用 text() 获取文本，用 val() 获取值等等。

而 this 代表当前元素，它是 JavaScript 关键词中的一个，表示上下文中的当前 DOM 元素。你不能对它调用 jQuery 方法，直到它被 $() 函数包裹，例如 $(this)。

### 4、jquery 怎么移除标签 onclick 属性？

获得 a 标签的 onclick 属性: \$("a").attr("onclick")

删除 onclick 属性：\$("a").removeAttr("onclick");

设置 onclick 属性：\$("a").attr("onclick","test();");

### 5、jquery 中 addClass,removeClass,toggleClass 的使用。

\$(selector).addClass(class)：为每个匹配的元素添加指定的类名

\$(selector).removeClass(class)：从所有匹配的元素中删除全部或者指定的类，删除 class 中某个值；

\$(selector).toggleClass(class)：如果存在（不存在）就删除（添加）一个类

\$(selector).removeAttr(class);删除 class 这个属性；

### 6、JQuery 有几种选择器?

(1)、基本选择器：#id，class,element,\*;

(2)、层次选择器：parent > child，prev + next ，prev ~ siblings

(3)、基本过滤器选择器：:first，:last ，:not ，:even ，:odd ，:eq ，:gt ，:lt

(4)、内容过滤器选择器： :contains ，:empty ，:has ，:parent

(5)、可见性过滤器选择器：:hidden ，:visible

(6)、属性过滤器选择器：[attribute] ，[attribute=value] ，[attribute!=value] ，[attribute^=value] ，[attribute$=value] ，[attribute*=value]

(7)、子元素过滤器选择器：:nth-child ，:first-child ，:last-child ，:only-child

(8)、表单选择器： :input ，:text ，:password ，:radio ，:checkbox ，:submit 等；

(9)、表单过滤器选择器：:enabled ，:disabled ，:checked ，:selected

### 7、jQuery 中的 Delegate()函数有什么作用？

delegate()会在以下两个情况下使用到：

1、如果你有一个父元素，需要给其下的子元素添加事件，这时你可以使用 delegate()了，代码如下：

```js
$("ul").delegate("li", "click", function() {
  $(this).hide();
});
```

2、当元素在当前页面中不可用时，可以使用 delegate()

### 8、\$(document).ready()方法和 window.onload 有什么区别？

(1)、window.onload 方法是在网页中所有的元素(包括元素的所有关联文件)完全加载到浏览器后才执行的。

(2)、\$(document).ready() 方法可以在 DOM 载入就绪时就对其进行操纵，并调用执行绑定的函数。

### 9、如何用 jQuery 禁用浏览器的前进后退按钮？

实现代码如下：

```html
<script type="text/javascript" language="javascript">
  $(document).ready(function() {
    window.history.forward(1); //OR window.history.forward(-1);
  });
</script>
```

### 10、 jquery 中$.get()提交和$.post()提交有区别吗？

相同点：都是异步请求的方式来获取服务端的数据；
异同点：

1、请求方式不同：$.get() 方法使用GET方法来进行异步请求的。$.post()  方法使用 POST 方法来进行异步请求的。

2、参数传递方式不同：get 请求会将参数跟在 URL 后进行传递，而 POST 请求则是作为 HTTP 消息的实体内容发送给 Web 服务器的，这种传递是对用户不可见的。

3、数据传输大小不同：get 方式传输的数据大小不能超过 2KB  而 POST 要大的多

4、安全问题： GET  方式请求的数据会被浏览器缓存起来，因此有安全问题。

### 11、写出一个简单的\$.ajax()的请求方式？

```js
$.ajax({
    url:'http://www.baidu.com',
    type:'POST',
    data:data,
    cache:true,
    headers:{},
    beforeSend：function(){},
    success:function(){},
    error:function(){},
    complete:function(){}
});
```

### 12、jQuery 的事件委托方法 bind 、live、delegate、on 之间有什么区别？

1、bind 【jQuery 1.3 之前】
定义和用法：主要用于给选择到的元素上绑定特定事件类型的监听函数；

语法：bind(type,[data],function(eventObject))；

特点：

(1)、适用于页面元素静态绑定。只能给调用它的时候已经存在的元素绑定事件，不能给未来新增的元素绑定事件。

(2)、当页面加载完的时候，你才可以进行 bind()，所以可能产生效率问题。

实例如下：\$( "#members li a" ).bind( "click", function( e ) {} );

2、live 【jQuery 1.3 之后】
定义和用法：主要用于给选择到的元素上绑定特定事件类型的监听函数；

语法：live(type, [data], fn);

特点：

(1)、live 方法并没有将监听器绑定到自己(this)身上，而是绑定到了 this.context 上了。

(2)、live 正是利用了事件委托机制来完成事件的监听处理，把节点的处理委托给了 document，新添加的元素不必再绑定一次监听器。

(3)、使用 live（）方法但却只能放在直接选择的元素后面，不能在层级比较深，连缀的 DOM 遍历方法后面使用，即$(“ul”").live...可以，但$("body").find("ul").live...不行；

实例如下：\$( document ).on( "click", "#members li a", function( e ) {} );

3、delegate 【jQuery 1.4.2 中引入】
定义和用法：将监听事件绑定在就近的父级元素上

语法：delegate(selector,type,[data],fn)

特点：

(1)、选择就近的父级元素，因为事件可以更快的冒泡上去，能够在第一时间进行处理。

(2)、更精确的小范围使用事件代理，性能优于.live()。可以用在动态添加的元素上。

实例如下：

\$("#info*table").delegate("td","click",function(){/*显示更多信息\_/});

\$("table").find("#info").delegate("td","click",function(){/_显示更多信息_/});

4、on 【1.7 版本整合了之前的三种方式的新事件绑定机制】
定义和用法：将监听事件绑定到指定元素上。

语法：on(type,[selector],[data],fn)

实例如下：\$("#info*table").on("click","td",function(){/*显示更多信息\_/});参数的位置写法与 delegate 不一样。

说明：on 方法是当前 JQuery 推荐使用的事件绑定方法，附加只运行一次就删除函数的方法是 one()。

总结：.bind(), .live(), .delegate(),.on()分别对应的相反事件为：.unbind(),.die(), .undelegate(),.off()

## HTML & CSS:

### 1、什么是盒子模型？

在网页中，一个元素占有空间的大小由几个部分构成，其中包括元素的内容（content），元素的内边距（padding），元素的边框（border），元素的外边距（margin）四个部分。这四个部分占有的空间中，有的部分可以显示相应的内容，而有的部分只用来分隔相邻的区域或区域。4 个部分一起构成了 css 中元素的盒模型。

### 2、行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？

行内元素：a、b、span、img、input、strong、select、label、em、button、textarea
块级元素：div、ul、li、dl、dt、dd、p、h1-h6、blockquote
空元素：即系没有内容的 HTML 元素，例如：br、meta、hr、link、input、img

### 3、CSS 实现垂直水平居中

一道经典的问题，实现方法有很多种，以下是其中一种实现：

```html
<!-- HTML结构： -->
<div class="wrapper">
  <div class="content"></div>
</div>

<!-- CSS -->
<style>
  .wrapper {
    position: relative;
    width: 500px;
    height: 500px;
    border: 1px solid red;
  }
  .content {
    position: absolute;
    width: 200px;
    height: 200px;
    /*top、bottom、left和right 均设置为0*/
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    /*margin设置为auto*/
    margin: auto;
    border: 1px solid green;
  }
</style>
```

### 4、简述一下 src 与 href 的区别

href 是指向网络资源所在位置，建立和当前元素（锚点）或当前文档（链接）之间的链接，用于超链接。

src 是指向外部资源的位置，指向的内容将会嵌入到文档中当前标签所在位置；在请求 src 资源时会将其指向的资源下载并应用到文档内，例如 js 脚本，img 图片和 frame 等元素。

当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，图片和框架等元素也如此，类似于将所指向资源嵌入当前标签内。这也是为什么将 js 脚本放在底部而不是头部。

### 5、简述同步和异步的区别

同步是阻塞模式，异步是非阻塞模式。
同步就是指一个进程在执行某个请求的时候，若该请求需要一段时间才能返回信息，那么这个进程将会一直等待下去，直到收到返回信息才继续执行下去；
异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时系统会通知进程进行处理，这样可以提高执行的效率。

### 6、px 和 em 的区别

相同点：px 和 em 都是长度单位；

异同点：px 的值是固定的，指定是多少就是多少，计算比较容易。em 得值不是固定的，并且 em 会继承父级元素的字体大小。
浏览器的默认字体高都是 16px。所以未经调整的浏览器都符合: 1em=16px。那么 12px=0.75em, 10px=0.625em。

### 7、浏览器的内核分别是什么?

IE: trident 内核
Firefox：gecko 内核
Safari：webkit 内核
Opera：以前是 presto 内核，Opera 现已改用 Google Chrome 的 Blink 内核
Chrome：Blink(基于 webkit，Google 与 Opera Software 共同开发)

### 8、什么叫优雅降级和渐进增强？

渐进增强 progressive enhancement：
针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。

优雅降级 graceful degradation：
一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。

区别：

a. 优雅降级是从复杂的现状开始，并试图减少用户体验的供给

b. 渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要

c. 降级（功能衰减）意味着往回看；而渐进增强则意味着朝前看，同时保证其根基处于安全地带

### 9、sessionStorage 、localStorage 和  cookie 之间的区别

共同点：用于浏览器端存储的缓存数据

不同点：

(1)、存储内容是否发送到服务器端：当设置了 Cookie 后，数据会发送到服务器端，造成一定的宽带浪费；

web storage,会将数据保存到本地，不会造成宽带浪费；

(2)、数据存储大小不同：Cookie 数据不能超过 4K,适用于会话标识；web storage 数据存储可以达到 5M;

(3)、数据存储的有效期限不同：cookie 只在设置了 Cookid 过期时间之前一直有效，即使关闭窗口或者浏览器；

sessionStorage,仅在关闭浏览器之前有效；localStorage,数据存储永久有效；

(4)、作用域不同：cookie 和 localStorage 是在同源同窗口中都是共享的；sessionStorage 不在不同的浏览器窗口中共享，即使是同一个页面；

### 10、Web Storage 与 Cookie 相比存在的优势：

1)、存储空间更大：IE8 下每个独立的存储空间为 10M，其他浏览器实现略有不同，但都比 Cookie 要大很多。

(2)、存储内容不会发送到服务器：当设置了 Cookie 后，Cookie 的内容会随着请求一并发送的服务器，这对于本地存储的数据是一种带宽浪费。而 Web Storage 中的数据则仅仅是存在本地，不会与服务器发生任何交互。

(3)、更多丰富易用的接口：Web Storage 提供了一套更为丰富的接口，如 setItem,getItem,removeItem,clear 等,使得数据操作更为简便。cookie 需要自己封装。

(4)、独立的存储空间：每个域（包括子域）有独立的存储空间，各个存储空间是完全独立的，因此不会造成数据混乱。

### 11、Ajax 的优缺点及工作原理？

#### 定义和用法:

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。Ajax 是一种用于创建快速动态网页的技术。Ajax 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。

传统的网页（不使用 Ajax）如果需要更新内容，必须重载整个网页页面。

#### 优点：

1.减轻服务器的负担,按需取数据,最大程度的减少冗余请求

2.局部刷新页面,减少用户心理和实际的等待时间,带来更好的用户体验

3.基于 xml 标准化,并被广泛支持,不需安装插件等,进一步促进页面和数据的分离

#### 缺点：

1.AJAX 大量的使用了 javascript 和 ajax 引擎,这些取决于浏览器的支持.在编写的时候考虑对浏览器的兼容性.

2.AJAX 只是局部刷新,所以页面的后退按钮是没有用的.

3.对流媒体还有移动设备的支持不是太好等

#### AJAX 的工作原理：

1.创建 ajax 对象（XMLHttpRequest/ActiveXObject(Microsoft.XMLHttp)）

2.判断数据传输方式(GET/POST)

3.打开链接 open()

4.发送 send()

5.当 ajax 对象完成第四步（onreadystatechange）数据接收完成，判断 http 响应状态（status）200-300 之间或者 304（缓存）执行回调函数

### 12、请指出 document load 和 document ready 的区别？

共同点：这两种事件都代表的是页面文档加载时触发。

异同点：

ready 事件的触发，表示文档结构已经加载完成（不包含图片等非文字媒体文件）。

onload 事件的触发，表示页面包含图片等文件在内的所有元素都加载完成。

## 正则表达式

### 1、写一个 function，清除字符串前后的空格。（兼容所有浏览器）

```js
function trim(str) {
  if (str && typeof str === "string") {
    return str.replace(/(^\s*)|(\s*)$/g, ""); //去除前后空白符
  }
}
```

### 2、使用正则表达式验证邮箱格式

```js
var reg = /^(\w)+(\.\w+)*@(\w)+((\.\w{2,3}){1,3})$/;
var email = "example@qq.com";
console.log(reg.test(email)); // true
```

## 开发及性能优化

### 1、规避 javascript 多人开发函数重名问题

命名空间
封闭空间
js 模块化 mvc（数据层、表现层、控制层）
seajs
变量转换成对象的属性
对象化

### 2、请说出三种减低页面加载时间的方法

压缩 css、js 文件
合并 js、css 文件，减少 http 请求
外部 js、css 文件放在最底下
减少 dom 操作，尽可能用变量替代不必要的 dom 操作

### 3、你所了解到的 Web 攻击技术

（1）XSS（Cross-Site Scripting，跨站脚本攻击）：指通过存在安全漏洞的 Web 网站注册用户的浏览器内运行非法的 HTML 标签或者 JavaScript 进行的一种攻击。
（2）SQL 注入攻击
（3）CSRF（Cross-Site Request Forgeries，跨站点请求伪造）：指攻击者通过设置好的陷阱，强制对已完成的认证用户进行非预期的个人信息或设定信息等某些状态更新。

### 4、web 前端开发，如何提高页面性能优化？

内容方面：

1. 减少 HTTP 请求 (Make Fewer HTTP Requests)

2. 减少 DOM 元素数量 (Reduce the Number of DOM Elements)

3. 使得 Ajax 可缓存 (Make Ajax Cacheable)

针对 CSS：

1. 把 CSS 放到代码页上端 (Put Stylesheets at the Top)

2. 从页面中剥离 JavaScript 与 CSS (Make JavaScript and CSS External)

3. 精简 JavaScript 与 CSS (Minify JavaScript and CSS)

4. 避免 CSS 表达式 (Avoid CSS Expressions)

针对 JavaScript ：

1. 脚本放到 HTML 代码页底部 (Put Scripts at the Bottom)

2. 从页面中剥离 JavaScript 与 CSS (Make JavaScript and CSS External)

3. 精简 JavaScript 与 CSS (Minify JavaScript and CSS)

4. 移除重复脚本 (Remove Duplicate Scripts)

面向图片(Image)：

1. 优化图片

2. 不要在 HTML 中使用缩放图片

3. 使用恰当的图片格式

4. 使用 CSS Sprites 技巧对图片优化

### 5、前端开发中，如何优化图像？图像格式的区别？

优化图像：
1、不用图片，尽量用 css3 代替。 比如说要实现修饰效果，如半透明、边框、圆角、阴影、渐变等，在当前主流浏览器中都可以用 CSS 达成。

2、 使用矢量图 SVG 替代位图。对于绝大多数图案、图标等，矢量图更小，且可缩放而无需生成多套图。现在主流浏览器都支持 SVG 了，所以可放心使用！

3、使用恰当的图片格式。我们常见的图片格式有 JPEG、GIF、PNG。

基本上，内容图片多为照片之类的，适用于 JPEG。

而修饰图片通常更适合用无损压缩的 PNG。

GIF 基本上除了 GIF 动画外不要使用。且动画的话，也更建议用 video 元素和视频格式，或用 SVG 动画取代。

4、按照 HTTP 协议设置合理的缓存。

5、使用字体图标 webfont、CSS Sprites 等。

6、用 CSS 或 JavaScript 实现预加载。

7、WebP 图片格式能给前端带来的优化。WebP 支持无损、有损压缩，动态、静态图片，压缩比率优于 GIF、JPEG、JPEG2000、PG 等格式，非常适合用于网络等图片传输。

图像格式的区别：
矢量图：图标字体，如 font-awesome；svg

位图：gif,jpg(jpeg),png

区别：

1、gif:是是一种无损，8 位图片格式。具有支持动画，索引透明，压缩等特性。适用于做色彩简单(色调少)的图片，如 logo,各种小图标 icons 等。

2、JPEG 格式是一种大小与质量相平衡的压缩图片格式。适用于允许轻微失真的色彩丰富的照片，不适合做色彩简单(色调少)的图片，如 logo,各种小图标 icons 等。

3、png:PNG 可以细分为三种格式:PNG8，PNG24，PNG32。后面的数字代表这种 PNG 格式最多可以索引和存储的颜色值。

关于透明：PNG8 支持索引透明和 alpha 透明;PNG24 不支持透明;而 PNG32 在 24 位的 PNG 基础上增加了 8 位（256 阶）的 alpha 通道透明;

优缺点：

1、能在保证最不失真的情况下尽可能压缩图像文件的大小。

2、对于需要高保真的较复杂的图像，PNG 虽然能无损压缩，但图片文件较大，不适合应用在 Web 页面上。

### 6、浏览器是如何渲染页面的？

渲染的流程如下：

1.解析 HTML 文件，创建 DOM 树。

自上而下，遇到任何样式（link、style）与脚本（script）都会阻塞（外部样式不阻塞后续外部脚本的加载）。

2.解析 CSS。优先级：浏览器默认设置<用户设置<外部样式<内联样式<HTML 中的 style 样式；

3.将 CSS 与 DOM 合并，构建渲染树（Render Tree）

4.布局和绘制，重绘（repaint）和重排（reflow）

## vue

### 1. 谈谈你对 MVVM 开发模式的理解

MVVM 分为 Model、View、ViewModel 三者。
Model 代表数据模型，数据和业务逻辑都在 Model 层中定义；
View 代表 UI 视图，负责数据的展示；
ViewModel 负责监听 Model 中数据的改变并且控制视图的更新，处理用户交互操作；
Model 和 View 并无直接关联，而是通过 ViewModel 来进行联系的，Model 和 ViewModel 之间有着双向数据绑定的联系。因此当 Model 中的数据改变时会触发 View 层的刷新，View 中由于用户交互操作而改变的数据也会在 Model 中同步。
这种模式实现了 Model 和 View 的数据自动同步，因此开发者只需要专注对数据的维护操作即可，而不需要自己操作 dom。

### 2. Vue 有哪些指令？

v-on、v-html、v-show、v-if、v-for 等等

### 3. v-if 和 v-show 有什么区别？

v-show 仅仅控制元素的显示方式，将 display 属性在 block 和 none 来回切换；而 v-if 会控制这个 DOM 节点的存在与否。当我们需要经常切换某个元素的显示/隐藏时，使用 v-show 会更加节省性能上的开销；当只需要一次显示或隐藏时，使用 v-if 更加合理。

### 4. 简述 Vue 的响应式原理

当一个 Vue 实例创建时，vue 会遍历 data 选项的属性，用 Object.defineProperty 将它们转为 getter/setter 并且在内部追踪相关依赖，在属性被访问和修改时通知变化。
每个组件实例都有相应的 watcher 程序实例，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的 setter 被调用时，会通知 watcher 重新计算，从而致使它关联的组件得以更新。

![](https://ws1.sinaimg.cn/large/a5caea9fgy1g2yl5nc9v1j20xc0kuabw.jpg)

### 5. Vue 中如何在组件内部实现一个双向数据绑定？

### 6. Vue 中如何监控某个属性值的变化？

比如现在需要监控 data 中，obj.a 的变化。Vue 中监控对象属性的变化你可以这样：

```js
watch: {
      obj: {
      handler (newValue, oldValue) {
        console.log('obj changed')
      },
      deep: true
    }
  }
```

deep 属性表示深层遍历，但是这么写会监控 obj 的所有属性变化，并不是我们想要的效果，所以做点修改：

```js
watch: {
   'obj.a': {
      handler (newName, oldName) {
        console.log('obj.a changed')
      }
   }
  }
```

还有一种方法，可以通过 computed 来实现，只需要：

```js
computed: {
    a1 () {
      return this.obj.a
    }
}
```

利用计算属性的特性来实现，当依赖改变时，便会重新计算一个新值。

### 7. Vue 中给 data 中的对象属性添加一个新的属性时会发生什么，如何解决？

示例：

```html
<template>
  <div>
    <ul>
      <li v-for="value in obj" :key="value">
        {{ value }}
      </li>
    </ul>
    <button @click="addObjB">添加obj.b</button>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        obj: {
          a: "obj.a"
        }
      };
    },
    methods: {
      addObjB() {
        this.obj.b = "obj.b";
        console.log(this.obj);
      }
    }
  };
</script>

<style></style>
```

点击 button 会发现，obj.b 已经成功添加，但是视图并未刷新：

![](https://ws1.sinaimg.cn/large/a5caea9fgy1g2ylb6m1rsj20es02r3yf.jpg)

![](https://ws1.sinaimg.cn/large/a5caea9fgy1g2ylbebw6fj209o03bt8i.jpg)

原因在于在 Vue 实例创建时，obj.b 并未声明，因此就没有被 Vue 转换为响应式的属性，自然就不会触发视图的更新，这时就需要使用 Vue 的全局 api \$set()：

```js
addObjB () {
      // this.obj.b = 'obj.b'
      this.$set(this.obj, 'b', 'obj.b')
      console.log(this.obj)
    }
```

\$set()方法相当于手动的去把 obj.b 处理成一个响应式的属性，此时视图也会跟着改变了：

![](https://ws1.sinaimg.cn/large/a5caea9fgy1g2ylc34kidj209k049web.jpg)

### 8. delete 和 Vue.delete 删除数组的区别

delete 只是被删除的元素变成了 empty/undefined 其他的元素的键值还是不变。
Vue.delete 直接删除了数组 改变了数组的键值。

```js
var a = [1, 2, 3, 4];
var b = [1, 2, 3, 4];
delete a[1];
console.log(a);
this.$delete(b, 1);
console.log(b);
```

![](https://ws1.sinaimg.cn/large/a5caea9fgy1g2ylcwiib5j20da04djra.jpg)
![](https://ws1.sinaimg.cn/large/a5caea9fgy1g2yld0tkkvj20i704ijrb.jpg)

### 9.如何优化 SPA 应用的首屏加载速度慢的问题？

将公用的 JS 库通过 script 标签外部引入，减小 app.bundel 的大小，让浏览器并行下载资源文件，提高下载速度；

在配置 路由时，页面和组件使用懒加载的方式引入，进一步缩小 app.bundel 的体积，在调用某个组件时再加载对应的 js 文件；

加一个首屏 loading 图，提升用户体验；

### 10. 前端如何优化网站性能？

#### 减少 HTTP 请求数量

在浏览器与服务器进行通信时，主要是通过 HTTP 进行通信。浏览器与服务器需要经过三次握手，每次握手需要花费大量时间。而且不同浏览器对资源文件并发请求数量有限（不同浏览器允许并发数），一旦 HTTP 请求数量达到一定数量，资源请求就存在等待状态，这是很致命的，因此减少 HTTP 的请求数量可以很大程度上对网站性能进行优化。

CSS Sprites：国内俗称 CSS 精灵，这是将多张图片合并成一张图片达到减少 HTTP 请求的一种解决方案，可以通过 CSS background 属性来访问图片内容。这种方案同时还可以减少图片总字节数。

合并 CSS 和 JS 文件：现在前端有很多工程化打包工具，如：grunt、gulp、webpack 等。为了减少 HTTP 请求数量，可以通过这些工具再发布前将多个 CSS 或者 多个 JS 合并成一个文件。

采用 lazyLoad：俗称懒加载，可以控制网页上的内容在一开始无需加载，不需要发请求，等到用户操作真正需要的时候立即加载出内容。这样就控制了网页资源一次性请求数量。

#### 控制资源文件加载优先级

浏览器在加载 HTML 内容时，是将 HTML 内容从上至下依次解析，解析到 link 或者 script 标签就会加载 href 或者 src 对应链接内容，为了第一时间展示页面给用户，就需要将 CSS 提前加载，不要受 JS 加载影响。
一般情况下都是 CSS 在头部，JS 在底部。

利用浏览器缓存
浏览器缓存是将网络资源存储在本地，等待下次请求该资源时，如果资源已经存在就不需要到服务器重新请求该资源，直接在本地读取该资源。

减少重排（Reflow）
基本原理：重排是 DOM 的变化影响到了元素的几何属性（宽和高），浏览器会重新计算元素的几何属性，会使渲染树中受到影响的部分失效，浏览器会验证 DOM 树上的所有其它结点的 visibility 属性，这也是 Reflow 低效的原因。如果 Reflow 的过于频繁，CPU 使用率就会急剧上升。

减少 Reflow，如果需要在 DOM 操作时添加样式，尽量使用 增加 class 属性，而不是通过 style 操作样式。

减少 DOM 操作

图标使用 IconFont 替换

### 11. 网页从输入网址到渲染完成经历了哪些过程？

大致可以分为如下 7 步：

输入网址；
发送到 DNS 服务器，并获取域名对应的 web 服务器对应的 ip 地址；
与 web 服务器建立 TCP 连接；
浏览器向 web 服务器发送 http 请求；
web 服务器响应请求，并返回指定 url 的数据（或错误信息，或重定向的新的 url 地址）；
浏览器下载 web 服务器返回的数据及解析 html 源文件；
生成 DOM 树，解析 css 和 js，渲染页面，直至显示完成；

### 12. jQuery 获取的 dom 对象和原生的 dom 对象有何区别？

js 原生获取的 dom 是一个对象，jQuery 对象就是一个类数组对象，其实就是选择出来的元素的数组集合，所以说他们两者是不同的对象类型不等价。

原生 DOM 对象转 jQuery 对象：

```js
var box = document.getElementById("box");
var $box = $(box);
```

jQuery 对象转原生 DOM 对象：

```js
var $box = $("#box");
var box = $box[0];
```

### 13. jQuery 如何扩展自定义方法

```js
(jQuery.fn.myMethod = function() {
  alert("myMethod");
})(
  // 或者：
  function($) {
    $.fn.extend({
      myMethod: function() {
        alert("myMethod");
      }
    });
  }
)(jQuery);
```

使用：

```js
$("#div").myMethod();
```

## 更多

1. [Vue 面试中，经常会被问到的面试题/Vue 知识点整理](https://segmentfault.com/a/1190000016344599)

2. [98 道经典 Vue 面试题总结（长期更新）](https://segmentfault.com/a/1190000016351284)

3. [务必熟知的 vuejs 面试题](https://blog.csdn.net/liangjielaoshi/article/details/84064095)

4. [Web 前端初级面试题总结](https://blog.csdn.net/qq_39252501/article/details/79754499)

5. [互联网公司前端初级 Javascript 面试题](https://www.cnblogs.com/zdz8207/p/JavaScript-simaple-view.html)

6. [最全前端面试问题及答案总结](https://www.cnblogs.com/autismtune/p/5210116.html)

7. [web 前端面试 100 题](https://blog.csdn.net/lvyang251314/article/details/80688651)

8. [2019 年最新经典 web 前端面试题](https://www.jianshu.com/p/eb0f269098d5)

9. [前端面试题整理](https://www.cnblogs.com/haoyijing/p/5789348.html)

10. [前端面试题](https://github.com/woai3c/Front-end-basic-knowledge)

11. [常见 Web 前端开发笔试题](https://www.cnblogs.com/shenxiaolin/p/5387775.html)

12. [前端开发面试题](https://github.com/markyun/My-blog/tree/master/Front-end-Developer-Questions/Questions-and-Answers)

## 其他

[写给初级前端的面试经验](https://zhuanlan.zhihu.com/p/59650410)

[JavaScript 开发者应懂的 33 个概念](https://zhuanlan.zhihu.com/p/48049957)

[Vue+Webpack打造todo应用](https://www.imooc.com/learn/935)