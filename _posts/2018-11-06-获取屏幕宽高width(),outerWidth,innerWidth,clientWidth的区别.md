---
layout: post
title: "获取屏幕宽高width的几种方法"
subtitle: "javascript width window "
author: "Few"
header-img: "img/home-bg-art.jpg"
header-mask: 0.4
tags:
  - javascript
  - width
---



## 基本介绍

### $(window).width()与$(window).height()

`$(window).width()`与`$(window).height()`：获得的是屏幕可视区域的宽高，不包括滚动条与工具条。

```
$(window).width() = width + padding
$(window).height() = height + padding
```

### document.documentElement.clientWidth与document.documentElement.clientHeight

`document.documentElement.clientWidth`与`document.documentElement.clientHeight`：获得的是屏幕可视区域的宽高，不包括滚动条与工具条，跟jquery的(window).width()与(window).height()获得的结果是一样的。

```
document.documentElement.clientWidth = width + padding
document.documentElement.clientHeight = height + padding
```

### window.innerWidth与window.innerHeight

`window.innerWidth`与`window.innerHeight`：获得的是可视区域的宽高，但是window.innerWidth宽度包含了纵向滚动条的宽度，window.innerHeight高度包含了横向滚动条的高度(IE8以及低版本浏览器不支持)。

```
window.innerWidth = width + padding + border + 纵向滚动条宽度
window.innerHeight = height + padding + border + 横向滚动条高度
```

### window.outerWidth与window.outerHeight

`window.outerWidth`与`window.outerHeight`：获得的是加上工具条与滚动条窗口的宽度与高度。

```
window.outerWidth = width + padding + border + 纵向滚动条宽度
window.outerHeight = height + padding + border + 横向滚动条高度 + 工具条高度
```

### document.body.clientWidth与document.body.clientHeight

`document.body.clientWidth`与`document.body.clientHeight`：document.body.clientWidth获得的也是可视区域的宽度，但是document.body.clientHeight获得的是body内容的高度，如果内容只有200px，那么这个高度也是200px,如果想通过它得到屏幕可视区域的宽高，需要样式设置，如下：

```
body {
height: 100%;
overflow: hidden;
}
body, div, p, ul {
margin: 0;
padding: 0;
}
```

最关键的是：body的height:100%影响document.body.clientHeight的值。
body的margin:0,padding:0影响document.body.clientWidth的值。

### offsetWidth & offsetHeight

返回本身的宽高 + padding + border + 滚动条

### offsetLeft & offsetTop

所有HTML元素拥有offsetLeft和offsetTop属性来返回元素的X和Y坐标

> 1.相对于已定位元素的后代元素和一些其他元素（表格单元），这些属性返回的坐标是相对于祖先元素
> 2.一般元素，则是相对于文档，返回的是文档坐标
>
> offsetParent属性指定这些属性所相对的父元素，如果offsetParent为null，则这些属性都是文档坐标

```
//用offsetLeft和offsetTop来计算e的位置
function getElementPosition(e){
    var x = 0,y = 0;
    while(e != null) {
        x += e.offsetLeft;
        y += e.offsetTop;
        e = e.offsetParent;
    }
    return {
        x : x,
        y : y
    };
}
```

### scrollWidth & scrollHeight

这两个属性是元素的内容区域加上内边距，在加上任何溢出内容的尺寸.

因此，如果没有溢出时，这些属性与clientWidth和clientHeight是相等的。

### scrollLeft & scrollTop

指定的是元素的滚动条的位置

scrollLeft和scrollTop都是可写的属性，通过设置它们来让元素中的内容滚动。

## 兼容性

1.window innerWidth 和 innerHeight 属性与outerWidth和outerHeight属性IE8以及以下不支持。

2.测试浏览器IE，火狐，谷歌，360浏览器，Safari都支持document.documentElement.clientWidth与document.documentElement.clientHeight。

## 结论

获取屏幕的可视区域的宽高可使用jquery的方式获得，也可以使用原生js获得，即：

document.documentElement.clientWidth与document.documentElement.clientHeight