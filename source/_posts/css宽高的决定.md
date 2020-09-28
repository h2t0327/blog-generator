---
title: CSS-元素宽高是由什么决定的
date: 2018-04-13 20:00:00
categories:
  - 'css'
tags:
  - 'css'
---

# CSS-元素宽高是由什么决定的

>  任何元素都可以是块级元素 或 行内元素
>  因为每个元素都可以设置成行内元素或块级元素   


## 行内元素表现形式
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqb3v2gjhvj309e01eq2q.jpg)
代码 
```
  <span>hello! </span>
  <span>hello! </span>
  <span>hello! </span>
  <span>hello! </span>
  <span>hello! </span>
  <span>hello! </span>
  <span>hello! </span>
  <span>hello! </span>
  <span>hello! </span>
```

- 行内元素就是在一行中显示，如果后面跟着的还是行内元素，就继续跟在后面显示，当一行不够显示时自动换行

## 块级元素表现形式
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqb423gjnaj309u02igld.jpg)
代码
```
<div style="border: 1px solid red;">123</div>
  <div style="border: 1px solid red;">123</div>
  <div style="border: 1px solid red;">123</div>
```

- 块级元素不管后面跟着的是什么元素，都会另起一行。也就是说块级元素会独占一行。
##  元素的高度由什么决定的
### span 行内元素高度由什么决定的
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    div{
      border: 1px solid blue;
    }
    span{
      border: 1px solid red;
      font-size: 72px;
    }
    .s1{
       font-family: sans-serif;  
    }
    .s2{
       font-family: monospace;
    }
    .s3{
      font-family:serif ;
    }
  </style>
</head>
<body>
  <div>
  <span class="s1">ABC</span>
  <span class="s2">ABC</span>
  <span class="s3">ABC</span>
    </div>
</body>
</html>
```
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqb4g6bbdmj30fr02yt8r.jpg)

- 可以看到， 我给每个span 都设置了一个字体， 而中间字体的高度明显高于两边的字体 。
- 每一种字体的设计师不一样， 每一种字体的设计师都会对自己设置出来的字体的默认行高不一样
- 所以，行内元素内容为字的元素的行高是由 字体的默认行高决定的。  
- 比较详细的解说可以看看这篇知乎文章[字号与行高](https://zhuanlan.zhihu.com/p/27381252)

### div 块级元素高度由什么决定的
- 从上面的程序代码可以看到， span是由一个div包裹的 。 div的告诉是中间最高的span的高度。
- 也就是说块级元素的高度是由它的内容决定的，而且是所有内容中最高的内容决定的。

## 元素的宽度是由什么决定的
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    div{
      border: 1px solid blue;
      font-size: 72px;
    }
    span{
      border: 1px solid red;
      font-size: 72px;
    }
  </style>
</head>
<body>
    <span>12345678</span>
    <div>12345678</div>
</body>
</html>
```
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqb50ogjyyj30g805jwep.jpg)

- 行内元素的宽度是由它的内容决定的，行内元素不能设置宽高
- 块级元素当没有设置宽度是默认100%宽 ，所以才会到最右边。当设置了宽度是就是固定的宽度 ， 下面我们把宽度设置为200px；
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqb5600a8aj30fc04q3yp.jpg)

- 看div的蓝色边框 ， 宽度就是固定的200px;
- 如果把div设置成行内元素，  它的宽度是怎样的呢,设置属性display:inline
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqb5itt1v9j30fu04vdg0.jpg)

-  div的宽度会收缩