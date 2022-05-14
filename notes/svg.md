### 一、SVG 简介

> Scalable Vector Graphics —— 可缩放的矢量图
>
> SVG 是 W3C 推出的基于 XML 的二维矢量图形标准，也就是一种用于描述二维的矢量图形。SVG 可以提供高质量的矢量图形渲染，同时由于支持 JavaScript 和文档对象模型，SVG 图形通常具有强大的交互能力。

#### 1、SVG 的优势

- SVG 是可伸缩的，并且伸缩不会对图像质量造成影响，而一般普通的图像放大或者缩小容易导致变形，例如 JPG 或 PNG 等。
- SVG 图像可在任何的分辨率下被高质量地打印。
- SVG 图像可被多种工具读取和修改，例如文本编辑器等。
- SVG 图像可被搜索、索引、脚本化或压缩 。
- SVG 图像与 JPEG 和 GIF 图像比起来，尺寸更小，且可压缩性更强。
- SVG 可以与 Java 技术一起运行。

#### 2、SVG  的使用方式

- 直接在 HTML 中作为 `<svg>` 标签使用。
- 在 HTML 中通过 `<img>` 标签来引用。
- 通过浏览器直接打开 SVG 文件。
- 可以作为 CSS 背景使用。

### 二、学习如何编写 SVG

#### 1、所有的svg图形都要求写在 svg 中。

#### 2、基本图形、属性、API

> 基本图形 —— <rect>、<circle>、<ellipse>、<line>、<polyline>、<polygon>

rect —— 矩形

```html
<rect x="" y="" width="" height="" rx="" ry="" />
x: 矩形左上角 x 位置		y: 矩形左上角 y 位置
width: 矩形宽			   height： 矩形高
rx：矩形 x 轴方向圆角       ry: 矩形 y 轴方向圆角
```

circle —— 圆

```html
<circle cx="" cy="" r="" />
cx: 圆心 x 轴位置		cy: 圆心 y 轴位置
r: 圆半径
```

ellipse —— 椭圆

```html
<ellipse cx="" cy="" rx="" ry="" />
cx: 圆心 x 轴位置		cy: 圆心 y 轴位置
rx: x 轴方向长度		    ry:  y 轴方向长度
```

line —— 线

```html
<line x1="" y1="" x2="" y2="" />
x1、y1: 开始点位置
x2、y2: 结束点位置
```

polyline —— 折线

```html
<polyline points="x1 y1 x2 y2 x3 y3 ...." />
points: 开始点到结束点的位置
```

polygon —— 多边形

```html
<polygon points="x1 y1 x2 y2 x3 y3 ...." />
points: 多边形每个点的顶点坐标
```



> 基本属性 —— fill、stroke、stroke-width、transform

- fill —— 填充颜色
- stroke —— 描边颜色
- stroke-width —— 描边厚度
- transform —— 类似于 CSS3 的 transform

> 基本操作 API

```js
// 创建图形
document.createElementNS(ns, tagName)

// 添加图形
element.appendChild(childElement)

// 设置/获取属性
element.setAttribute(name, value)
element.getAttribute(name)
```

#### 3、分组标签

- <g>标签来创建
- 分组标签上的属性会被子标签继承
- 使用 transform 属性定义分组坐标的变化
- 分组标签可以嵌套

```html
<svg>
    <!-- 这里定义了一个分组，里面有 圆 和 矩形 他们的填充颜色为 blue 描边颜色为 red -->
	<g stroke="red" fill="blue">
        <rect width="100" height="100" x="0" y="0" />
    	<circle r="50" cx="150" cy="150" />
    </g>
</svg>
```

#### 4、颜色、渐变和笔刷

##### Ⅰ、认识 RGB 和 HSL

> RGB —— 不符合人类描述颜色的习惯

- 红色、绿色、蓝色三个分量
- 格式：rgb( r, g, b ) 或 #rrggbb
- 每个分量取值范围：[ 0, 255 ]

- 优势：显示器容易解析

> HSL —— 符合人类描述颜色的习惯

- 颜色、饱和度、亮度三个分量
- 格式：hsl( h, s%, l%)
- 取值范围：
  - h：[ 0, 359 ] 
  - s，l：[ 0, 100 ]

##### Ⅱ、渐变

> 线性渐变

先看代码 —— 其实很容易懂~

```html
<svg>
	<defs>
    	<linearGradient id="grad1" gradientUnits="objectBoundingBox" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0" stop-color="red" />
            <stop offset="0.5" stop-color="blue" />
            <stop offset="1" stop-color="yellow" />
        </linearGradient>
    </defs>
    <rect x="100" y="100" fill="url(#grad1)" width="200" height="150" />
</svg>
```

<defs> —— 相当于一个容器，里面存放的就是像渐变一样的工具标签

<linearGradient> —— 线性渐变标签

```xml
<linearGradient id="grad1" gradientUnits="objectBoundingBox" x1="0" y1="0" x2="1" y2="1"></linearGradient>
<!--
	id: 为这个渐变取名字，方便以后使用
	gradientUnits: 
		objectBoundingBox: 默认值 以引用渐变的图形大小为坐标 单位 % 0 ~ 1
		userSpaceOnUser: 以 svg 左上角顶点开始为坐标 单位PX
	x1,y1: 渐变开始的点 —— 单位由 gradientUnits 类型来决定
	x2,y2: 渐变结束的点
-->
<rect x="100" y="100" fill="url(#grad1)" width="200" height="150" />
<!--
	在图形中使用 fill="url(#id)" 来使用这个渐变
-->
```

<stop> —— 渐变的颜色切换

```xml
<stop offset="0" stop-color="red" />
<stop offset="0.5" stop-color="blue" />
<stop offset="1" stop-color="yellow" />
<!--
	嵌套在渐变标签中使用，这里是一个由 红 => 蓝 => 黄 的一个渐变过程
	显而易见：
		offset —— 最终渐变到这个颜色的位置
		stop-color —— 渐变的颜色
-->
```



> 径向渐变

```xml
<!-- 使用方式与线性渐变一致。 -->
<radialGradient id="grad2" cx="0.5" cy="0.5" r="0.5" fx="0.6" fy="0.3"></radialGradient>
<!--
	cx、cy: 渐变开始的坐标
	r：渐变的半径
	fx、fy：渐变的焦点偏移位置
-->
```



> 笔刷 —— 自定义背景

```xml
<!-- 使用方式与渐变一致。 -->
<svg>
	<defs>
    	<pattern id="p1" x="0" y="0" width="0.2" height="0.2">
            <circle cx="10" cy="10" r="5" fill="red" />
            <polygon points="30 10 60 50 0 50" fill="green" />
        </pattern>
    </defs>
    <rect x="100" y="100" fill="url(#p1)" stroke="blue" width="200" height="150" />
</svg>
```

<pattern>  使用次标签定义好一个背景，可以被其他图形以 fill 的形式调用，成为那个图形的背景

### 三、Path 的使用 （高级）

#### 1、Path 概述

> 一个强大的绘图工具
>
> 规范： http://www.w3.org/TR/SVG11/paths.html
>
> 由命令及其参数组成的字符串
>
> <path d="M 0 0 l 100 100 M 0 100 l 100 -100" />

命令基本规律

- 区分大小写：大写表示坐标参数为绝对位置，小写则为相对位置
- 最后的参数表示最终要到达的位置
- 上一个命令结束的位置就是下一个命令开始的位置
- 命令可以重复表示重复执行同一条命令

#### 2、移动和直线命令

- M (x, y)+ 移动画笔，后面如果由重复参数，会当作是 L 命令处理
- L (x, y)+ 绘制直线到指定位置
- H (x)+ 绘制水平线到指定的 x 位置
- V (y)+ 绘制竖直线到指定的 y 位置
- m、l、h、v 使用相对位置绘制

```xml
<svg>
	<path d="M 0 0 h 100
             M 0 0 v 100
             M 100 0 v 100
             M 0 100 h 100
             M 0 0 l 100 100 
             M 100 0 l -100 100"
          stroke="#fff" stroke-width="2" />
</svg>
```

<div style="display: flex; justify-content: center;">
    <svg style="height: 100px; width: 100px;">
	<path d="M 0 0 h 100
             M 0 0 v 100
             M 100 0 v 100
             M 0 100 h 100
             M 0 0 l 100 100 
             M 100 0 l -100 100"
          stroke="#fff" stroke-width="2" />
</svg>
</div>


#### 3、弧线命令

> A ( rx, ry xr, laf, sf, x, y ) —— 绘制弧线

- rx - ( radius-x ) 弧线所在椭圆的 x 半轴长
- ry - ( radius-y ) 弧线所在椭圆的 y 半轴长
- xr - ( xAxis-rotation ) 弧线所在椭圆的长轴角度
- laf - ( large-arc-flag ) 是否选择弧长较长的那一段弧
- sf - ( sweep-flag ) 是否选择逆时针方向的那一段弧
- x，y - 弧的终点位置

```xml
<svg>
	<path d="M 0 0 h 100
             M 0 0 v 100
             M 0 100 A 100 100 0 0 0 100 0 
             "
          stroke="#fff" fill="transparent" />
</svg>
```

<div style="display: flex; justify-content: center;">
    <svg style="height: 100px; width: 100px;">
        <path d="M 0 0 h 100
                 M 0 0 v 100
                 M 0 100 A 100 100 0 0 0 100 0 
                 "
              stroke="#fff" fill="transparent" />
    </svg>
</div>

#### 4、贝塞尔曲线命令

Q(x1 y1 x y) —— 二次贝塞尔曲线

C(x1 y1 x2 y2 x y) —— 三次贝塞尔曲线

```xml
<svg>
	<path d="M 0 0 Q 0 100 100 100
             M 100 100 C 200 0 300 100 400 0"
          stroke="#fff" fill="transparent" />
</svg>
```

<div style="display: flex; justify-content: center;">
    <svg style="height: 100px; width: 400px;">
        <path d="M 0 0 Q 0 100 100 100
                 M 100 100 C 200 0 300 100 400 0
                 "
              stroke="#fff" fill="transparent" />
    </svg>
</div>

### 四、SVG 文本

#### 1、<text> 和 <tspan> 创建文本

```xml
<text x="" y="" dx="" dy="">你好我是 Text 文本标签</text>
<!--
	dx、dy: 用于控制文本基线位置，值可以为一个，或者多个
		一个的时候，统一设置够所有文字
		多个的时候，从第一个文字开始依次设置
-->
例如：<text dx="10 20 30 40 50" dy="10 20 30 40 50">ABCDE</text>
```

<div style="display: flex; justify-content: center;">
    <svg style="height: 200px"><text dx="10 20 30 40 50" dy="10 20 30 40 50">ABCDE</text></svg>
</div>

2、垂直居中问题

3、<textPath> 让文本在指定路径上排列

4、<a> 插入超链接