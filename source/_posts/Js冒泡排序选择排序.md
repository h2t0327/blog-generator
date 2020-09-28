---
title: Js冒泡排序&选择排序
date: 2018-05-03 23:00:00
categories:
  - 'js'
  - '排序'
tags:
  - 'js'
  - '排序'
---

# Js冒泡排序&选择排序

## 冒泡排序原理
- 两相邻的数依次比较
- 若从小到大排列两两比较时前一个数比后一个数大互换位置
- 相互比较完一轮最大的数就会到最后面，并且不再参与比较
- 循环比较 直到比较完成
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqy8ra7e3cg30d706vn7w.jpg)

## 冒泡排序步骤
1. 确定外层循环次数   数组的长度
2. 确定内层循环的次数  每确定冒泡一个数内层循环减少一次 数组长度 减 外层循环的index 
3. 相邻两数相比较  前一个数比后一个数大 互换两数位置

## 冒泡排序代码实现
```
var a = [36,26,27,2,4,19,50,48];
var temp;

for(var i= 0; i <  a.length; i++)
for(var j = 0; j < a.length-i; j++){
    if(a[j] >  a[j+1]){
        temp = a[j];
        a[j] = a[j+1];
        a[j+1] = temp;
    }
}
console.log(a);
```

## 选择排序原理
- 找未排序的元素中最小的数
- 将最小数与起始位置互换
- 直到排序完成
![](https://ws1.sinaimg.cn/large/006WOZytgy1fqy96u2mbgg30gg06n7aa.jpg)

## 选择排序步骤
1. 确定外层循环次数 index为每一次寻找最小值的起始位置 直到数组长度
2. 内层循环每次都是由起始位置 +1 直到数组长度
3. 假设每一次的起始位置为最小数 碰到更小的用更小的和后面的数继续做比较
4. 保存最小数的索引
5. 内层循环结束后最小数与起始位置互换

## 选择排序代码实现
```
var a = [4,12,13,4,3,42,33,4,43,44];
var temp;
var minIndex;

for(var i = 0; i < a.length; i ++){
    minIndex = i;
    for(var j = i + 1; j < a.length; j++){
        if(a[minIndex] > a[j]){
            minIndex = j;
        }
    }
    temp = a[minIndex];
    a[minIndex] = a[i];
    a[i] = temp;
}
console.log(a);
```