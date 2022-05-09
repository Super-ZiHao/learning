## 一、注释

> Less 支持标准的 CSS 多行注释 `/* */`，以及单行注释 `//`，前者会被完整输出到编译后的 CSS 文件中，而后者则不会。
## 二、变量

### 1.定义

> 变量以 @ 开头，赋值方法与 CSS 属性的写法一样

```less
@width: 1600px;
@pen-size: 3em;
```

### 2.使用

> 直接使用变量的名称即可调用变量

```scss
#app {
  height: @width;
  font-size: @pen-size;
}
```

### 3.作用域

> 变量支持块级作用域，嵌套规则内定义的变量只能在嵌套规则内使用（局部变量）

```less
#foo {
  @width: 5em;
  width: @width;
}

#bar {
  width: @width;
}
```

编译后：

```css
#foo {
  width: 5em;
}

#bar { /* 报错 */
}
```

---

