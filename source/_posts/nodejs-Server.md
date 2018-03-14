---
title: node.js Server
date: 2018-03-14 00:00:00
tags: Server client 请求 响应
categories: 前端
---

## 脚本建Server

### 用什么脚本建服务器
- 用脚本就可以提供 HTTP 服务，不管是 Bash 脚本还是 Node.js 脚本都可以。
- 由于 Bash 脚本的语法实在是反人类，而且我们今后要学习 JavaScript，所以我们先用 Node.js 脚本试试水吧。
- 建成的服务器就是我们的电脑，没钱买服务器，穷逼的我们就用电脑做服务器实验吧，哈哈哈

### 创建node.js Server脚本
- 用bush命令操作，进个自己认为安全好用的目录
- 创建文件 `touch server.js` ,将以下内容加入：

````

var http = require('http')
var fs = require('fs')
var url = require('url')
var port = process.argv[2]

if(!port){
  console.log('请指定端口号好不啦？\nnode server.js 8888 这样不会吗？')
  process.exit(1)
}

var server = http.createServer(function(request, response){
  var parsedUrl = url.parse(request.url, true)
  var path = request.url 
  var query = ''
  if(path.indexOf('?') >= 0){ query = path.substring(path.indexOf('?')) }
  var pathNoQuery = parsedUrl.pathname
  var queryObject = parsedUrl.query
  var method = request.method

  /******** 从这里开始看，上面不要看 ************/

  console.log('HTTP 路径为\n' + path)
  if(path == '/style.css'){
    response.setHeader('Content-Type', 'text/css; charset=utf-8')
    response.write('body{background-color: #ddd;}h1{color: red;}p{color: green;}')
    response.end()
  }else if(path == '/main.js'){
    response.setHeader('Content-Type', 'text/javascript; charset=utf-8')
    response.write('alert("这是JS执行的")')
    response.end()
  }else if(path == '/'){
    response.setHeader('Content-Type', 'text/html; charset=utf-8')
    response.write('<!DOCTYPE>\n<html>'  + 
      '<head><link rel="stylesheet" href="/style.css">' +
      '</head><body>'  +
      '<h1>你好</h1>' +
      '<p>这里是你访问到的内容，字体的颜色为你访问到的css添加</p>'+
      '<script src="/main.js"></script>' +
      '</body></html>')
    response.end()
  }else{
    response.statusCode = 404
    response.end()
  }

  /******** 代码结束，下面不要看 ************/
})

server.listen(port)
console.log('监听 ' + port + ' 成功\n请用在空中转体720度然后用电饭煲打开 http://localhost:' + port)

````

- 运行 `node server.js` ,如果开始创建文件没有加后缀就运行 `node server` ,会看到报错  
	![](http://ww1.sinaimg.cn/large/006WOZytgy1fpbmpoffrjj308002aweh.jpg)  
	没有监听端口那我们就 `node server 8888`
- 成功之后，这个 server 会保持运行(相当于服务器开始运行了，可以接受请求了)，无法退出
	- 如果你想「中断」这个 server，按 <kb>Ctrl</kbd> + <kbd>C</kbd> 即可（C 就是 Cancel 的意思）
	- 中断后你才能输入其他命令
	- 我建议你把这个 server 放在那里别动，新开一个 Bash 窗口，完成下面的教程

### 服务器当前的功能
1. 这个服务器目前只有一个功能，那就是打印出路径
2. 发出响应，返回一个页面

### 发送请求
* 使用bush 或者 浏览器 向我们这个服务器发起请求 ，那么服务器的地址是什么？  
>服务器的地址当然就是我们的本地地址啦 ，`http://127.0.0.1` 或者 `http://localhost` 发起访问： 报错
![](http://ww1.sinaimg.cn/large/006WOZytgy1fpbn1ddvzmj30f70ffdg5.jpg)    
- 我们还是忘记了，http 访问 必须 IP + 端口号 ，所以，我们重新访问 `http://127.0.0.1:8888` 
![](http://ww1.sinaimg.cn/large/006WOZytgy1fpbnfc8nsaj30p505haaa.jpg)

### 服务器响应
可以看到服务器响应给我们了一个页面， 有HTML内容的显示，css样式的加持，JS动态的弹窗
- 同时 服务器打印出请求的路径  
![](http://ww1.sinaimg.cn/large/006WOZytgy1fpbnj1w33ej30bt03074h.jpg)

### 我们需要知道的
```
response.setHeader('Content-Type', 'text/css; charset=utf-8')  //设置响应内容的类型，以及响应内容的编码方式，返回                                                                  //css文件 
response.setHeader('Content-Type', 'text/javascript; charset=utf-8') //返回js文件
response.setHeader('Content-Type', 'text/html; charset=utf-8')     //返回html文件
 response.statusCode = 404                   //返回状态码
response.write('Hi')          //响应内容
response.end()             //响应结束
```