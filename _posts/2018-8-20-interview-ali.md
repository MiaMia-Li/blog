---
title: 阿里面经
description: 
categories: 面试
tags: 
- CSS布局
- Http
- 数组方法
- ES6
- Vue
---
### 两栏布局
1. **float+margin-left**
````css
aside{
	background: yellow;
	width: 200px;
	float: left;
}
div{
	margin-left: 210px;/*大于aside的宽度*/
	width: auto;
	background: red;
}
````
2. **float+overflow：hidden（形成BFC）**
````css
div{
	overflow:hidden;
	width: auto;
	background: red;
	height: 400px;
}
````
3. **flex** 
````css
body{
	display: flex;
}
aside{
	background: yellow;
	flex:0 0 200px;
}
div{
	flex:1 1 auto;
	background: red;
}
````
4. **grid**
````css
body{
	 display: grid;
	 grid-template-columns: 200px auto;
}
````
5. **table**
````css
aside{
	  width: 200px;
	  display: table-cell;
	  background: yellow;
}
div{
	display: table-cell;
	background: red;
}
````

### meta标签
<meta> 元素可提供有关页面的元信息（meta-information）  
  
| 属性 | 值 | 描述 |
| --- | --- | --- |
| charset（#） | character_set | 定义文档的字符编码。 |
| content | text | 定义与 http-equiv 或 name 属性相关的元信息。 |
| http-equiv | content-typ edefault-style refresh | 把 content 属性关联到 HTTP 头部。 |
| name | application-nam eauthor description generator keywords | 把 content 属性关联到一个名称。 |
| scheme | format/URI | HTML5不支持。定义用于翻译 content 属性值的格式。 |  

#### name属性  
name属性主要用于描述网页，与之对应的属性值为content，content中的内容主要是便于搜索引擎机器人查找信息和分类信息用的。  
meta标签的name属性语法格式是：`<meta name="参数" content="具体的参数值">。`  
其中name属性主要有以下几种参数：  
##### Keywords（关键字）  
说明：keywords用来告诉搜索引擎你网页的关键字是什么。  
举例 `<meta name ="keywords" content="science human culture">`
##### description（网站内容描述)  
说明：description用来告诉搜索引擎你的网站主要内容。   
网站内容描述（description）的设计要点:
1. 网页描述为自然语言而不是罗列关键词（与keywords设计正好相反）；
2. 尽可能准确地描述网页的核心内容，通常为网页内容的摘要信息，也就是希望搜索引擎在检索结果中展示的摘要信息；
3. 网页描述中含有有效关键词；
4. 网页描述内容与网页标题内容有高度相关性；
5. 网页描述内容与网页主体内容有高度相关性；
6. 网页描述的文字不必太多，一般不超过搜索引擎检索结果摘要信息的最多字数（通常在100中文字之内，不同搜索引擎略有差异）。  


##### robots（机器人向导）  
说明：robots用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引。content的参数有all,none,index,noindex,follow,nofollow。默认是all。  
举例 `<meta name="robots" content="none">`

##### author（作者）  
说明：标注网页的作者


#### http-equiv属性
http-equiv顾名思义，相当于http的文件头作用，它可以向浏览器传回一些有用的信息，以帮助正确和精确地显示网页内容，与之对应的属性值为content，content中的内容其实就是各个参数的变量值。  
meta标签的http-equiv属性语法格式是：`<meta http-equiv="参数" content="参数变量值"> `  
其中http-equiv属性主要有以下几种参数：

##### Expires（期限）  
说明：可以用于设定网页的到期时间。一旦网页过期，必须到服务器上重新传输。  
用法：`<meta http-equiv="expires" content="Fri,12 Jan 2001 18:18:18 GMT">`  
注意：必须使用GMT的时间格式。
##### Pragma(cache模式）  
说明：禁止浏览器从本地计算机的缓存中访问页面内容。  
用法：`<meta http-equiv="Pragma" content="no-cache">`  
注意：这样设定，访问者将无法脱机浏览。
##### Refresh（刷新）  
说明：自动刷新并转到新页面。  
用法：`<meta http-equiv="Refresh" content="2;URL">`（注意后面的分号，分别在秒数的前面和网址的后面，URL可为空）  
注意：其中的2是指停留2秒钟后自动刷新到URL网址。
##### Set-Cookie(cookie设定）  
说明：如果网页过期，那么存盘的cookie将被删除。  
用法：`<meta http-equiv="Set-Cookie" content="cookievalue=xxx; expires=Friday,12-Jan-2001 18:18:18 GMT; path=/">`  
注意：必须使用GMT的时间格式。
##### Window-target（显示窗口的设定）  
说明：强制页面在当前窗口以独立页面显示。  
用法：`<meta http-equiv="Window-target" content="_top">`  
注意：用来防止别人在框架里调用自己的页面。
##### content-Type（显示字符集的设定）  
说明：设定页面使用的字符集。  
用法：`<meta http-equiv="content-Type" content="text/html; charset=gb2312">`
##### content-Language（显示语言的设定）  
用法：`<meta http-equiv="Content-Language" content="zh-cn" />`

#### 功能
- 帮助主页被各大搜索引擎登录
- 定义页面的使用语言
- 自动刷新并指向新的页面


### put/post区别
**最根本的区别就是：POST方法不是幂等的，而PUT方法则有幂等性。**  

一个幂等操作的特点就是其任意多次执行所产生的影响均与依次一次执行的影响相同。
POST在请求的时候，服务器会每次都创建一个文件，但是在PUT方法的时候只是简单地更新，而不是去重新创建。因此PUT是幂等的。

假如我们发送两个/blog/post/Sample请求，服务器端是什么样的行为？如果产生了两个博客帖子，那就说明这个服务不是idempotent的，因为多次使用产生了副作用了嘛；如果后一个请求把第一个请求覆盖掉了，那这个服务就是idempotent的。前一种情况，每次返回结果不一样的时候，应该使用POST方法，后一种情况，应该使用PUT方法。

### http状态码
- **202**状态码：服务器已接受请求，但尚未处理；
- **301**状态码：被请求的资源已永久移动到新位置。服务器返回此响应（对 GET 或 HEAD 请求的响应）时，会自动将请求者转到新位置。永久重定向
- **302**状态码：请求的资源临时从不同的URI响应请求，但请求者应继续使用原有位置来进行以后的请求。暂时重定向
- **304**自从上次请求后，请求的网页未修改过。服务器返回此响应时，不会返回网页内容。 如果网页自请求者上次请求后再也没有更改过，您应将服务器配置为返回此响应(称为 If-Modified-Since HTTP 标头)。
- **401**状态码：请求要求身份验证。 对于需要登录的网页，服务器可能返回此响应。
- **403**状态码：服务器已经理解请求，但是拒绝执行它。与401响应不同的是，身份验证并不能提供任何帮助，而且这个请求也不应该被重复提交。
- **404**状态码：请求失败，请求所希望得到的资源未被在服务器上发现。没有信息能够告诉用户这个状况到底是暂时的还是永久的。假如服务器知道情况的话，应当使用410状态码来告知旧资源因为某些内部的配置机制问题，已经永久的不可用，而且没有任何可以跳转的地址。404这个状态码被广泛应用于当服务器不想揭示到底为何请求被拒绝或者没有其他适合的响应可用的情况下。
- **500**状态码：服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。一般来说，这个问题都会在服务器的程序码出错时出现。
- **503**状态码：由于临时的服务器维护或者过载，服务器当前无法处理请求。通常，这个是暂时状态，一段时间会恢复。

### 跨域

#### JSONP
利用`<script>`标签没有跨域限制的漏洞，通过`<script>`标签指向一个需要访问的地址并提供一个回调函数来接收数据当需要通讯时。JSONP 使用简单且兼容性不错，但是只限于 get 请求。  
`<script src="http://domain/api?param1=a&param2=b&callback=jsonp"></script>`   
在开发中可能会遇到多个 JSONP 请求的回调函数名是相同的，这时候就需要自己 封装一个 JSONP，以下是简单实现。
````javascript
function jsonp(url, jsonpCallback, success) {
	let script = document.createElement("script");
	script.src = url;
	script.async = true;
	script.type = "text/javascript";
	window[jsonpCallback] = function(data) {
		success & success(data);
	};
	document.body.appendChild(script);
}
jsonp(
	"http://xxx",
	"callback",
	function(value) {
		console.log(value);
	}
); 
````
#### CORS
浏览器会自动进行 CORS 通信，实现CORS通信的关键是后端。只要后端实现了 CORS，就实现了跨域。   
服务端设置 Access-Control-Allow-Origin 就可以开启 CORS。 该属性表示哪些 域名可以访问资源，如果设置通配符则表示所有网站都可以访问资源。 

#### document.domain 
该方式只能用于二级域名相同的情况下，比如 a.test.com 和 b.test.com 适用于 该方式。 
只需要给页面添加 document.domain = 'test.com' 表示二级域名都相同就可以实现跨域 

#### postMessage 
这种方式通常用于获取嵌入页面中的第三方页面数据。一个页面发送消息，另一个页面判断来源并接收消息 。  
````javascript
// 发送消息端
window.parent.postMessage('message', 'http://test.com'); 
// 接收消息端
var mc = new MessageChannel(); 
mc.addEventListener('message', (event) => { 
	var origin = event.origin || event.originalEvent.origin;
	if (origin === 'http://test.com') {
		console.log('验证通过')
	} 
}); 
````
### 数组去重
1. 新建一新数组，遍历传入数组，值不在新数组就push进该新数组中（IE8以下不支持数组的indexOf方法）
````javascript
function uniq1(arr){
	var temp=[];
	for(var i=0;i<arr.length;i++){
		if(temp.indexOf(arr[i])==-1){
			temp.push(arr[i]);
		}
	}
	return temp;
}
````
2. 对象键值对  
该方法执行的速度比其他任何方法都快， 就是占用的内存大一些。
**注意点**：判断是否为js对象键时，会自动对传入的键执行`toString()`
````javascript
function uniq2(arr){
	var obj={},r=[],type,val;
	for(var i=0;i<arr.length;i++){
		val=arr[i];
		type=typeof val;
		if(!obj[val]){
			obj[val]=[type];
			r.push(val);
		}else if(obj[val].indexOf(type)<0){
			obj[val].push(type);
			r.push(val);
		}
	}
	console.log(obj);
	return r;
}
````
3. ES6数组去重（无法判断对象重复）  
向 Set 加入值的时候，不会发生类型转换，所以 5 和 ‘5’ 是两个不同的值。 Set 内部判断两个值是否相同，使用的算法是 “Same-value equality”，它类似于精确相等运算符（===）。主要的区别是 NaN等于自身，而精确运算符认为 NaN 不等于自身。两个对象总是不相等的，所以无法达到对象重复去重
````javascript
function uniq3(arr){
	return Array.from(new Set(arr));
}
````
4. 排序后遍历数组
````javascript
function uniq4(arr){
	var temp=[arr[0]];
	arr.sort();
	console.log(arr);
	for(var i=1;i<arr.length;i++){
		if(arr[i]!==temp[temp.length-1]){
			temp.push(arr[i]);
		}
	}
	return temp;
}
````
5. map 值-值
````javascript
function uniq5(arr){
	var map=new Map();
	for(var i=0;i<arr.length;i++){
		var temp=arr[i];
		if(!map.has(temp)){
			map.set(temp,1);
		}else{
			continue;
		}
	}
	console.log(map)
	return [...map.keys()];
}
````
### ES6 Generate
### vue双向绑定
### vue生命周期


