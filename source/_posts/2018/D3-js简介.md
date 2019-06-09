---
title: D3.js简介
comments: true
date: 2018-08-09 17:32:33
updated: 2018-08-09 17:32:33
tags: D3
categories: D3
---

## D3.js

### D3.js(Data-Driven Documents) 数据驱动文档

D3.js 是一个可以基于数据来操作文档的 Javascript 库。可以帮助你使用 HTML, CSS, SVG 以及 Canvas 来展示数据。D3 遵循现有的 Web 标准，可以不需要其他任何框架独立运行在现代浏览器中，它结合强大的可视化组件来驱动 DOM 操作。


### 特性

D3 可以将数据绑定到 DOM 上，然后根据数据来计算对应 DOM 的属性值。

D3 不是一个框架，因此也没有操作上的限制。没有框架的限制带来的好处就是你可以完全按照自己的意愿来表达数据，而不是受限于条条框框，非常灵活。D3 的运行速度很快，支持大数据集和动态交互以及动画。

### 功能

  1、选择集(Selections)
  2、动态属性
  3、enter和exit操作
  4、过渡

D3 不引入新的视觉表示方法，而是借助于现有的 Web 元素: HTML, CSS, SVG 等。D3 可以借助 SVG, Canvas 以及 HTML 将你的数据生动的展现出来。

### D3.js的学习方式

官方网站： https://d3js.org
中文版： https://d3js.org.cn
Github地址：https://github.com/d3/

学习D3.js: http://d3.decembercafe.org/index.html
学习D3.js DEMO入门： https://www.cnblogs.com/fastmover/p/7779660.html

### 学习D3需要储备的知识

```
  HTML：超文本标记语言，用于设定网页的内容
  CSS：层叠样式表，用于设定网页的样式
  JavaScript：一种直译式脚本语言，用于设定网页的行为
  DOM：文档对象模型，用于修改文档的内容和结构
  SVG：可缩放矢量图形，用于绘制可视化的图形

```

### 选择集

使用 d3.select() 或 d3.selectAll() 选择元素后返回的对象，就是选择集。

#### 选择元素
在 D3 中，用于选择元素的函数有两个：

d3.select()：是选择所有指定元素的第一个
d3.selectAll()：是选择指定元素的全部
这两个函数返回的结果称为选择集。

#### 绑定数据

D3 中是通过以下两个函数来绑定数据的：

datum()：绑定一个数据到选择集上
data()：绑定一个数组到选择集上，数组的各项值分别与选择集的各元素绑定
相对而言，data() 比较常用。

在上面的代码中，用到了一个无名函数 function(d, i)。当选择集需要使用被绑定的数据时，常需要这么使用。其包含两个参数，其中：

d 代表数据，也就是与某元素绑定的数据。
i 代表索引，代表数据的索引号，从 0 开始。
