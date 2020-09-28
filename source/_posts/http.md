---
title: HTTP
date: 2018-03-11 23:45:50
categories:
  - 'http'
  - ''
tags:
  - 'http'
  - 'tcp'
  - 'udp'
---

# HTTP

## URL
`URL` 俗称网址 ， 也就是统一资源`定位`符/`定位`地址
### URL 的组成

https://www.baidu.com/s?wd=hello&rsv_spt=1#1

`https` 为超文本传输协议，两个电脑之间传输内容的协议 。也就是说前面的`http` 或者 `https`指的是协议

`www.baidu.com` 域名 

`/s` 路径， 这个路径非计算机中文件路径。 `https://www.baidu.com` 这个网址默认会有一个 `/`的路径

`wd=hello&rsv_spt=1` 查询参数 ，可以点击 https://www.baidu.com/s?wd=hi&rsv_spt=1#1 会发现变成了在百度hi的内容

`#1` 锚点 ， 将网站#1 变为 #3 ，点击 https://www.baidu.com/s?wd=hello&rsv_spt=1#3 会发现直接显示在第一行的是该搜索项网页的第三个链接 ，多次修改#后面的数字就会明白了

`:80` 其实这个网址还有一个端口号，http协议的服务端口号就是对应的80。https://www.baidu.com/s?wd=hello&rsv_spt=1#1:80 这个网址的效果和 https://www.baidu.com/s?wd=hello&rsv_spt=1#1是一样的。

## DNS
>网域名称系统（DNS，Domain Name System，有时也简称为域名）是因特网的一项核心服务，它作为可以将域名和IP
>地址相互映射的一个分布式数据库，能够使人更方便的访问互联网，而不用去记住能够被机器直接读取的IP地址数串。

>例如，www.wikipedia.org是一个域名，和IP地址208.80.152.2相对应。DNS就像是一个自动的电话号码簿，我们可以
>直接拨打wikipedia的名字来代替电话号码（IP地址）。我们直接调用网站的名字以后，DNS就会将便于人类使用的名字
>（如www.wikipedia.org）转化成便于机器识别的IP地址（如208.80.152.2）。[1]

- 简单理解就是，DNS 可以把 域名 转换为IP地址 

### 两种查看域名对应IP地址的方法
```
nslookup baidu.com
ping baidu.com
```

## 请求
### 请求百度页面
![请求](//video.jirengu.com/FsfB2P_WlfvCBOfU2vUARSL0AmCg)
访问百度网站   ，我们点击第一个，然后点Request  右边的view 
![图片](//video.jirengu.com/FlXCfBPkgLIkBd4ceo1wubiB-K9k)



请求的格式是：
```
1 动词 路径 协议/版本
2 Key1: value1
2 Key2: value2
2 Key3: value3
2 Content-Type: application/x-www-form-urlencoded
2 Host: www.baidu.com
2 User-Agent: curl/7.54.0
3 
4 要上传的数据
```

###分析请求
```
GET / HTTP/1.1                        动词 路径 协议/版本
Host: www.baidu.com               key1
Connection: keep-alive             key2
Cache-Control: max-age=0      key3
...   
```
1. 请求最多包含四部分，最少包含三部分。（也就是说第四部分可以为空）
2. 第三部分永远都是一个回车（\n）
3. 动词有 GET POST PUT PATCH DELETE HEAD OPTIONS 等
    i. GET就是获取的意思
   ii. POST 就是上传的意思， 上传信息会有一个content-length ： 上传的数据长度 ，然后第四部分会有上传信息的内容
   iii. 
4. 这里的路径包括「查询参数」，但不包括「锚点」
5. 如果你没有写路径，那么路径默认为 /
6. 第 2 部分中的 Content-Type 标注了第 4 部分的格式
7. 如果有请求的第四部分，那么在 FormData 或 Payload 里面可以看到

## 响应
### 有请求就有响应，下面是百度的响应
![查看 Response Headers，点击「view source」，点击「view source]](//video.jirengu.com/FqFw99ah9wk45yKcfF5TKwrqIwI5)

- GET 请求和 POST 请求对应的响应可以一样，也可以不一样
- 响应的第四部分可以很长很长很长

```
HTTP/1.1 200 OK
Bdpagetype: 2
Bdqid: 0x8f2fe8e100013131
Bduserid: 941701595
Cache-Control: private
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html;charset=utf-8
Date: Mon, 12 Mar 2018 14:49:48 GMT
...
```

响应的格式：
```
1 协议/版本号 状态码 状态解释
2 Key1: value1
2 Key2: value2
2 Content-Length: 17931
2 Content-Type: text/html
3
4 要下载的内容
```
- 状态码要背，是服务器对浏览器说的话 ,每个记到6就好了 ，想多记可以搜HTTP状态码，看维基百科
    - 1xx 不常用
         
         >这一类型的状态码，代表请求已被接受，需要继续处理。这类响应是临时响应，只包含状态行和某些可选的响应头信息，并以空行结束。由于HTTP/1.0协议中没有定义任何1xx状态码，所以除非在某些试验条件下，服务器禁止向此类客户端发送1xx响应。[4] 这些状态码代表的响应都是信息性的，标示客户应该采取的其他行动。
    - 2xx 表示成功
         >200 OK  
    请求已成功，请求所希望的响应头或数据体将随此响应返回。
    >201 Created  
    请求已经被实现，而且有一个新的资源已经依据请求的需要而创建，且其URI已经随Location头信息返回。
    >202 Accepted  
    服务器已接受请求，但尚未处理。
    >203 Non-Authoritative Information（自HTTP / 1.1起  
     服务器是一个转换代理服务器（transforming proxy，例如网络加速器），以200 OK状态码为起源，但回应了原始响应的修改版本。
    >204 No Content  
    服务器成功处理了请求，没有返回任何内容
    >205 Reset Content  
    服务器成功处理了请求，但没有返回任何内容。与204响应不同，此响应要求请求者重置文档视图。
    >206 Partial Content  
     服务器已经成功处理了部分GET请求。
    - 3xx 表示滚吧
    >300 Multiple Choices  
    被请求的资源有一系列可供选择的回馈信息，每个都有自己特定的地址和浏览器驱动的商议信息。用户或浏览器能够自行选择一个首选的地址进行重定向。
    >301 Moved Permanently:  
    被请求的资源已永久移动到新位置，并且将来任何对此资源的引用都应该使用本响应返回的若干个URI之一。
    >302 Found  
    要求客户端执行临时重定向 ,服务器临时换了个地址
    >303 See Other  
    对应当前请求的响应可以在另一个 URI上被找到，当响应于POST（或PUT / DELETE）接收到响应时，客户端应该假定服务器已经收到数据，并且应该使用单独的GET消息发出重定向。
    >304 Not Modified   
    表示资源未被修改，因为请求头指 定的版本If-Modified-Since或If-None-Match。在这种情况下，由于客户端仍然具有以前下载的副本，因此不需要重新传输资源。
    >305 Use Proxy   
    被请求的资源必须通过指定的代理才能被访问。
    >306 Switch Proxy  
    在最新版的规范中，306状态码已经不再被使用。
    - 4xx 表示你丫错了
    >400 Bad Request  
    由于明显的客户端错误（例如，格式错误的请求语法，太大的大小，无效的请求消息或欺骗性路由请求），服务器不能或不会处理该请求。  
    >401 Unauthorized  
    类似于403 Forbidden，401语义即“未认证”，即用户没有必要的凭据。[32]该状态码表示当前请求需要用户验证。
    >402 Payment Required  
    该状态码是为了将来可能的需求而预留的。
    >403 Forbidden  
    服务器已经理解请求，但是拒绝执行它。
    >404 Not Found  
    请求失败，请求所希望得到的资源未被在服务器上发现，但允许用户的后续请求。
    >405 Method Not Allowed  
    请求行中指定的请求方法不能被用于请求相应的资源。
    >406 Not Acceptable  
    请求的资源的内容特性无法满足请求头中的条件，因而无法生成响应实体，该请求不可接受。
    - 5xx 表示好吧，我错了
    >500 Internal Server Error  
    通用错误消息，服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理。没有给出具体错误信息。
    >501 Not Implemented  
    服务器不支持当前请求所需要的某个功能。当服务器无法识别请求的方法，并且无法支持其对任何资源的请求。
    >502 Bad Gateway  
    作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应。
    >503 Service Unavailable  
    由于临时的服务器维护或者过载，服务器当前无法处理请求。
    >504 Gateway Timeout  
    作为网关或者代理工作的服务器尝试执行请求时，未能及时从上游服务器（URI标识出的服务器，例如HTTP、FTP、LDAP）或者辅助服务器（例如DNS）收到响应。
    >505 HTTP Version Not Supported  
    服务器不支持，或者拒绝支持在请求中使用的HTTP版本。
    >506 Variant Also Negotiates（RFC 2295）  
    由《透明内容协商协议》（RFC 2295）扩展，代表服务器存在内部配置错误，[64]被请求的协商变元资源被配置为在透明内容协商中使用自己，因此在一个协商处理中不是一个合适的重点。
- 状态解释没什么用
- 第 2 部分中的 Content-Type 标注了第 4 部分的格式
- 第 2 部分中的 Content-Type 遵循 MIME 规范
- - 查看 Response 或者 Preview，你会看到响应的第 4 部分