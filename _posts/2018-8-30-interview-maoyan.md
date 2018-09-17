---
title: 猫眼面经
description: 
categories: 面试
tags: 
- CSS布局
- DOM操作
- 数组方法
- 字符串
---

### 水平垂直居中布局
1. **flex**
````css
.box{
    display: flex;
    align-items: center;  /*垂直*/
    justify-content: center; /*水平*/
    height: 100vh; /*视口高度*/
}
````
2. **table**
````css
.box{
    display: table;    /* 让div以表格的形式渲染 */
    width: 100%;
    height: 100vh;
}
.content{
    display: table-cell;  /* 让子元素以表格的单元格形式渲染 */
    text-align: center;
    vertical-align: middle;
}
````

3. **relative+absolute**
````css
.box{
    position: relative;
    height: 100vh;
}
.content{
   position: absolute;
   top:50%;
   left:50%;
   transform: translate(-50%,-50%);
}
```` 

### 盒模型
标准模型中，盒模型的宽高只是内容（content）的宽高，
而在IE模型中盒模型的宽高是内容(content)+填充(padding)+边框(border)的总宽高。
````css
/* 标准模型 */
box-sizing:content-box;
 /*IE模型*/
box-sizing:border-box;  
````

### CSS-position
1. static 正常文档流，忽略left，top，right，bottom，z-index   
2. relative 相对于原本位置的定义，对周围元素没有任何影响   
3. absolute 脱离文档流，绝对定位，相对于 static 定位以外的第一个父元素进行定位。 元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 
4. fixed 相对于浏览器窗口，脱离文档流  
5. sticky 粘性定位，该定位基于用户滚动的位置。它的行为就像 position:relative; 而当页面滚动   超出目标区域时，它的表现就像 position:fixed;它会固定在目标位置。元素未滚动，top不生效，margin有效。元素滚动：top有效，margin失效。

### 块级、行内元素
1. 块级元素 自动换行，可设置高度 **div p h1~h6 ul ol dl li dd table hr blockquote address table menu pre header section aside footer**
2. 行内元素 **span br a  em b i  strong sub sup**
3. 行块级元素 有内在尺寸，可设置高宽，无法自动换行 **img  input  td  textarea**

### Ul增加多个Li
- 文档碎片documentFragment
````javascript
var fragment=document.createDocumentFragment();
var ul=document.getElementById("myList");
var li=null;
for(var i=0;i<n,i++){
    li=document.createElement("li");
    li.appendChild(document.createTextNode("item"+(i+1)));
    fragment.appendChild(li);
}
ul.appendChild(fragment);
````  
- innerHTML

### 类型判断
**typeof** 是一个一元运算，放在一个运算数之前，运算数可以是任意类型。它返回值是一个字符串，该字符串说明运算数的类型。包括：number、boolean、string、object、undefined、function等6种数据类型。typeof (null) //"object"
**instanceof** 运算符用来测试一个对象在其原型链中是否存在一个构造函数的 prototype 属性。语法：object instanceof constructor
**Object.prototype.toString.call(value)** 方法去调用对象，得到对象的构造函数名。可以解决instanceof的跨框架问题，缺点是对用户自定义的类型，它只会返回[object Object]

### 数组遍历
````javascript
//数组遍历,都不会修改数组中包含的值
//对数组每一项运行给定的函数
//every 如果该函数对每一项都返回true，则返回true
//some 如果该函数对任一项返回true，则返回true
var nums=[1,2,4,5,2,8,9];
var everyResult=nums.every(function(item,index,arr){
    return(item>2);
})
//false
var someResult=nums.some(function(item,index,arr){
    return(item>2);
})
//true

var filterResult=nums.filter(function(item,index,arr){
    return(item>2)
})
//[4,5,8,9]

var mapResult=nums.map(function(item,index,arr){
    return item*2
})
//[2,4,8,10,4,16,18]

nums.forEach(function(item,index,arr){
    //执行某些操作
})
````

### 两个有序数组，一升一降，返回第k大
````javascript
function findMax(a,b,k){
	var maxK,n=0;
	var i=a.length-1,j=0;
	while(j<a.length&&i>=0){
		if(a[i]<b[j]){
			maxK=b[j];
			j++;
			n++;
		}else if(a[i]==b[j]){
			j++;
		}else{
			maxK=a[i];
			i--;
			n++;
		}
		if(n==k){
			return maxK;
		}
	}
}
````

### 字符串压缩 aaabbcaadd---a3b2c1a2d2
````javascript
function compress(str){
	if(!str||str.length==0){
		return false;
	}
	str=str.trim();
	var cur=str[0];
	var marks='';
	var count=1;
	for(var i=0;i<str.length;i++){
		if(str[i]==cur){
			count++;
		}else{
			marks+=cur+count;
			cur=str[i];
			count=1;
		}
	}
	return marks+cur+count;
}
````