## 2 0 2 2 ：

### 4-08、:root 是什么？

> :root 相当于 html，但是权级要比 html 高

```css
:root {
    color: red  /* 生效 */
}
html {
    color: blue /* 不生效 */
}
```



### 4-11、a 的 margin-bottom 和 b 的 margin-top 的值重叠了。如何解决？

> 块级元素的上边距与下边距有时候会合并为单哥外边距，这种现象称为 margin 合并

```html
/* 1、浮动 */
/* 2、定位(absolute | fixed) */
/* 3、修改 dom 结构 */
例:
<div class="top" style="margin-bottom: 20px;"></div>
<div class="box">
	<div class="bottom" style="margin-top: 20px;"></div>
</div>
```



### 4-13、从一个没有滚动条的页面切换到一个有滚动条的页面会发生抖动？

> 因为滚动条占有一部分宽度，从没有到出现就会造成此现象

```css
/* 1、浏览器一直显示滚动条 —— 不美观 */
body { overflow: scroll }
/* 2、滚动条宽度不参与计算 —— 属性不兼容 火狐 IE */
body { overflow: overlay }
/* 3、滚动条宽度设为 0 —— 属性不兼容 火狐 IE */
::-webkit-scrollbar{ width: 0px }
/* 4、计算出滚动条的宽度，并特殊处理 */
body { margin-left: calc(100vw - 100%) } /* 或 */ body { padding-left: calc(100vw - 100%) }
```



### 4-15、什么是重排？重绘？

> 重排——当你改变宽高的时候，浏览器需要重新计算现在的宽高，同样其他元素的位置也会因为现在的宽高收到影响，浏览器渲染的时候会有部分失效，然后重新渲染，这个过程就是重排

> 重绘——完成重排之后，浏览器重新渲染后展示新的页面到屏幕上，这个过程我们称为重绘

> 建议——当我们改变大小的时候，会产生重排，给dom设置颜色的时候，会导致重绘，重排一定会重绘，单重绘不会重排，重排会影响性能，所以尽可能减少重排的操作。

### 4-18、用 display: flex align-items: center 之后发现字体没有垂直居中?

> 产生原因——字体的 line-height 不是默认值，影响到了排列

```css
/* 解决办法: 单独给字体设置 */
.text {
    line-height: normal; 
}
```



### 4-19、回过头复习一下样式的复合写法？

```css
html {
    /* 字体属性 */
    font：font-style font-weight font-size/line-height font-family;
    
    /* 背景图片 */
    background: black url(“images/logo.jpg”) no-repeat fixed center top;
    
    /* 边框 */
    border:5px solid red;
    
    /* margin Or padding */
    margin: 1px;	 
    margin: 1px 2px;	/* 上下1px 左右2px */
    margin: 1px 2px 3px;	/* 上1px 左右2px 下3px */
    margin: 1px 2px 3px 4px;	/* 上1px 右2px 下3px 左4px */
}
```



### 5-07、vmax 和 vmin 是什么？

> vmax——一个单位，值是视口宽度和高度中最大的那个
>
> v-min——与 vmax 相反

```css
html {
    font-size: 1vmax;
}
/* 当宽度比高度要大——例如 Pc 端屏幕，此时的 1vmax === 1vw */
/* 当宽度比高度要小——例如 手机 端屏幕，此时的 1vmax === 1vh */
/* vmin相反就不做多例子了 */
```