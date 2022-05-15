### 一、pointer-event: none

> 顾名思义，就是关闭元素的鼠标事件 —— 元素应用了该 CSS 属性 click hover move 等全部鼠标事件将无效，不触发。
>
> 例：一个阴影的 z-index 比较高，但是你不需要点击到阴影，而是要点击阴影下边的 Button，则可给阴影加上此属性，使之不触发事件，转而穿透给 层级更低的 button



### 二、clip-path

> 裁剪路径 —— 可能听名字不是那么易懂，那么我们一步一步往下看。()

#### 1、polygon() —— 多边形

##### Ⅰ、思考 —— 画三角形

> 我们来想一下，如何通过样式画一个 **三角形**

```scss
/* 你可能会想到 —— border */
.box {
    display: inline;
    
    border-top: 50px solid transparent;
    border-bottom: 50px solid transparent;
    border-left: 50px solid transparent;
    border-right: 50px solid green;
}

/* 或者 —— linear-gradient */
.box {
    width: 100px;
    height: 100px;
    
    background-image: linear-gradient(45deg, deeppink 50%, transparent 50%);
}

/* 还有 —— transform: rotate + overflow: hidden */
.main {
    position: relative;
    width: 100px;
    height: 100px;
    overflow: hidden;
    .box {
        position: absolute;
        left: 0;
        bottom: 0;
        width: 70%;
        height: 70%;
        background: red;
        transform-origin: left bottom;
        transform: rotate(45deg)
    }
}
```

##### Ⅱ、介绍 polygon

> 虽然方法很多，但是一个点很明显，可控性不够，有很强的局限性，但是现在，我们有弥补的办法了 clip-path: polygon() 

```scss
/*
	clip-path: polygon(x1 y1, x2 y2, x3 y3)
	不知道到这里能不能看明白：
	    x1 y1: 代表点一坐标
        x2 y2: 代表点二坐标
        x3 y3: 代表点三坐标
	当三个点连起来，的那块区域就是被裁剪的位置，元素将显示出被裁剪的位置
	到了这里是不是很简单易懂了~
*/

.box { 
    width: 200px;
  	height: 200px;
    background-color: red;
  	clip-path: polygon(0 0, 100% 0, 0 100%)
}
```

##### Ⅲ、扩展

> clip-path: polygo() 的参数并没有规定几个，所以你想要几个点就写出几个点的坐标来就好了，只要坐标够多，你拿这个画画都没问题，更别说 三角形 五边形六边形了。
>
> 是不是很像 PS 里面的钢笔工具~

#### 2、circle() —— 圆

```scss
/*
	两个可选参数
		1：圆的半径，默认元素宽高中短的那个为直径，支持百分比
		2：圆心的位置，默认为元素中心点
*/
.box {
    width: 200px;
  	height: 200px;
    background-color: red;
  	clip-path: circle(50px at 50px 50px)
}
```

#### 3、ellipse() —— 椭圆

```scss
/*
	三个可选参数
		1：椭圆的 x 轴半径，默认是宽度的一半，支持百分比
		2：椭圆的 y 轴半径，默认是高度的一半，支持百分比
		3、椭圆的中心位置，默认是元素的中心点
*/
.box {
    width: 200px;
    height: 200px;
    background-color: red;
    clip-path: ellipse(50% 50% at 50% 50%);
}
```



### 三、print-color-adjust

>  一个在打印时候可能会用到的属性。

> 默认值：economy 英文直译意思是“经济”，“节省”。表现为，浏览器（或其他客户端）对于元素进行样式上的调整，调整的规则由浏览器自己决定，以免达到更好的输出效果。
>
> 例如，当打印时，浏览器会选择省略所有背景图像，并调整文本颜色，以确保对比度对于白纸上的阅读是最佳的。

> exact则是“精确”，“准确”的意思。意思是告诉浏览器，我设置的这些颜色，背景啥的都是有必要的，精确匹配的，你不要自作聪明帮我做调整。



### 四、overscroll-behavior: contain

> 这个属性在我平常的工作上用得挺多的
>
> 作用是：让具有滚掉条的元素，滑到顶或滑到底后继续滑动，不会造成滚动穿透，导致它的父级以及往上有滚动条的元素滚动



### 五、word-break: keep-all 

> 控制文本换行，但不允许文本中的单词换行，只能在半角空格或连字符处换行。

