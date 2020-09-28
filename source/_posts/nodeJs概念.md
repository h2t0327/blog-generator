---
title: nodeJs概念
categories:
  - 'node'
  - '1'
tags:
  - 'node'
  - 'js'
comments: true
date: 2020-09-23 09:02:41
---

# node.js 概念

## 前言

1. node 不是web后端框架

2. node 不能用来跟spring 和flask作对比

3. node 不是后端的js

4. node 不能用来跟python和PHP作对比

5. node 是一个平台

6. node 是把多种技术结合在一起使用

7. node 是让js也能调用系统接口，开发后端应用



## node 用到了哪些技术？

- v8引擎
- libuv
- c/c++ 实现的c-ares、http-parser、openSSL、zlib等库

![image-20200922200118311](https://tva1.sinaimg.cn/large/007S8ZIlgy1gj0b4ukd40j30ws0843zw.jpg)





### 什么是nodeJs  bindings？

背景

- c/c++ 实现了一个http_parser库，很高效
- js不能调用它
- 这个时候需要一个桥梁

实现

- node用c++对http_parser做封装，使它符合一些要求，封装的这个文件叫http_parser_bindings.cpp
- Node提供的编译工具将其编译为.node文件
- js代码可以直接require这个.node文件
- 这样js就能调用这个c++库，中间的桥梁就是bindings
- 由于binding提供很多所以叫bindings

### 什么是c/c++ 插件

当需要自己实现一个c++库的时候，没有提供的binding， 也需要自己写这个bindings

### 什么是libuv

所有平台上一个通用的异步I/O库，libuv会根据系统选择合适的方案

功能：用于UDP、TCP、DNS、文件等异步操作

### 什么是v8

功能

- 将js代码转换成机器码执行
- 维护调用栈，确保js函数按顺序执行
- 内存管理，为所有对象分配内存
- 垃圾回收，重复利用无用的内存
- 实现js的标准库

注意

- v8不提供DOM API
- v8本身是多线程的
- v8执行js是单线程的
- 可以开启两个线程分别执行js
- v8本身是包含多个线程的，如垃圾回收为一个线程
- 自带event loop ，但是node基于libuv自己做了一个

### 什么是event loop

1. 什么是event？
   1. 计时器到期了
   2. 读取到文件了
   3. socket有信息了

2. 什么是loop？
   1. loop就是循环，比如while（true）循环
   2. 由于事件是分优先级的， 所以循环的时候先循环优先级高的
   3. 所以Node需要从高到低循环事件
   4. 1>2>3>1>2>3

3. 什么是event loop
   1. 操作系统可以触发事件，js可以处理事件
   2. event loop就是对事件处理顺序的管理

4. nodeJs的event loop 执行顺序
   1. 检查是否有定时器 timers
   2. 输入输出的回调 I/O callbacks 
   3. 空闲一会， 清理东西
   4. 轮询阶段  检查系统事件，  比如读文件， http请求。 poll阶段
   5. check 阶段 检查setlmmediate回调
   6. close callbacks

注意

Node大部分时间都是停留在poll阶段,一直轮询

大部分事件都在poll阶段被处理，比如读文件， http请求

## 总结

- 用libuv进行异步I/O操作
- 用event loop 管理事件处理顺序
- 用c/c++库高效处理DNS/http
- 用bindings让js能和c/c++沟通
- 用v8运行js
- 用node提供的API简化js代码

![image-20200922214518898](https://tva1.sinaimg.cn/large/007S8ZIlgy1gj0b4uzyuvj31gm0rk77x.jpg)

