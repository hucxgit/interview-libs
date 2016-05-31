## vocinno前端面试题

### css 部分

* 1 常用哪些display属性

```
答出inline-block inline block none等为满足普通前端工程师的标准，否则为不满足。
另答出table table-cell flex grid index-flex等属性者可认为满足高级前端工程师的标准
```

* 2 写出最后class是a的DOM节点直接子节点中最后一个子节点的选择器

```
.a:nth-last-child(1)
```

* 3 textarea标签如何禁止调整大小

```
resize:none;
```

* 5 简单介绍下css样式渲染时的顺序规则

```
能讲出前后左右、Id、class、tag和内联之间顺序关系的算满足普通前端工程师的标准，否则为不满足。
能讲出选择器级联，并联，media选择器，!important等算满足高级前端工程师的标准。
```

* 6 简要介绍transition transform translate各自的用途、用法

```
能答出transition的property、duration、time-function、delay的，transform的scale、rotate、skew的，translate是用作形变矩阵的，满足普通前端工程师的标准，否则为不满足。
另答出transform的matrix matrix3d translate加速性能的可认为满足高级前端工程师的标准
```

* 7 在DOM结构和css样式分别如下的情况下，hello实际显示的字号是多少？

```
<body>
  <div class="inner">
    <p>Hello</p>
  </div>
</body>
```

```
body{
  font-size: 14px;
}
.inner {
  font-size: 1.5em;
}
p{
  font-size: 2em;
}
```

```
答案 42px
```


* 8 简单介绍下css预处理器

```
有了解过Less、SASS、STYLUS等css预处理器的算满足普通前端工程师的标准，否则为不满足。
有实践过css预处理器且能合理分割css文件者，算满足高级前端工程师的标准。
```

* 9 请使用css绘制一个向右的等边三角形箭头，边长为50。（并非要求完全等边三角形）

```
<div id="triangle"></div>

#triangle {
  width: 0;
  height: 0;
  border-left: 43.3px solid #000;
  border-top: 25px solid transparent;
  border-bottom: 25px solid transparent;
}

```


### javascript部分

* 1 请使用最简单的方式判断一个对象obj是否是数据对象

```
Object.prototype.toString.call(obj) === "[object Array]"
```

* 2 请使用最简单的方式判断一个对象obj是否是function/undefined

```
if (obj instanceof Function) {
  console.log("true");
} else {
  console.log("false");
}

OR

if (typeof obj === "undefined") {
  console.log("true");
} else {
  console.log("false");
}
```

* 3 请使用javascript实现一个类A，使得A具有属性a、b、fooA，其中a默认值为字符串'undefined'，b默认值为'0'，fooA为匿名函数，内部就做一件事情，即打印this.a;另外A需要有方法fooB，内部也只是打印this.a。请写出代码并实例化一个A的对象a，然后判断执行a.fooA()、a.fooB()的结果。

```
function A() {
  this.a = 'undefined';
  this.b = '0';
  this.fooA = function() {
    console.log(this.a);
  }
}

A.prototype.fooB = function() {
  console.log(this.a);
}

var a = new A();
a.fooA();
a.fooB();

=====>
undefined
'undefined'
```

* 4 请重写Date的toString方法，使得Date类型对象的toString()结果格式为"YY-MM-DD HH-MM-SS"

```
Date.prototype.toString = function() {
  function to10(raw) {
    return raw > 9 ? raw + '' : '0'  + raw;
  }

  return this.getFullYear() + '-'
       + (this.getMonth() > 8 ? (this.getMonth()+1) : '0' + (this.getMonth()+1)) + '-'
       + to10(this.getDate()) + ' '
       + to10(this.getHours()) + ':'
       + to10(this.getMinutes()) + ':'
       + to10(this.getSeconds());
}
```

* 5 strict模式下，执行下述代码后将打印哪些信息？（高级前端工程师需要）

```
function fooA(){
  "use strict";

  console.log("1",this);
}

function fooB() {
  console.log("2",this);
}

function fooC() {
  var x = 5;
  eval("var x=15;console.log('3',x)");
  console.log("4",x);
}

function fooD() {
  "use strict";
  var x = 5;
  eval("var x=15;console.log('5',x)");
  console.log("6",x);
}

fooA();
fooB();
fooC();
fooD();
```

```
1 undefined
2 window对象
3 15
4 15
5 15
6 5
```
