---
title: D3.js基础
comments: true
date: 2018-08-16 14:01:56
updated: 2018-08-16 14:01:56
tags: D3
categories: D3
---

## D3.js基础用法

### 使用 D3.js

D3.js 是一个 JavaScript 函数库，并不需要通常所说的“安装”。它只有一个文件，在 HTML 中引用即可。有两种方法：

（1）下载 D3.js 的文件

 d3.zip: https://github.com/mbostock/d3/releases/download/

解压后，在 HTML 文件中包含相关的 js 文件即可。

（2）还可以直接包含网络的链接，这种方法较简单：

```
<script src="http://d3js.org/d3.v3.min.js" charset="utf-8"></script>

```
但使用的时候要保持网络连接有效，不能再断网的情况下使用。

### 开发中需要使用的工具

记事本软件：Notepad++、Editplus、Sublime Text 等，选择自己喜欢的即可。

浏览器：IE9 以上、Firefox、Chrome等，推荐用 Chrome

服务器软件：Apache、Tomcat 等

其中，服务器软件可能不是必须的，不过 D3 中有些函数需要将 HTML 文件放置于服务器目录下，才能正常使用，关于这点以后会再做说明。


### 选择集

使用 d3.select() 或 d3.selectAll() 选择元素后返回的对象，就是选择集。

另外，有人会发现，D3 能够连续不断地调用函数，形如：

d3.select().selectAll().text()。这称为链式语法。

### 选择元素

在 D3 中，用于选择元素的函数有两个：

d3.select()：是选择所有指定元素的第一个
d3.selectAll()：是选择指定元素的全部
这两个函数返回的结果称为选择集。

### 绑定数据

D3 中是通过以下两个函数来绑定数据的：

datum()：绑定一个数据到选择集上
data()：绑定一个数组到选择集上，数组的各项值分别与选择集的各元素绑定
相对而言，data() 比较常用。

在上面的代码中，用到了一个无名函数 function(d, i)。当选择集需要使用被绑定的数据时，常需要这么使用。其包含两个参数，其中：

d 代表数据，也就是与某元素绑定的数据。
i 代表索引，代表数据的索引号，从 0 开始。


### 选择、插入、删除元素

选择元素涉及的函数有两个:select 、 selectAll

关于 select 和 selectAll 的参数，其实是符合 CSS 选择器的条件的，即用“井号（#）”表示 id，用“点（.）”表示 class。


插入元素涉及的函数有两个：

append()：在选择集末尾插入元素
insert()：在选择集前面插入元素


删除一个元素时，对于选择的元素，使用 remove 即可.

##  绘制一个简单的图表

HTML 5 提供两种强有力的“画布”：SVG 和 Canvas。

### SVG

SVG，指可缩放矢量图形（Scalable Vector Graphics），是用于描述二维矢量图形的一种图形格式，是由万维网联盟制定的开放标准。SVG 使用 XML 格式来定义图形，除了 IE8 之前的版本外，绝大部分浏览器都支持 SVG，可将 SVG 文本直接嵌入 HTML 中显示。

SVG 有如下特点：

SVG 绘制的是矢量图，因此对图像进行放大不会失真。
基于 XML，可以为每个元素添加 JavaScript 事件处理器。
每个图形均视为对象，更改对象的属性，图形也会改变。
不适合游戏应用。

### Canvas

Canvas 是通过 JavaScript 来绘制 2D 图形，是 HTML 5 中新增的元素。

Canvas 有如下特点：

绘制的是位图，图像放大后会失真。
不支持事件处理器。
能够以 .png 或 .jpg 格式保存图像
适合游戏应用

### 绘制矩形

```
var width = 300;  //画布的宽度
var height = 300;   //画布的高度
 
var svg = d3.select("body")     //选择文档中的body元素
    .append("svg")          //添加一个svg元素
    .attr("width", width)       //设定宽度
    .attr("height", height);    //设定高度

```

上面的 rect 里没有矩形的属性。矩形的属性，常用的有四个：

x：矩形左上角的 x 坐标
y：矩形左上角的 y 坐标
width：矩形的宽度
height：矩形的高度
要注意，在 SVG 中，x 轴的正方向是水平向右，y 轴的正方向是垂直向下的。

```
svg.selectAll("rect")
    .data(dataset)
    .enter()
    .append("rect")
    .attr("x",20)
    .attr("y",function(d,i){
         return i * rectHeight;
    })
    .attr("width",function(d){
         return d;
    })
    .attr("height",rectHeight-2)
    .attr("fill","steelblue");

```

## 比例尺

将某一区域的值映射到另一区域，其大小关系不变，这就是比例尺（Scale）。

D3 中的比例尺，也有定义域和值域，分别被称为 domain 和 range。开发者需要指定 domain 和 range 的范围，如此即可得到一个计算关系。

### 线性比例尺

线性比例尺，能将一个连续的区间，映射到另一区间。要解决柱形图宽度的问题，就需要线性比例尺。

将 dataset 中最小的值，映射成 0；将最大的值，映射成 300。

```
var min = d3.min(dataset);
var max = d3.max(dataset);
 
var linear = d3.scale.linear()
        .domain([min, max])
        .range([0, 300]);

```

d3.scale.linear() 返回一个线性比例尺。domain() 和 range() 分别设定比例尺的定义域和值域。在这里还用到了两个函数，它们经常与比例尺一起出现：

d3.max()
d3.min()
这两个函数能够求数组的最大值和最小值.

### 序数比例尺

定义域和值域不一定是连续的，如

```
var index = [0, 1, 2, 3, 4];
var color = ["red", "blue", "green", "yellow", "black"];

```

这些值都是离散的，线性比例尺不适合，需要用到序数比例尺。

```
var ordinal = d3.scale.ordinal()
        .domain(index)
        .range(color);
```

### 坐标轴

在 SVG 画布的预定义元素里，有六种基本图形：

矩形 <rect>
圆形 <circle>
椭圆 <ellipse>
线段 <line>
折线 <polyline>
多边形 <polygon>
另外，还有一种比较特殊，也是功能最强的元素：

路径 <path>
画布中的所有图形，都是由以上七种元素组成。

D3 提供了一个组件：d3.svg.axis()。

```
//数据
var dataset = [ 2.5 , 2.1 , 1.7 , 1.3 , 0.9 ];
//定义比例尺
var linear = d3.scale.linear()
      .domain([0, d3.max(dataset)])
      .range([0, 250]);
 
var axis = d3.svg.axis()
     .scale(linear)      //指定比例尺
     .orient("bottom")   //指定刻度的方向
     .ticks(7);          //指定刻度的数量
```
d3.svg.axis()：D3 中坐标轴的组件，能够在 SVG 中生成组成坐标轴的元素。
scale()：指定比例尺。
orient()：指定刻度的朝向，bottom 表示在坐标轴的下方显示。
ticks()：指定刻度的数量。

通常在添加元素的时候就一并设定，写成如下形式：

```
svg.append("g")
  .attr("class","axis")
  .attr("transform","translate(20,130)")
  .call(axis);
```
### 动态图表

动态的图表，是指图表在某一时间段会发生某种变化，可能是形状、颜色、位置等，而且用户是可以看到变化的过程的。

D3 提供了 4 个方法用于实现图形的过渡：从状态 A 变为状态 B。

transition()
启动过渡效果。

其前后是图形变化前后的状态（形状、位置、颜色等等）


duration()
指定过渡的持续时间，单位为毫秒。

如 duration(2000) ，指持续 2000 毫秒，即 2 秒。


ease()
指定过渡的方式，常用的有：

linear：普通的线性变化
circle：慢慢地到达变换的最终状态
elastic：带有弹跳的到达最终状态
bounce：在最终状态处弹跳几次
调用时，格式形如： ease(“bounce”)。

delay()
指定延迟的时间，表示一定时间后才开始转变，单位同样为毫秒。此函数可以对整体指定延迟，也可以对个别指定延迟。

### 理解update 、 enter 、 exit

当数组的长度与元素数量不一致（数组长度 > 元素数量 or 数组长度 < 元素数量）时,使用此方法可以添加足够的元素或删除多余的元素。


update 和 enter的使用
当对应的元素不足时 （ 绑定数据数量 > 对应元素 ），需要添加元素（append）。

update 部分的处理办法一般是：更新属性值
enter 部分的处理办法一般是：添加元素后，赋予属性值

Update 和 Exit 的使用

当对应的元素过多时 （ 绑定数据数量 < 对应元素 ），需要删掉多余的元素。

exit 部分的处理办法一般是：删除元素（remove）

### 交互式操作

1. 什么是交互
交互，指的是用户输入了某种指令，程序接受到指令之后必须做出某种响应。对可视化图表来说，交互能使图表更加生动，能表现更多内容。例如，拖动图表中某些图形、鼠标滑到图形上出现提示框、用触屏放大或缩小图形等等。

用户用于交互的工具一般有三种：鼠标、键盘、触屏。

在 D3 中，每一个选择集都有 on() 函数，用于添加事件监听器。

on() 的第一个参数是监听的事件，第二个参数是监听到事件后响应的内容，第二个参数是一个函数。


鼠标常用的事件有：

click：鼠标单击某元素时，相当于 mousedown 和 mouseup 组合在一起。
mouseover：光标放在某元素上。
mouseout：光标从某元素上移出来时。
mousemove：鼠标被移动的时候。
mousedown：鼠标按钮被按下。
mouseup：鼠标按钮被松开。
dblclick：鼠标双击。
键盘常用的事件有三个：

keydown：当用户按下任意键时触发，按住不放会重复触发此事件。该事件不会区分字母的大小写，例如“A”和“a”被视为一致。
keypress：当用户按下字符键（大小写字母、数字、加号、等号、回车等）时触发，按住不放会重复触发此事件。该事件区分字母的大小写。
keyup：当用户释放键时触发，不区分字母的大小写。
触屏常用的事件有三个：

touchstart：当触摸点被放在触摸屏上时。
touchmove：当触摸点在触摸屏上移动时。
touchend：当触摸点从触摸屏上拿开时。
当某个事件被监听到时，D3 会把当前的事件存到 d3.event 对象，里面保存了当前事件的各种参数，请大家好好参详。如果需要监听到事件后立刻输出该事件，可以添加一行代码：


circle.on("click", function(){
    console.log(d3.event);
});

监听器函数中都使用了 d3.select(this)，表示选择当前的元素，this 是当前的元素，要改变响应事件的元素时这么写就好。


### 布局

选择 D3：如果希望开发脑海中任意想象到的图表。
选择 Highcharts、Echarts 等：如果希望开发几种固定种类的、十分大众化的图表。

布局的作用是：将不适合用于绘图的数据转换成了适合用于绘图的数据。

布局的作用解释成：数据转换。

D3 总共提供了 12 个布局：饼状图（Pie）、力导向图（Force）、弦图（Chord）、树状图（Tree）、集群图（Cluster）、捆图（Bundle）、打包图（Pack）、直方图（Histogram）、分区图（Partition）、堆栈图（Stack）、矩阵树图（Treemap）、层级图（Hierarchy）。

12 个布局中，层级图（Hierarchy）不能直接使用。集群图、打包图、分区图、树状图、矩阵树图是由层级图扩展来的。如此一来，能够使用的布局是 11 个（有 5 个是由层级图扩展而来）。这些布局的作用都是将某种数据转换成另一种数据，而转换后的数据是利于可视化的。

布局不是要直接绘图，而是为了得到绘图所需的数据。


### 饼状图

定义一个布局，

var pie = d3.layout.pie();

返回值赋给变量 pie，此时 pie 可以当做函数使用。

var piedata = pie(dataset);