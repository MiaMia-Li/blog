---
title: 斐波那契数列
description: 
categories: 算法
tags: 剑指offer
---

### 斐波那契数列  
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。
n<=39  
````javascript
function Fibonacci(n)
{
    if(n==0){
        return 0;
    }
    if(n==1||n==2){
        return 1;
    }
    var f1=1,f2=1,f3=0;
    for(var i=3;i<=n;i++){
        f3=f1+f2;
        f1=f2;
        f2=f3;
    }
    return f3;
}
````    
### 跳台阶  
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。  
递归公式`f(n)=f(n-1)+f(n-2)`  
````javascript
function jumpFloor(number)
{
    if(number<=3){
        return number;
    }
    var f1=2,f2=3,f3=0;
    for(var i=4;i<=number;i++){
        f3=f1+f2;
        f1=f2;
        f2=f3;
    }
    return f3;
}
````

### 变态跳台阶  
一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。  
````javascript
function jumpFloorII(number)
{
    if(number==0||number==1){
        return 1;
    }
    return 2* jumpFloorII(number-1);
}
````

### 矩形覆盖  
我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？
````javascript
function rectCover(number)
{
    if(number<=2){
        return number;
    }
    var f1=1,f2=2,f3=0;
    for(var i=3;i<=number;i++){
        f3=f1+f2;
        f1=f2;
        f2=f3;
    }
    return f3;
}
````
