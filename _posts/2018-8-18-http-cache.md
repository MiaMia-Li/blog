---
title: Http缓存总结
description:
categories: Http
tags:
--- 
## 前言
接上一篇[从输入URL到页面加载的过程]({{site.url}}/http/2018/09/17/http-url/)中，
http的缓存问题，这部分内容很重要，便来温习梳理一遍。  

## 简单介绍HTTP报文  
HTTP报文就是浏览器和服务器间通信时发送及响应的数据块。  
浏览器向服务器请求数据，发送请求(request)报文；服务器向浏览器返回数据，返回响应(response)报文。
报文信息主要分为两部分
1. 包含属性的首部(header)  附加信息（cookie，缓存信息等）**与缓存相关的规则信息，均包含在header中**
2. 包含数据的主体部分(body)  HTTP请求真正想要传输的部分

## http缓存规则   
HTTP缓存有多种规则，根据是否需要重新向服务器发起请求来分类，可以将其分为两大类(强制缓存，对比缓存)，强制缓存如果生效，不需要再和服务器发生交互，而对比缓存不管是否生效，都需要与服务端发生交互。  
两类缓存规则可以同时存在，强制缓存优先级高于对比缓存，也就是说，当执行强制缓存的规则时，如果缓存生效，直接使用缓存，不再执行对比缓存规则。  
下图是http缓存流程  
![](https://segmentfault.com/img/bVS05q?w=790&h=623)   

### 强制缓存  
强制缓存，在缓存数据未失效的情况下，可以直接使用缓存数据，那么浏览器是如何判断缓存数据是否失效呢？  
在没有缓存数据的时候，浏览器向服务器请求数据时，服务器会将数据和缓存规则一并返回，**缓存规则信息包含在响应header中**。  
对于强制缓存来说，响应header中会有两个字段来标明失效规则（**Expires/Cache-Control**） 
如图，Google开发者工具中，可看到对于强制缓存生效时，网络请求的情况。
![]({{site.url}}/assets/images/2018-9-17-http-url/disk-cache.png)  

#### Expires  
Expires的值为服务端返回的到期时间，即下一次请求时，请求时间小于服务端返回的到期时间，直接使用缓存数据。  
不过Expires 是HTTP 1.0的东西，现在默认浏览器均默认使用HTTP 1.1，所以它的作用基本忽略。
另一个问题是，到期时间是由服务端生成的，但是客户端时间可能跟服务端时间有误差，这就会导致缓存命中的误差。
所以HTTP 1.1 的版本，使用Cache-Control替代。
#### Cache-Control
Cache-Control 是最重要的规则。常见的取值有private、public、no-cache、max-age，no-store，默认为private。  
参考[MDN Cache-Control](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Cache-Control)  
 
|值|含义|  
|---|---|
|private|表明响应只能被单个用户缓存，不能作为共享缓存（即代理服务器不能缓存它）,可以缓存响应内容|
|public|表明响应可以被任何对象（包括：发送请求的客户端，代理服务器，等等）缓存|
|max-age=xxx|设置缓存存储的最大周期，超过这个时间缓存被认为过期(单位秒)。与Expires相反，时间是相对于请求的时间|
|no-cache|在释放缓存副本之前，强制高速缓存将请求提交给原始服务器进行验证|
|no-store|缓存不应存储有关客户端请求或服务器响应的任何内容|   
一个例子:
![]({{site.url}}/assets/images/2018-9-17-http-url/max-age.png)
图中Cache-Control仅指定了max-age，所以默认为private，缓存时间为2592000秒（30天）
也就是说，在30天内再次请求这条数据，都会直接获取缓存数据库中的数据，直接使用。 
     
### 对比缓存(协商缓存)

## 参考
- [彻底弄懂HTTP缓存机制及原理](https://www.cnblogs.com/chenqf/p/6386163.html)
- [http协议缓存机制](https://segmentfault.com/a/1190000010690320)
- [从输入URL到页面加载的过程](http://www.dailichun.com/2018/03/12/whenyouenteraurl.html)