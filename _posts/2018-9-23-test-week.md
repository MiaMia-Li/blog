---
title: 一周笔试总结 
description: 作业帮 ihandy 百度
categories: 笔试
tags:
- JS基础
- 算法
--- 
### 创建100个宽高100px的div，div按红黄蓝绿背景色排列，页面实现10*10布局。  
````html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<style type="text/css">
		body{
			display: grid;
			grid-template-rows: repeat(10,100px);
			grid-template-columns: repeat(10,100px);
		}
	</style>
</head>
<body>
<script type="text/javascript">
	var fragment=document.createDocumentFragment();
	for(var i=1;i<=100;i++){
		var div=document.createElement('div');
		if(i%4==1){
			div.style.backgroundColor='red';
		}
		if(i%4==2){
			div.style.backgroundColor='yellow';
		}
		if(i%4==3){
			div.style.backgroundColor='blue';
		}
		if(i%4==0){
			div.style.backgroundColor='green';
		}
		div.appendChild(document.createTextNode(''+i));
		fragment.appendChild(div);
	}
	document.body.appendChild(fragment);	  
</script>
</body>
</html>
````   

### 改变作用域判断输出  
call,apply返回一个立即执行函数，bind返回函数。
````javascript
let obj1={
	name:'zuoyebang',
	getName:function(){
		return this.name;
	}
}
let obj2={name:'zyb'};
console.log(obj1.name);  //zuoyebang
console.log(obj1.getName.call(obj2));  //zyb
console.log(obj1.getName.bind(obj2)); //function getName() {}. 
````  
### typeof 运算符判断  
变量提升，还未赋值时，typeof--undefined  
+运算，有一边是字符串时则转换为字符串拼接，-运算，都为数字运算
````javascript
var a=20;
var b=18;
function sum(){
	console.log(typeof b); //undefined
	var b='19';
	return 1+b-2;
}
console.log(a+sum()); //137
````  

### ES6 Set  
值的相等  
因为 Set 中的值总是唯一的，所以需要判断两个值是否相等。
在ECMAScript规范的早期版本中，这不是基于和===操作符中使用的算法相同的算法。具体来说，对于 Set s， +0 （+0 严格相等于-0）和-0是不同的值。然而，在 ECMAScript 2015规范中这点已被更改。  
另外，NaN和undefined都可以被存储在Set 中， NaN之间被视为相同的值（尽管 NaN !== NaN） 
参考[MDN Set](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Set)
````javascript
var set=new Set([0,2,2,0,0,5,9,{},{},NaN,NaN])
console.log(set) // {0,2,5,9,{},{},NaN}
console.log(set.size)  //7  
````  

### JS eventloop  
可以参考之前总结的另一篇[JavaScript 运行机制详解]({{site.url}}/js基础/2018/09/15/js-eventloop)  
定义promise的时候，promise构造部分是**同步**执行的。其余会放入异步任务中，等同步执行完之后从task栈取出才执行。    
`console.log`是同步任务，输出`name=4`，之后执行`promise resolve()`,`name=2`
````javascript
var name='1';
new Promise(function(resolve,reject){
    resolve();
    reject();
}).then(function(){
    name='2';
}).catch(function(){
    name='3';
})
name='4';
console.log(name) //4
````  
### 闭包
````javascript
var name='tom';
function getMethod(){
    var result=function(){
        return name;
    }
    var name='jerry';
    return result;
}
var getName=getMethod();
var name1=getName();
console.log(name1);//jerry
```` 
### 原型链
````javascript
function Person(){}
var person1=new Person();
var person2=new Person();
Person.prototype.getName=function(){
    return this.name;
}
Person.prototype.name='tom';
person1.name='jerry';
var name=person2.getName();
console.log(name)//tom
````


 
 
