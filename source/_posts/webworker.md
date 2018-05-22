---
title: webworker
tags: tags
date: 2018-05-14 10:44:47
---
### 如何理解Js的单线程
<img src="../assets/blogImg/eventloop.png" alt="Event Loop"/>


1. 所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。
2. 主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
3. 一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
4. 主线程不断重复上面的第三步。
### Event Loop
### MicroTasks 
 - process.nextTick
 - promise
 - Object.observe
### Macrotasks
 - setTimeout
 - setInterval
 - setImmediate
 - I/O
 
``` javascript
console.log('start')

const interval = setInterval(() => {  
  console.log('setInterval')
}, 0)

setTimeout(() => {  
  console.log('setTimeout 1')
  Promise.resolve()
    .then(() => {
      console.log('promise 3')
    })
    .then(() => {
      console.log('promise 4')
    })
    .then(() => {
      setTimeout(() => {
      console.log('setTimeout 2')
      Promise.resolve()
        .then(() => {
          console.log('promise 5')
        })
        .then(() => {
          console.log('promise 6')
        })
        .then(() => {
          clearInterval(interval)
        })
      }, 0)
    })
}, 0)

Promise.resolve()
  .then(() => {  
    console.log('promise 1')
  })
  .then(() => {
    console.log('promise 2')
  })
  
// result 
start
promise 1
promise 2
setInterval
setTimeout 1
promise 3
promise 4
setInterval
setTimeout 2
promise 5
promise 6
```
chrome 66.0.3359.181 测试第二个setInterval会打印两次

### [WebWorker](https://developer.mozilla.org/zh-CN/docs/Web/API/Web_Workers_API/Using_web_workers)
```javascript
var myWorker = new Worker('worker.js');
```
