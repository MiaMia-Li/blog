--- 
title: JS解析与执行过程
description: 
categories: JS基础
tags:
--- 
 
![](https://segmentfault.com/img/bVbe2UQ?w=1744&h=782)
### 全局代码处理过程
#### 预解析阶段 
1. 读取整个源代码
2. 先查找函数声明，在查找变量声明 
  - 函数声明有冲突，会覆盖 
  - 变量声明有冲突，会忽略
3. 将找到的函数和变量保存到一个对象中（全局的保存到window对象中）
4. 变量的值是undefined，函数的值则指向该函数（函数字符串） 
  
#### 运行阶段 
从上至下，顺序执行  

### 函数处理过程
#### 预解析阶段 
1. 读取整个函数源代码
2. 将函数的参数添加到词法对象中
3. 先查找函数声明，再查找变量声明 
  - 若有重复的函数声明，则后面的会把前面的覆盖 
  - 若有重复的变量声明，会忽略
4. 将找到的函数和变量保存到一个词法对象中
5. 变量的值是undefined，函数的值则指向该函数（函数字符串） 

#### 运行阶段 
从上至下，顺序执行

### 执行上下文  
当执行 JS 代码时，会产生三种执行上下文
- 全局执行上下文
- 函数执行上下文
- eval 执行上下文  

每个执行上下文中都有三个重要的属性
- 变量对象（VO），包含变量、函数声明和函数的形参，该属性只能在全局上下文中访问
- 作用域链（JS 采用词法作用域，也就是说变量的作用域是在定义时就决定了）
- this    
![](https://dailc.github.io/staticResource/blog/basicKnowledge/whenyouenteraurl/js_engine_context.png)  

#### VO与AO
VO是执行上下文的属性（抽象概念），但是只有全局上下文的变量对象允许通过VO的属性名称来间接访问（因为在全局上下文里，全局对象自身就是变量对象）  
AO（activation object)，当函数被调用者激活，AO就被创建了  
````javascript
var a = 10
function foo(i) {
  var b = 20
}
foo()
````
对于上述代码，执行栈中有两个上下文：全局上下文和函数 foo 上下文。
````
stack = [
    globalContext,
    fooContext
]
````
对于全局上下文来说，VO 大概是这样的
````
globalContext.VO === globe
globalContext.VO = {
    a: undefined,
	foo: <Function>,
}
````
对于函数 foo 来说，VO 不能访问，只能访问到活动对象（AO）
````
fooContext.VO === foo.AO
fooContext.AO {
    i: undefined,
	b: undefined,
    arguments: <>
}
// arguments 是函数独有的对象(箭头函数没有)
// 该对象是一个伪数组，有 `length` 属性且可以通过下标访问元素
// 该对象中的 `callee` 属性代表函数本身
// `caller` 属性代表函数的调用者
````

#### 作用域链 
可以把它理解成包含自身变量对象和上级变量对象的列表，通过 `[[Scope]]` 属性查找上级变量
````
fooContext.[[Scope]] = [
    globalContext.VO
]
fooContext.Scope = fooContext.[[Scope]] + fooContext.VO
fooContext.Scope = [
    fooContext.VO,
    globalContext.VO
]
````    
#### this指针  
this是执行上下文环境的一个属性，而不是某个变量对象的属性  
- this是没有一个类似搜寻变量的过程
- 当代码中使用了this，这个 this的值就直接从执行的上下文中获取了，而不会从作用域链中搜寻
- this的值只取决中进入上下文时的情况  
  
##### 一个🌰
````javascript
var baz = 200;
var bar = {
    baz: 100,
    foo: function() {
        console.log(this.baz);
    }
};
var foo = bar.foo;

// 进入环境：global
foo(); // 200，严格模式中会报错，Cannot read property 'baz' of undefined

// 进入环境：global bar
bar.foo(); // 100
````
### 参考
- [JS的预解析与执行过程详解](https://blog.csdn.net/bingo_wangbingxin/article/details/79159015)
- [InterviewMap](https://yuchengkai.cn/docs/zh/frontend/#this)