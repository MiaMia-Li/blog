---
title: 前端面试HTML+CSS总结
description:
categories: 面试
tags:
- CSS布局
- 
---   
## HTML部分
### 什么是<!DOCTYPE>？  
DOCTYPE是html5标准网页声明，且必须声明在HTML文档的第一行。来告知浏览器的解析器用什么文档标准解析这个文档。  
文档解析类型有：
- `BackCompat`：怪异模式，浏览器使用自己的怪异模式解析渲染页面。（如果没有声明DOCTYPE，默认就是这个模式）
- `CSS1Compat`：标准模式，浏览器使用W3C的标准解析渲染页面。    
### 块级元素 行内元素  
#### 块级元素
|标签||
|---|---|
|h1-h6|标题|
|ul ol li|列表|
|p|段落|
|table|表格|
|form|表单|
|address|地址|
|blockquote|块引用|
|center|居中对齐|   
 
**特性**
1. 在新一行开始，而且其后的元素也必须另起一行显示  
2. 宽度(width)、高度(height)、内边距(padding)和外边距(margin)都可控制
3. 宽度没有设置时，默认为100%
4. 块级元素可以容纳行内元素和其他块级元素  

#### 行内元素  
|标签||
|---|---|
|a|锚点|
|b|粗体|
|br|换行|
|cite|引用|
|code|代码|
|em|强调|
|img|图片|
|input|输入框|   
|label|表格标签|
|q|短引用|
|select|项目选择|
|small|小字体文本|
|span|常用内联容器，定义文本内区块|
|strong|粗体强调|
|sub|下标|
|sup|上标|
|textarea|多行文本输入框|  

**特性**
1. 内联元素允许其他内联元素与其位于同一行 
2. 行内元素不可以设置宽高
3. 行内元素水平方向的 margin 和 padding 可以生效。但竖直方向的 margin 和 padding 不能生效
4. 行内元素只能包含数据和其他行内元素   

### HTML5离线储存   
|特性|cookie|localStorage|sessionStorage|indexDB|
|---|---|---|---|---|
|数据生命周期|一般由服务器生成，可以设置过期时间|除非被清理，否则一直存在|页面关闭就清理|除非被清理，否则一直存在|
|数据存储大小|4K|5M|5M|无限|
|与服务端通信|每次都会携带在 header 中，对于请求性能影响|不参与|不参与|不参与|    

从上表可以看到，cookie 已经不建议用于存储。如果没有大量数据存储需求的话，可以使用 localStorage 和 sessionStorage 。
对于不怎么改变的数据尽量使用 localStorage 存储，否则可以用 sessionStorage 存储。

#### 常用API
`setItem(key,value)`: 设置由参数定义的键值对。如果该键已经存在，那么对应值更新为参数中的值。  
`getItem(key)`: 获取参数中键对应的键值对  
`removeItem(key)`: 删除参数中对应的键值对  
`key(n)`: 返回索引对应的键名  
`clear`: 删除所有的键值对  
`length`: 提供存储列表中键值对的数量  

🌰 对用户访问页面的次数进行计数   
````javascript
<script type="text/javascript">
if (localStorage.pagecount)
  {
  localStorage.pagecount=Number(localStorage.pagecount) +1;
  }
else
  {
  localStorage.pagecount=1;
  }
document.write("Visits "+ localStorage.pagecount + " time(s).");
</script>
````

### 浏览器内核 
|浏览器|内核|兼容性前缀|
|---|---|---|
|IEtrident|-ms-|
|chrome|webkit|-webkit-|
|safari|webkit|-webkit-|
|firefox|gecko|-moz-|
|opera|blink|-o-|   

### meta标签  
meta标签：提供给页面的一些元信息（名称/值对）， 比如针对搜索引擎和更新频度的描述和关键词。  
- name：名称/值对中的名称。常用的有author、description、keywords、generator、revised、others。 把 content 属性关联到一个名称。
- http-equiv：没有name时，会采用这个属性的值。常用的有content-type、expires、refresh、set-cookie。把content属性关联到http头部。
- content： 名称/值对中的值， 可以是任何有效的字符串。 始终要和 name 属性或 http-equiv 属性一起使用。
- scheme： 用于指定要用来翻译属性值的方案。  

## CSS部分  
### css哪些属性可以继承  
- 字体相关：line-height, font-family, font-size, font-style, font-variant, font-weight, font
- 文本相关： letter-spacing, text-align, text-indent, text-transform, word-spacing
- 列表相关：list-style-image, list-style-position, list-style-type, list-style
- 颜色：color  

### css3有哪些新属性  
1）边框  
- border-radius：圆角边框，border-radius:25px;
- box-shadow：边框阴影，box-shadow: 10px 10px 5px #888888;
- border-image：边框图片，border-image:url(border.png) 30 30 round;  

2）背景：
- background-size：规定背景图片的尺寸，background-size:63px 100px;
- background-origin：规定背景图片的定位区域，背景图片可以放置于 content-box、padding-box 或 border-box 区域。background-origin:content-box;
- CSS3 允许您为元素使用多个背景图像。background-image:url(bg_flower.gif),url(bg_flower_2.gif);  
3）文本效果：
- text-shadow：向文本应用阴影，可以规定水平阴影、垂直阴影、模糊距离，以及阴影的颜色。text-shadow: 5px 5px 5px #FF0000;
- word-wrap：允许文本进行换行。word-wrap:break-word;  
4）字体：CSS3 @font-face 规则可以自定义字体。  
5）2D 转换（transform）
- translate()：元素从其当前位置移动，根据给定的 left（x 坐标） 和 top（y 坐标） 位置参数。 transform: translate(50px,100px);
- rotate()：元素顺时针旋转给定的角度。允许负值，元素将逆时针旋转。transform: rotate(30deg);
- scale()：元素的尺寸会增加或减少，根据给定的宽度（X 轴）和高度（Y 轴）参数。transform: scale(2,4);
- skew()：元素翻转给定的角度，根据给定的水平线（X 轴）和垂直线（Y 轴）参数。transform: skew(30deg,20deg);
- matrix()： 把所有 2D 转换方法组合在一起，需要六个参数，包含数学函数，允许您：旋转、缩放、移动以及倾斜元素。transform:matrix(0.866,0.5,-0.5,0.866,0,0);  
6）3D 转换
- rotateX()：元素围绕其 X 轴以给定的度数进行旋转。transform: rotateX(120deg);
- rotateY()：元素围绕其 Y 轴以给定的度数进行旋转。transform: rotateY(130deg);  
7）transition：过渡效果，使页面变化更平滑
- transition-property：执行动画对应的属性，例如 color，background 等，可以使用 all 来指定所有的属性。
- transition-duration：过渡动画的一个持续时间。
- transition-timing-function：在延续时间段，动画变化的速率，常见的有：ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier 。
- transition-delay：延迟多久后开始动画。  
简写为：transition: [<transition-property> || <transition-duration> || <transition-timing-function> || <transition-delay>];  
8）animation：动画  
使用CSS3 @keyframes 规则。
- animation-name: 定义动画名称
- animation-duration: 指定元素播放动画所持续的时间长
- animation-timing-function:ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>)： 指元素根据时间的推进来改变属性值的变换速率，说得简单点就是动画的播放方式。
- animation-delay: 指定元素动画开始时间
- animation-iteration-count:infinite | <number>：指定元素播放动画的循环次
- animation-direction: normal | alternate： 指定元素动画播放的方向，其只有两个值，默认值为normal，如果设置为normal时，动画的每次循环都是向前播放；另一个值是alternate，他的作用是，动画播放在第偶数次向前播放，第奇数次向反方向播放。
- animation-play-state:running | paused：控制元素动画的播放状态。  
简写为：animation:[<animation-name> || <animation-duration> || <animation-timing-function> || <animation-delay> || <animation-iteration-count> || <animation-direction>]  

### .px，em，rem，pt的区别  
1）px实际上就是像素，用px设置字体大小时，比较稳定和精确   
但是这种方法存在一个问题，当用户在浏览器中浏览我们制作的web页面时，如果对浏览器进行了缩放，这时会使我们的web页面布局被打破。因此，这时就提出了使用“em”来定义web页面的字体。  
2）em就是根据基准来缩放字体的大小   
em是相对于其父元素来设置字体大小的，这样就会存在一个问题，进行任何元素设置，都有可能需要知道他父元素的大小  
3）rem是相对于根元素字体大小来显示的    
rem是相对于根元素<html>，这样就意味着，我们只需要在根元素确定一个参考值  
4）pt的大小等于1英寸的1/72磅：他是作为文字的一种计量单位  
这种度量方式来源于打印-设计背景，最适合于媒体，但同样广泛应用于显示器  

### css3新增伪类  
 p:first-of-type 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。  
 p:last-of-type  选择属于其父元素的最后 <p> 元素的每个 <p> 元素。  
 p:only-of-type  选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。  
 p:only-child        选择属于其父元素的唯一子元素的每个 <p> 元素。  
 p:nth-child(2)  选择属于其父元素的第二个子元素的每个 <p> 元素。  
 :after          在元素之前添加内容,也可以用来做清除浮动。  
 :before         在元素之后添加内容  
 :enabled        
 :disabled       控制表单控件的禁用状态。  
 :checked        单选框或复选框被选中。  





