---
title: 防抖与节流
description:
categories: JS基础
tags:
--- 
### 函数防抖(debounce)
在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时。
1. 给按钮加函数防抖防止表单多次提交。
2. 对于输入框连续输入进行AJAX验证时，用函数防抖能有效减少请求次数。
3. 判断scroll是否滑到底部，滚动事件+函数防抖   
 
总的来说，**适合多次事件一次响应的情况**
````javascript
function debounce(fn, wait) {
  var timer = null;
  return function () {
      var context = this
      var args = arguments
      if (timer) {
          clearTimeout(timer);
          timer = null;
      }
      timer = setTimeout(function () {
          fn.apply(context, args)
      }, wait)
  }
}
````

### 函数节流(throttle)
规定一个单位时间，在这个单位时间内，只能有一次触发事件的回调函数执行，如果在同一个单位时间内某事件被触发多次，只有一次能生效。
1. 游戏中的刷新率
2. DOM元素拖拽
3. Canvas画笔功能  

总的来说，**适合大量事件按时间做平均分配触发**。
````javascript
function throttle(fn, gapTime) {
  let _lastTime = null;
  return function () {
    let _nowTime = + new Date()
    if (_nowTime - _lastTime > gapTime || !_lastTime) {
      fn();
      _lastTime = _nowTime
    }
  }
}
````