---
title: ES6读书笔记(一)
tags: 
  - ES6
  - js
---
### let和const
- **暂时性死区**：只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响，使用let命令声明变量之前，该变量都是不可用的
```javascript
if (true) {
  // TDZ开始
  tmp = 'abc'; // ReferenceError
  console.log(tmp); // ReferenceError

  let tmp; // TDZ结束
  console.log(tmp); // undefined

  tmp = 123;
  console.log(tmp); // 123

  typeof x; // ReferenceError
  let x;
}
```
**for循环变量部分是父作用域，循环体内是子作用域**
```javascript
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
```
<!-- more -->
- **不允许重复声明**:let不允许在相同作用域内，重复声明同一个变量,因此不能在函数内部重新声明参数
```javascript
function func(arg) {
  let arg; // 报错
}

function func(arg) {
  {
    let arg; // 不报错
  }
}
```
- **块级作用域与函数声明**
  - 允许在块级作用域内声明函数。
  - 函数声明类似于var，即会提升到全局作用域或函数作用域的头部。
  - 同时，函数声明还会提升到所在的块级作用域的头部
```javascript
// 浏览器的 ES6 环境
function f() { console.log('I am outside!'); }

(function () {
  if (false) {
    // 重复声明一次函数f
    function f() { console.log('I am inside!'); }
  }

  f();
}());
// Uncaught TypeError: f is not a function
```
- **const:const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动**
```javascript
const a = [];
a.push('Hello'); // 可执行
a.length = 0;    // 可执行
a = ['Dave'];    // 报 错
```
常量a是一个数组，这个数组本身是可写的，但是如果将另一个数组赋值给a，就会报错
如果想将对象冻结，应该使用[Object.freeze()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)
```javascript
const foo = Object.freeze({});

// 常规模式时，下面一行不起作用；
// 严格模式时，该行会报错
foo.prop = 123;
```
彻底将对象冻结的函数
```javascript
var deepFreeze = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach((key) => {
    var prop = obj[key]
    if (prop && typeof prop === 'object' ) {
      deepFreeze(prop)
    }
  });
};
// Object.keys不包含对象不可枚举属性，完整版本
var deepFreeze = (obj) {
  Object.freeze(obj)
  var propNames = Object.getOwnPropertyNames(obj)
  propNames.forEach((key) => {
    var prop = obj[key]
    if (prop && typeof prop === 'object' ) {
      deepFreeze(prop)
    }
  })
}
```
### 变量的解构赋值
注意⚠️⚠️
```javascript
let arr = new Array(5);

arr[0] = 1;
arr[4] = 5;

function iteration(item = 2, index = 1) {
  return item * index;
}

let result = arr.map(iteration) // [0,undefined,undefined,undefined,20]

```
### 函数的扩展
```javascript
function foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) // undefined 5
foo({x: 1}) // 1 5
foo({x: 1, y: 2}) // 1 2
foo() // TypeError: Cannot read property 'x' of undefined

```
如上图，只用了对象的解构赋值，即只有函数参数为对象时，x y才通过解构赋值生成，当参数不是对象时就会报错，改进代码如下
```javascript
function foo({x, y = 5} = {}) {
  console.log(x, y);
}
```
函数参数默认值的两种写法与对比
```javascript
function m1({x = 0, y = 0} = {}) {
  console.log(x,y)
}
function m2({x, y} = {x = 0, y = 0}) {
  console.log(x,y)
}

// 函数没有参数的情况
m1() // [0, 0]
m2() // [0, 0]

// x 和 y 都有值的情况
m1({x: 3, y: 8}) // [3, 8]
m2({x: 3, y: 8}) // [3, 8]

// x 有值，y 无值的情况
m1({x: 3}) // [3, 0]
m2({x: 3}) // [3, undefined]

// x 和 y 都无值的情况
m1({}) // [0, 0];
m2({}) // [undefined, undefined]

m1({z: 3}) // [0, 0]
m2({z: 3}) // [undefined, undefined]
```
### 数组的扩展
- 扩展运算符：…可以将一个数组转换为用，分隔的参数队列
```javascript
// ES5 的写法
Math.max.apply(null, [14, 3, 77])

// ES6 的写法
Math.max(...[14, 3, 77])

// 等同于
Math.max(14, 3, 77);
```
- 扩展方法：Array.from()、Array.of()、Array.copyWithin()、Array.keys()、Array.values()、Array.entries()、
Array.find()、Array.findIndex()、Array.includes()、Array.fill()