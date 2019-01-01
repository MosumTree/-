# CSS居中指南
关于CSS中的居中一直是被经常抱怨的子问题之一，为什么想实现一个居中有时候非常困难？其实重点不是居中本身实现起来难，而是我们需要考虑很多种情况下实现css居中的方法，所以有时候在不同的情况下不知道应该选择哪一种，所以在这里我们梳理一下。
<!-- TOC -->

- [CSS居中指南](#css居中指南)
    - [水平居中](#水平居中)
        - [内联元素](#内联元素)
        - [块级元素](#块级元素)
        - [多个块级元素](#多个块级元素)
            - [想让块级元素在同一行就得将其设置成inline-block，然后对父元素设为text-align,其实这个就和第一种相同了](#想让块级元素在同一行就得将其设置成inline-block，然后对父元素设为text-align其实这个就和第一种相同了)
            - [当然如果你会用flex布局，就可以更简单的实现，对父元素添加如下属性：](#当然如果你会用flex布局，就可以更简单的实现，对父元素添加如下属性：)
    - [垂直居中](#垂直居中)
        - [内联元素](#内联元素)
            - [内联元素内容只有一行](#内联元素内容只有一行)
            - [内联元素内容有多行](#内联元素内容有多行)
        - [块级元素](#块级元素)
            - [知道元素高度](#知道元素高度)
            - [不知道元素高度](#不知道元素高度)
            - [flex布局](#flex布局)
    - [水平垂直居中](#水平垂直居中)
        - [确定的宽高](#确定的宽高)
        - [宽高未知](#宽高未知)
        - [flex布局](#flex布局)
        - [grid布局](#grid布局)

<!-- /TOC -->
## 水平居中
### 内联元素
设置父元素text-align属性
```css
.center-children {
  text-align: center;
}
```
这个对inline, inline-block, inline-table, inline-flex属性都适用。
### 块级元素
想让一个块级元素居中，把它的margin置为如下值就可以了
```css
.center-me {
  margin: 0 auto;
}
```
### 多个块级元素
#### 想让块级元素在同一行就得将其设置成inline-block，然后对父元素设为text-align,其实这个就和第一种相同了
```css
.inline-block-center {
  text-align: center;
}
.inline-block-center div {
  display: inline-block;
  text-align: left;
}
```

#### 当然如果你会用flex布局，就可以更简单的实现，对父元素添加如下属性：
```css
.flex-center {
  display: flex;
  justify-content: center;
}
```
2.如果不需要同一行，统一让父元素下的块级元素添加margin属性：
```css
main div {
  margin: 0 auto;
}
```

## 垂直居中
垂直居中要比水平居中更麻烦一点。
### 内联元素
#### 内联元素内容只有一行
子元素容器设置上下相同的padding
```css
main a {
  background: black;
  color: white;
  padding: 40px 30px;
  text-decoration: none;
}
```
如果你的padding属性有其他用处，最好还是将容器的height和line-height属性置成相同的高度：
```css
.center-text-trick {
  height: 100px;
  line-height: 100px;
  white-space: nowrap;
}
```
#### 内联元素内容有多行
上下padding相同的方式有时候会有效；
同时如果是表单元素，<table>下的单元格内容是默认垂直居中的，当然我们也可以给其它类型的inline元素的父级这是display:table，给该内联元素设置display:table-cell;vertical-align:middle;来达到垂直居中的效果：
```html
<table>
  <tr>
    <td>
      I'm vertically centered multiple lines of text in a real table cell.
    </td>
  </tr>
</table>

<div class="center-table">
  <p>I'm vertically centered multiple lines of text in a CSS-created table layout.</p>
</div>
```
```css
body {
  background: #f06d06;
  font-size: 80%;
}

table {
  background: white;
  width: 240px;
  border-collapse: separate;
  margin: 20px;
  height: 250px;
}

table td {
  background: black;
  color: white;
  padding: 20px;
  border: 10px solid white;
  /* default is vertical-align: middle; */
}

.center-table {
  display: table;
  height: 250px;
  background: white;
  width: 240px;
  margin: 20px;
}
.center-table p {
  display: table-cell;
  margin: 0;
  background: black;
  color: white;
  padding: 20px;
  border: 10px solid white;
  vertical-align: middle;
}
```
垂直居中同样可以同flex布局解决，父级元素如下设置就可以了，详细的flex布局可以看我的另一篇博文（硬广一波）：
```css
.flex-center-vertically {
  display: flex;
  justify-content: center;
  flex-direction: column;
  height: 400px;
}
```
这里我们必须保证给容器一个确定的高，%,px等单位都可以。
如果前面两种方式都实现不了，我们可以使用"ghost element"，设置容器的position:relative;
```css
.ghost-center {
  position: relative;
}
.ghost-center::before {
  content: " ";
  display: inline-block;
  height: 100%;
  width: 1%;
  vertical-align: middle;
}
.ghost-center p {
  display: inline-block;
  vertical-align: middle;
}
```
### 块级元素
不了解网页布局的高度是很常见的，原因很多：如果宽度变化，文档流可以改变高度。文字样式的变化可以改变高度。文字数量的变化可以改变高度。具有固定长宽比的元素（如图像）可以在调整大小时改变高度，等等。
#### 知道元素高度
```css
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  height: 100px;
  margin-top: -50px; /* account for padding and border if not using box-sizing: border-box; */
}
```
#### 不知道元素高度
```css
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```
#### flex布局
```css
.parent {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
```
## 水平垂直居中
### 确定的宽高
```css
.parent {
  position: relative;
}

.child {
  width: 300px;
  height: 100px;
  padding: 20px;

  position: absolute;
  top: 50%;
  left: 50%;

  margin: -70px 0 0 -170px;
}
```
### 宽高未知
```css
.parent {
  position: relative;
}
.child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```
### flex布局
```css
.parent {
  display: flex;
  justify-content: center;
  align-items: center;
}
```
### grid布局
网格布局，这个平时不是太常用，有兴趣的可以研究一下。
```css
body, html {
  height: 100%;
  display: grid;
}
span { /* thing to center */
  margin: auto;
}
```
本文译自[Centering In CSS](https://css-tricks.com/centering-css-complete-guide/)

