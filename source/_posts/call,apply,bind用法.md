---
title: call,apply,bind用法
date: 2018-05-28 23:00:00
tags: call apply bind
categories: 前端
---

##  call
```
var obj = {
   name: 'hht',
   age : 1
}

function f(name,age){
  this.name = name;
  this.age = age;
  console.log(this.name);
  console.log(this.age);
}

f.call(obj,'mmd',18);
```
![](https://ws1.sinaimg.cn/large/006WOZytgy1fromntpn9mj305i02za9v.jpg)
- call()方法调用一个函数, 其具有一个指定的this值和分别地提供的参数(参数的列表).
- call 的第一个参数是指定调用的这个函数的this ，非严格模式下this的值如果是null或者undefine ，那么这个this指向window
- call 第二个以及之后的参数就是我们的arguments的值

## apply
```
var obj = {
   name: 'hht',
   age : 1
}

function f(name,age){
  this.name = name;
  this.age = age;
  console.log(this.name);
  console.log(this.age);
}

f.apply(obj,['mmd',18]);
f.apply(obj,{0: 'mmd', 1: 18, length: 2});
```
![](https://ws1.sinaimg.cn/large/006WOZytgy1frompayhl9j304s03u3yb.jpg)
- call()方法的作用和 apply() 方法类似，只有一个区别，就是 call()方法接受的是若干个参数的列表，而apply()方法接受的是一个包含多个参数的数组, 或伪数组。

## bind
```
var obj = {
   name: 'hht',
   age : 1
}

function f(){
  for(let i = 0; i < 4; i++)
  {
    console.log(arguments[i]);
  }
  console.log(this);
}

var f1Bind = f.bind(obj,'hht',18);
f1Bind();
f1Bind(1,2);
```
![](https://ws1.sinaimg.cn/large/006WOZytgy1fromlqepfyj30au078mx7.jpg)
- bind 绑定时接受的参数跟 call 一致.
- bind 不会立即调用，它会生成一个新的函数，你想什么时候调就什么时候调。
- bind 绑定好的this不会改变
- bind 绑定时的给的参数会成为这个绑定函数的固定参数，调用这个函数时这几个参数一定会在
