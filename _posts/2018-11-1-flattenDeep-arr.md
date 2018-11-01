---
title: 数组降维
description: 
categories: JS基础
tags: 
- 数组方法
- ES6
---  
### reduce方法  
参考[MDN Array.prototype.reduce()](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)  
 
`arr.reduce(callback,[initialValue])`   
reduce为数组中的每一个元素依次执行callback函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：  
**accumulator** 累计器  
**currentValue** 当前值  
**currentIndex** 当前索引  
**array** 数组  
  
````javascript
const flattenDeep = (arr) => Array.isArray(arr)
	  ? arr.reduce( (a, b) => [...a, ...flattenDeep(b)] , [])
	  : [arr]
````   
... 展开操作符 
允许一个表达式在某处展开，用于存在多个参数（函数调用）、多个元素（数组）、多个变量（解构赋值)  
把数组自动展开为单个值  
   
````javascript
var arr=[];
arr.push(...[1,2,3])//[1,2,3]
````
### toString方法  
eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码  
````javascript
const flattenDeep2=(arr)=>{
    var arr=arr.toString().split(','); //1,2,3,4,5
	var res=[];
	for(var i=0;i<arr.length;i++){
	    res[i]=eval(arr[i]);
	}
	return res;
}
````  

### 递归方法  
````javascript
const flattenDeep3=(arr)=>{
	var res=[];
	arr.forEach((val,ind)=>{
		if(Array.isArray(val)){
			res.push.apply(res,flattenDeep3(val));  //处理递归调用的返回值
		}else{
			res.push(val);
		}
	})
	return res;
}
````