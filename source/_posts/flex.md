---
title: Flex布局
date: 2018-05-23 23:00:00
tags: flex
categories: 前端
---

# Flex布局

[阮一峰-Flex布局](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)  
[阮一峰-Flex布局实例教程](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
## Flex布局

### 块级元素
```
.box{
  display: flex;
}
```
### 行内元素
```
.box{
  display: inline-flex;
}
```
- 注意，设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效

## Flex布局属性
- 采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。
- 主轴：水平线 
- 交叉轴：垂直线

### flex-direction属性
- 决定主轴的方向 或  交叉轴的方向
```
	.box{
   		 // flex-direction: row;  从左至右
         // flex-direction: row-reverse;  从右至左
         // flex-direction: column;  从上至下
         // flex-direction: column-reverse;  从下至上
    }
```

### flex-wrap属性
- 决定如何换行
```
	.box{
   	  //flex-wrap: nowrap;     不换行
         //flex-wrap: wrap;    换行，第一行在上方（从上往下）
         //flex-wrap: wrap-reverse;  换行，第一行在下方（从下往上）
    }
```

### flex-flow属性
- `flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`。
```
    .box {
     	// flex-flow: <flex-direction> || <flex-wrap>;
        // flex-flow: row nowrap;
    }
```

### justify-content属性
- 决定了项目的水平对齐方式
- 与 主轴的方向有关，以下假设为`flex-direction: row;`
```
.box {
  // justify-content: flex-start;   左对齐
  // justify-content: flex-end;    右对齐
  // justify-content: center;     居中对齐
  // justify-content: space-between;  两端对齐，项目之间的间隔都相等。
  // justify-content: space-around; 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
}
```

### align-items属性
- 决定了项目的垂直对齐方式
- 与交叉轴的方向有关，以下假设为`flex-direction: column;`
```
// align-items: flex-start 上对齐
// align-items: flex-end：下对齐
// align-items: center：居中对齐
// align-items: baseline: 项目的第一行文字的基线对齐。
// align-items: stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```
### align-content属性
- align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
```
.box {
 // align-content: flex-start;  与交叉轴的起点对齐。
 // align-content: flex-end;    与交叉轴的终点对齐。
 // align-content: center;		与交叉轴的中点对齐。
 // align-content: space-between;  与交叉轴两端对齐，轴线之间的间隔平均分布。
 // align-content: space-around;  每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
 // align-content: stretch;  轴线占满整个交叉轴。
}
```

## 项目的属性
```
order : 0123...（优先级设置） 项目的排列顺序
flex-grow：0123...（默认为0,不放大） 项目的放大比例，自动按比列分配容器空间
flex-shrink：0123...（默认为1,默认空间不足时可等比缩放，为0不缩）
flex-basis：length | auto 设置项目的主轴空间（main size） ，auto 为项目的本来大小
flex： 前三个的省略写法属性 ，两个快捷值 auto（1  1 auto） none （0 0 auto）
align-self：auto | flex-start | flex-end | center | baseline | stretch;
允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
```