---
title: HTML语义化
date: 2018-03-18 15:20:00
tags: W3C MDN HTML Tag 空Tag 可替换Tag
categories: 前端
---
# HTML-语义化-(iframe-a-form的使用)

## 语义化
参考资料：  
[semantic-html](http://justineo.github.io/slideshows/semantic-html/)  
[关于语义化 HTML 以及前端架构的一点思考](http://www.oschina.net/translate/about-html-semantics-front-end-architecture)  
[如何理解 web 语义化](http://www.zhihu.com/question/20455165)

>语义化的含义就是用正确的标签做正确的事情，html语义化就是让页面的内容结构化，便于对浏览器、搜索引擎解析；在没有样式CCS情况下也以一种文档格式显示，并且是容易阅读的。搜索引擎的爬虫依赖于标记来确定上下文和各个关键字的权重，利于 SEO。使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

列举几个常见的标签：  
标题从大到小： h1 , h2 , h3 , h4 , h5 , h6  
超链接： a  
段落： p  
无序列表： ul>li  
有序列表： ol>li  
自定义列表： dl>{dt , dd}  
[`<header>`](http://www.runoob.com/tags/tag-header.html)  
[`<main>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/main)  
[`<section>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/section)  
[`<footer>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/footer)  
[`<article>`](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/article)

## a标签

### 作用
跳转页面。 发起 HTTP GET 请求

### target 属性
- _blank 在新页面打开网页
- _self 在当前页面打开网页  
- _parent 在父页面打开网页  ， 这种要在当前页面被嵌套在一个iframe网页中容易体现出来
- _top 在最外围页面打开网页 ， 这种要在当前页面被嵌套在多个iframe网页中容易体现出来

### download
- 表示下载href所对应的网页

## iframe标签

默认宽高为300 * 150大小

### 作用
- 可以在一个网页嵌套一个网页  
例如：  
![](http://ww1.sinaimg.cn/large/006WOZytgy1fpg8heal7qj309508sdfv.jpg)

### 与 a标签

看图：  
![](http://ww1.sinaimg.cn/large/006WOZytgy1fpgqn7mfjuj309i084gm1.jpg)  
```
<iframe name=xxx src="http://baidu.com" frameborder="0"></iframe>
    <a href="http://qq.com" target="xxx">QQ</a>
    <p>我是iframe外面的P标签</p>
```

QQ为 a 标签链接  ，它的target 属性等于 `xxx`,点击QQ 就会在iframe 中打开`qq.com`的网页
iframe 标签中本来打开的网页时`baidu.com` ，iframe 有一个属性时`name` ，`name`属性等于 a标签的target属性的值，所以点击a标签的时候就会在iframe中打开a标签中的URL。

## form标签

跳转页面。 发起 HTTP POST 请求  
常用属性
- action ：  规定当提交表单时向何处发送表单数据。值为：URL
- method ：  规定用于发送表单数据的 HTTP 方法。值只能是： GET 或 POST请求
- target ：  规定在何处打开 action URL。值为：	
 i. _blank  
 ii. _self  
 iii. _parent  
 iv. _top  
 和 标签是一样的。  
-  `<form>` 元素包含一个或多个如下的表单元素：   ```<input>
<textarea>
<button>
<select>
<option>
<optgroup>
<fieldset>
<label>
```  

### input标签
type属性:
 1. text： 简单文本输入
 2. password： 加密文本输入
 3. radio： 单选框 ，相同的name ，为一组单选框
 4. chekbox： 复选框 ， 相同的name ，为一组复选框
 5. reset： 重置按钮 ，value为按钮名字，重置之前所有的输入
 6. submit：提交按钮 ，value为按钮名字 ，将输入的内容提交至 form 标签的 action属性对应的URL中
 7. button： 普通按钮 ，value为按钮名字
- 注意： 要想输入的内容能提交 ， 需要加一个name属性

require属性： 加了这个属性就表示，输入框中必须有输入

lable : lable for id , lable标签for 中值  ，对应lable想关联的标签的id 值。

textarea: 文本输入框

select ： 下拉菜单 ， option为选项