---
title: 猿辅导面经
description: 
categories: 面试
tags: 
- Http
- 数组方法
---
### http请求头
- Accept：告诉服务器，客户端支持的数据类型。
- Accept-Charset：告诉服务器，客户端采用的编码。
- Accept-Encoding：告诉服务器，客户机支持的数据压缩格式。
- Accept-Language：告诉服务器，客户机的语言环境。
- Host：客户机通过这个头告诉服务器，想访问的主机名。
- If-Modified-Since:客户机通过这个头告诉服务器，资源的缓存时间。
- Referer:客户机通过这个头告诉服务器，它是从哪个资源来访问服务器的。（一般用于防盗链
- User-Agent:客户机通过这个头告诉服务器，客户机的软件环境。
- Cookie：客户机通过这个头告诉服务器，可以向服务器带数据。
- Connection：客户机通过这个头告诉服务器，请求完后是关闭还是保持链接。
- Date：客户机通过这个头告诉服务器，客户机当前请求时间。

### http状态码  

| 状态码 | 响应类别 | 响应类别 |  
| --- | --- | --- |  
| 1XX | 信息性状态码（Informational） | 服务器正在处理请求 |  
| 2XX | 成功状态码（Success） | 请求已正常处理完毕 |  
| 3XX | 重定向状态码（Redirection） | 需要进行额外操作以完成请求 |  
| 4XX | 客户端错误状态码（Client Error） | 客户端原因导致服务器无法处理请求 |  
| 5XX | 服务器错误状态码（Server Error） | 服务器原因导致处理请求出错 |  

-   200 OK 请求正常处理完毕
-	204 No Content 请求成功处理，没有实体的主体返回
-	206 Partial Content GET范围请求已成功处理
-	301 Moved Permanently 永久重定向，资源已永久分配新URI
-	302 Found 临时重定向，资源已临时分配新URI
-	303 See Other 临时重定向，期望使用GET定向获取
-	304 Not Modified 发送的附带条件请求未满足
-	307 Temporary Redirect 临时重定向，POST不会变成GET
-	400 Bad Request 请求报文语法错误或参数错误
-	401 Unauthorized 需要通过HTTP认证，或认证失败
-	403 Forbidden 请求资源被拒绝
-	404 Not Found 无法找到请求资源（服务器无理由拒绝）
-	500 Internal Server Error 服务器故障或Web应用故障
-	503 Service Unavailable 服务器超负载或停机维护

### 一个完整的URL
假设这是一个url地址http://localhost:8080/a/b/c?a=1&b=2#abc，里面包含的部分：
- protocol: 'http:',//协议
- host: 'localhost:8080',
- port: '8080',//端口
- hostname: 'localhost',域名
- hash: '#abc',锚点
- search: '?a=1&b=2' 等于 ?query: 'a=1&b=2',
- pathname: '/a/b/c',
- path: '/a/b/c?a=1&b=2',
- href: 'http://localhost:8080/a/b/c?a=1&b=2#abc'

### 获得URL中key对应的val值
````javascript
function getVal(url,key){
	var start=url.indexOf("?");
	var end=url.indexOf("#");
	if(start<0){
		return null;
	}
	var query=end<0?url.slice(start+1):url.slice(start+1,end);
	var pairs=query.split("&");
	var args={};
	for(var i=0;i<pairs.length;i++){
		var pos=pairs[i].indexOf("=");
		if(pos==-1){
			continue;
		}
		var argname=pairs[i].substring(0,pos);
		var value=decodeURIComponent(pairs[i].substring(pos+1));
		args[argname]=value;
	}
	return args[key];
}
````

### js小数相加
````javascript
function add(){
	var args=arguments,
	    d=0,//小数位数;
	    sum=0;
	for(var key in args){ //遍历所有参数，取最大小数位数
		var str=""+args[key];
		if(str.indexOf(".")!=-1){
			var temp=str.split(".")[1].length;
			d=d<temp?temp:d;
		}
	}
	var m=Math.pow(10,d);
	for(var key in args){
		sum+=args[key]*m;
	}
	return sum/m;
}
````

### a-z对应1-26，输入123输出abc，aw，lc
````javascript
function splitNumber(num){
	var obj={
		1:"a",
		2:"b",
		3:"c",
		12:"l",
		23:"w",
	}
	var res=[];
	var temp=[];
	var str="";
	for(var i=1;i<num.length;i++){
		temp.push(num.substring(0,i),num.substring(i));
	}
	for(var j=0;j<temp.length;j+=2){
		res.push(obj[temp[j]]+obj[temp[j+1]]);
	}
	var str="";
	for(var k=0;k<num.length;k++){
		str+=obj[num.charAt(k)];
	}
	res.push(str);
	return res;
	
}
````
