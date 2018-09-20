---
title: JavaScript 运行机制详解——Event Loop
description:
categories: JS基础
tags: JS
---
### JavaScript是非阻塞单线程语言  
JavaScript的单线程，与它的用途有关。
作为浏览器脚本语言，JavaScript的主要用途是与用户互动，以及操作DOM。这决定了它只能是单线程，否则会带来很复杂的同步问题。
比如，假定JavaScript同时有两个线程，一个线程在某个DOM节点上添加内容，另一个线程删除了这个节点.这时浏览器应该以哪个线程为准？  

### 任务队列  
单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。  
于是，所有任务可以分成两种，一种是**同步任务**（synchronous），另一种是**异步任务**（asynchronous）。
同步任务指的是，在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；异步任务指的是，不进入主线程、而进入"任务队列"（task queue）的任务，
只有"任务队列"通知主线程，某个异步任务可以执行了，该任务才会进入主线程执行。  
具体来说，异步执行的运行机制如下。
1. 所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。  
2. 主线程之外，还存在一个"任务队列"（task queue）。
  只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。  
3. 一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，
  看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。  
4. 主线程不断重复上面的第三步。  


![](http://www.ruanyifeng.com/blogimg/asset/2014/bg2014100801.jpg)

### Event Loop
````javascript
console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

console.log('script end');
````  
以上代码虽然 `setTimeout` 延时为 0，其实还是异步。这是因为 HTML5 标准规定这个函数第二个参数不得小于 4 毫秒，不足会自动增加。
所以 `setTimeout` 还是会在 `script end` 之后打印。    

不同的任务源会被分配到不同的 Task 队列中，任务源可以分为 微任务（microtask） 和 宏任务（macrotask）。在 ES6 规范中，microtask 称为 `jobs`，macrotask 称为 `task`.   
**微任务包括 process.nextTick ，promise ，Object.observe ，MutationObserver  
宏任务包括 script ， setTimeout ，setInterval ，setImmediate ，I/O ，UI rendering**   
假设 
macro-task队列包含任务: a1, a2 , a3   
micro-task队列包含任务: b1, b2 , b3  
执行顺序为，首先执行marco-task队列开头的任务，也就是 a1 任务，
执行完毕后，在执行micro-task队列里的所有任务，也就是依次执行b1, b2 , b3，
执行完后清空micro-task中的任务，接着执行marco-task中的第二个任务，依次循环。    
由此我们得到的执行顺序应该为：  
`script(主程序代码)—>process.nextTick—>Promises…——>setTimeout——>setInterval——>setImmediate——> I/O——>UI rendering`
````javascript
console.log('script start');

setTimeout(function() {
  console.log('setTimeout');
}, 0);

new Promise((resolve) => {
    console.log('Promise')
    resolve()
}).then(function() {
  console.log('promise1');
}).then(function() {
  console.log('promise2');
});

console.log('script end');
// script start => Promise => script end => 
// promise1 => promise2 => setTimeout
````  
这里要注意的一点在定义promise的时候，promise构造部分是**同步**执行的.  
````javascript
setTimeout(function(){console.log(1)},0);

new Promise(function(resolve,reject){
   console.log(2);
   resolve();
}).then(function(){console.log(3)
}).then(function(){console.log(4)});

process.nextTick(function(){console.log(5)});

console.log(6);
//输出2,6,5,3,4,1
````  

### 参考  
- [JavaScript 运行机制详解：再谈Event Loop(阮一峰)](http://www.ruanyifeng.com/blog/2014/10/event-loop.html)
 

