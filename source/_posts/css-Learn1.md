---
title: CSS-Learn1
date: 2018-04-10 11:00:00
tags: css布局 清除浮动 引入css的方法  推荐工具
categories: 前端
---

## 引入css的4种方法
1.  style 属性
```
<div style="height:100px;background-color: red;"></div>
```
<div style="height:100px;background-color: red;"></div>

2. style 标签
在head标签内容中添加
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
 div{
    height: 100px;
    background-color: red;
  }
  </style>
  </head>
<body>
<div></div>
</body>
</html>
```
<div style="height:100px;background-color: red;"></div>

3. link 标签引入  
   i 创建一个a.css文件 ，并添加内容
    ```
    div{
     height: 100px;
     background-color: red;
     }
    ```
    ii 在head中添加 
    ```
    <link rel="stylesheet" type="text/css" href="a.css">
    ```
    
4. import 
	该方法是在一个css文件中引入另一个css文件，语法为
    ```
    @import url("b.css")
    ```
    
 	（以下观点属个人理解）
   
## 水平布局

### 导航栏
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    a{
      text-decoration:none;
    }
    ul{
      list-style-type: none;
    }
    ul>li{
      float:left;
      margin:20px;
    }
  </style>
  </head>
<body>
  <nav>
    <ul>
      <li><a href="#">HOME</a></li>
      <li><a href="#">ABOUT</a></li>
      <li><a href="#">CONTACT</a></li>
    </ul>
  </nav>
</body>
</html>
```

![导航栏.png](https://i.loli.net/2018/04/09/5acb3337aa951.png)

在导航条下面加一个div
```
div{
      width: 100px;
      height: 100px;
      background-color: grey;
    } 
```

### 未清除浮动效果
![未清楚浮动.png](https://i.loli.net/2018/04/10/5acc1bb8afc89.png)

### 清楚浮动效果
![2018-04-10 10-24-12 的屏幕截图.png](https://i.loli.net/2018/04/10/5acc207970cc2.png)

- 所以在给元素添加float后都有可能带来一些问题 ，所以我们需要清除浮动带来的影响。
- 清除浮动的办法有很多种，我们只用以下一种方法  
  i 给浮动元素的父元素的类  加  `clearfix`  
  ii `clearfix` 的css代码具体实现
  ```
  .clearfix::after{
       content:'';
       display:block;
       clear:both;
    }
  ```
  
## 垂直布局

### 个人理解 
 整个网页就是在做一个垂直布局 ， 而水平布局就是在整体的纵向垂直布局上做一块内容的横向水平布局
 
###  各块的垂直布局
![2018-04-10 10-45-56 的屏幕截图.png](https://i.loli.net/2018/04/10/5acc25c1a9055.png)

- 可以看到导航栏部分和所有div做整体的垂直布局
- 而导航栏这一块里面又做了水平布局
- 所以  我觉得浏览器的布局就是整体在做垂直布局，但是又有水平布局组合的复杂布局

## 实用且好用的工具推荐

[工具推荐](https://c.m.163.com/news/a/DDJFF6P905118DFD.html?spss=newsapp&fromhistory=1)