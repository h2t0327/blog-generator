---
title: HTML
date: 2018-03-14 23:00:00
tags: W3C MDN HTML Tag 空Tag 可替换Tag
categories: 前端
---

## W3C

### 历史
> 万维网联盟（W3C）由蒂姆·伯纳斯-李于1994年10月离开欧洲核子研究中心（CERN）后成立。
> 该组织试图通过W3C制定的新标准来促进业界成员间的兼容性和协议。不兼容的HTML版本由不同的供应商提供，导致网页显示方式不一致。联盟试图让所有的供应商实施一套由联盟选择的核心原则和组件。

### 标准
> 为解决网络应用中不同平台、技术和开发者带来的不兼容问题，保障网络信息的顺利和完整流通，万维网联盟制定了一系列标准并督促网络应用开发者和内容提供者遵循这些标准。标准的内容包括使用语言的规范，开发中使用的导则和解释引擎的行为等等。W3C也制定了包括XML和CSS等的众多影响深远的标准规范。

> 但是，W3C制定的网络标准似乎并非强制而只是推荐标准。因此部分网站仍然不能完全实现这些标准。特别是使用早期所见即所得网页编辑软件设计的网页往往会包含大量非标准代码。

```
-  -W3C推荐标准
CSS：层叠样式表
DOM：文档对象模型
HTML：超文本标记语言
RDF：资源描述框架
SMIL：同步多媒体集成语言
SVG：可缩放向量图形
WAI
Widgets
XHTML：可扩展超文本标记语言
XML：可扩展标记语言
```

## MDN
- MDN Web Docs 是一个汇集众多Mozilla基金会产品和网络技术开发文档的免费网站
- 该项目始于2005年，最初由Mozilla公司员工Deb Richardson领导。自2006年以来，文档工作由Eric Shepherd领导
- - 关于前端的一些技术都可以先从MDN中搜索了解，比如一些HTML标签的使用，CSS属性的使用等

## HTML

### MDN链接
[HTML All Tags ,MDN](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element)

## 空标签

### 什么是空标签？
```  
HTML，SVG 和 MathML 的规范都详细定义了每个元素能包含的具体内容（define very precisely what each element can contain）。许多组合是没有任何语义含义的，比如一个 <audio> 元素嵌套在一个 <hr> 元素里。
在 HTML 中，通常在一个空元素上使用一个闭标签是无效的。例如， <input type="text"></input> 的闭标签是无效的 HTML。
```
- 理解： 一个没有闭标签(或者说闭标签加了无效) 或者 HTML、SVG、MathML规范中没有定义标签能包含哪些内容的标签就是 空标签。

### HTML中的空标签
```
<area>
<base>
<br>
<col>
<colgroup> when the span is present
<command>
<embed>
<hr>
<img>
<input>
<keygen>
<link>
<meta>
<param>
<source>
<track>
<wbr>
```

## 可替换标签？

### 什么是可替换标签？
>可替换元素就是浏览器根据元素的标签和属性，来决定元素的具体显示内容。

```
例如浏览器会根据<img>标签的src属性的值来读取图片信息并显示出来，而如果查看(x)html代码，则看不到图片的实际内容；又例如根据<input>标签的type属性来决定是显示输入框，还是单选按钮等。
```

### 常见的几个可替换标签

```
<img>、<input>、<textarea>、<select>、<object>
```