---
title: 关于this
tags: 
  - js
date: 2017-09-26 15:04:58
---
### [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- 无论是否在严格模式下，在全局执行上下文中（在任何函数体外部）this都指代全局对象(window||global)。
- 在函数内部，this的值取决于函数被调用的方式,可以通过call或apply改变this的值
```javascript
function add(c, d) {
  return this.a + this.b + c + d;
}

var o = {a: 1, b: 3};

// The first parameter is the object to use as
// 'this', subsequent parameters are passed as 
// arguments in the function call
add.call(o, 5, 7); // 1 + 3 + 5 + 7 = 16

// The first parameter is the object to use as
// 'this', the second is an array whose
// members are used as the arguments in the function call
add.apply(o, [10, 20]); // 1 + 3 + 10 + 20 = 34
```
<!-- more -->
### bind
调用f.bind(某个对象)会创建一个与f具有相同函数体和作用域的函数，但是在这个新函数中，this将**永久地被绑定**到了bind的第一个参数，无论这个函数是如何被调用的
```javascript
function f() {
  return this.a;
}

var g = f.bind({a: 'azerty'});
console.log(g()); // azerty

var h = g.bind({a: 'yoo'}); // bind only works once!
console.log(h()); // azerty

var o = {a: 37, f: f, g: g, h: h};
console.log(o.f(), o.g(), o.h()); // 37, azerty, azerty
```
### bind call apply三者的异同
### 如何实现bind
```javascript
function.prototype.bind = function() {
  var fc = this // 指向实际调用bind的fucntion
  var thisArg = Array.prototype.slice.call(arguments,0,1)
  return function() {
    return fc.apply(thisArg)
  }
}
```
### arrow function
- 箭头函数的this默认指向在定义它时,它所处的对象(宿主对象),而不是执行时的对象
- 如果有对象嵌套的情况，则this绑定到最近的一层对象上
```javascript
var globalObject = this;
var foo = (() => this);
console.log(foo() === globalObject); // true
// 作为对象的一个方法调用
var obj = {foo: foo};
console.log(obj.foo() === globalObject); // true

// 尝试使用call来设定this
console.log(foo.call(obj) === globalObject); // true

// 尝试使用bind来设定this
foo = foo.bind(obj);
console.log(foo() === globalObject); // true
```
多层嵌套的情况
```javascript
var obj1={  
  num:4,  
  fn:function(){  
    var f=() => {    //object，也就是指obj1  
      console.log(this);  
        setTimeout(() => {  
          console.log(this); //object，也就是指obj1  
        });  
      }  
    f();  
  }  
}  
obj1.fn();

var obj1={  
  num:4,  
  fn:function(){  
    var f= function () {    //window,因为函数f定义后并没有对象调用，this直接绑定到最外层的window对象 
      console.log(this);  
        setTimeout(() => {  
          console.log(this); //window，外层this绑定到了window,内层也相当于定义在window层（全局环境
        });  
      }  
    f();  
  }  
}  
obj1.fn();

var obj1={  
  num:4,  
  fn:function(){  
    var f=() => {    //object,f()定义在obj1对象中，this就指向obj1,这就是箭头函数this指向的关键 
      console.log(this);  
        setTimeout(function () {  
          console.log(this);
          // window，非箭头函数的情况下要看宿主对象是谁，如果没有被对象调用，函数体中的this就绑定的window上  
        });  
      }  
    f();  
  }  
}  
obj1.fn();
```