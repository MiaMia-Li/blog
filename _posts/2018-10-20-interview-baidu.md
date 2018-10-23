---
title: 百度面经
description: 
categories: 面试
tags: 
- CSS布局
- Http
- ES6
- Vue
- 闭包
- 作用域链
---  
### 写在前面  
百度是三面技术，题目还是挺基础的，重点是要抓住面试官想问你什么，哪个知识点，
抽象出来就很好回答了～⛽️

### 闭包 
#### 题目 
````javascript
    var makeAdd;
    //完成makeAdd函数
    var add=makeAdd(1);
    console.log(add(2)); //3
````  
自己写成函数科里化了😓...面试官提醒其实就个闭包的应用，`makeAdd`是一个函数，
返回值也是一个函数，两个参数相加就ok了～  
ps:这是[闭包 MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures)的原题  

````javascript
	var makeAdd=function(x){
		return function(y){
			return x+y;
		}
	}
	var add=makeAdd(1);
	console.log(add(2));
````  
#### 扩展  
##### 写一个闭包  
闭包就是能够读取其他函数内部变量的函数。例如在javascript中，只有函数内部的子函数才能读取局部变量，所以闭包可以理解成**定义在一个函数内部的函数**。  
在本质上，闭包是将函数内部和函数外部连接起来的桥梁  
````javascript
　　function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n); 
　　　　}
　　　　return f2;
　　}
　　var result=f1();
　　result(); // 999
````  
##### 闭包的用途  
一个是可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。    
举🌰🌰🌰 
````javascript
var makeCounter = function() {
  var privateCounter = 0;
  function changeBy(val) {
    privateCounter += val;
  }
  return {
    increment: function() {
      changeBy(1);
    },
    decrement: function() {
      changeBy(-1);
    },
    value: function() {
      return privateCounter;
    }
  }  
};

var Counter1 = makeCounter();
var Counter2 = makeCounter();
console.log(Counter1.value()); /* logs 0 */
Counter1.increment();
Counter1.increment();
console.log(Counter1.value()); /* logs 2 */
Counter1.decrement();
console.log(Counter1.value()); /* logs 1 */
console.log(Counter2.value()); /* logs 0 */
````  
两个计数器 counter1 和 counter2 是如何维护它们各自的独立性的。每个闭包都是引用自己词法作用域内的变量 privateCounter 。  
每次调用其中一个计数器时，通过改变这个变量的值，会改变这个闭包的词法环境。然而在一个闭包内对变量的修改，不会影响到另外一个闭包中的变量。
##### 在循环中创建闭包  
````javascript
//包裹在立即执行的函数里
var btns=document.getElementsByTagName("button")
for(var i=0;i<btns.length;i++){
	btns[i].onclick=(function(){
		return function(){
			console.log("我是第" + (i+1) + "个按钮")
		}
	}(i))
} 

//ES6 let关键字  
var btns=document.getElementsByTagName("button")
for(let i=0;i<btns.length;i++){
	btns[i].onclick=(function(){
		return function(){
			console.log("我是第" + (i+1) + "个按钮")
		}
	}(i))
}
````
### flex布局  
左右宽度固定，中间自适应的三栏布局
````css
	.wrapper{
		display: flex;
		min-height: 200px;
	}
	.left{
		background: red;
		flex:0 0 200px;
	}
	.center{
		background: yellow;
		flex:0 1 auto;
		width: 100%;
	}
	.right{
		background: blue;
		flex:0 0 200px;
	}
````  

### 原生JS实现给定标签添加class  
面试官提示可以用新属性`classList`,自己之前没有了解到的  
````javascript
	function addClass(){
		var args=Array.prototype.slice.call(arguments);
		var ele=args.shift();
		var cla=args.join(' ');
		ele.classList=cla;
	}
```` 

### 写在最后  
##### **高频题**👏👏👏  
[数组去重]({{site.url}}/面试/2018/08/20/interview-ali/#数组去重)  
[获得URL中key对应的val值]({{site.url}}/面试/2018/08/17/interview-yfd/#获得url中key对应的val值)  
[盒模型]({{site.url}}/面试/2018/08/30/interview-maoyan/#盒模型)  
[position的值]({{site.url}}/面试/2018/08/30/interview-maoyan/#CSS-position)

  
 


### 参考 
- [学习Javascript闭包（Closure](http://www.ruanyifeng.com/blog/2009/08/learning_javascript_closures.html)  
- [闭包-廖雪峰](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/00143449934543461c9d5dfeeb848f5b72bd012e1113d15000)  
- [破解前端面试（80% 应聘者不及格系列）：从闭包说起](https://segmentfault.com/p/1210000009077868/read)
- [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
