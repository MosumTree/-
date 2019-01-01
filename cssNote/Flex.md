# Flex布局
本来觉得阮一峰老师关于flex布局写的非常详细了，就像直接照搬过来作为转载，经过一些项目的练手，越发觉得flex布局相较于一些css样式操作的确是方便了许多，因此就就想再写一些自己的心得体会，更深入的了解一下CSS中的flex布局。
   <!-- TOC -->

- [Flex布局](#flex布局)
    - [基本情景](#基本情景)
    - [容器属性](#容器属性)
        - [1.flex-direction](#1flex-direction)
        - [2.flex-wrap](#2flex-wrap)
        - [3.flex-flow](#3flex-flow)
        - [4.justify-content](#4justify-content)
        - [5.align-items](#5align-items)
        - [6.align-content](#6align-content)
    - [成员属性](#成员属性)

<!-- /TOC -->
## 基本情景 
CSS的伸缩布局盒模型是经历过几次更新改版的，从最初的display:box到后面的display:flexbox再到现在的W3C标准display:flex,目的和形式是差不多的，所以这里只讨论一下最新的形式。首先看下图：
<html>
  <head>
    <style type="text/css">
      .container{
        height:210px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
      }
      .box1{
        height:40px;
        width:100px;
        background:#2578b5;
        margin:10px;
        text-align:center;
        line-height:40px;
        border-radius:5px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="box1">1</div>
      <div class="box1">2</div>
      <div class="box1">3</div>
      <div class="box1">4</div>
    </div>
  </body>
</html>


```html
<html>
  <head>
    <style type="text/css">
      .container{
        height:210px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
      }
      .box1{
        height:40px;
        width:100px;
        background:#2578b5;
        margin:10px;
        text-align:center;
        line-height:40px;
        border-radius:5px;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <div class="box1">1</div>
      <div class="box1">2</div>
      <div class="box1">3</div>
      <div class="box1">4</div>
    </div>
  </body>
</html>
```

不对布局进行任何修饰，仅仅美化一下图形，我们得到的大盒中的4个方块默认按一下顺序排列，因为div属于块级元素，独占一行，自然会折行。如果我们想要让他们横着排列呢？直观的想法就是对小方块设置float:left,就会达到如下效果：
<html>
  <head>
    <style type="text/css">
      .container2{
        height:110px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
      }
      .box2{
        height:40px;
        width:100px;
        background:#2578b5;
        margin:10px;
        text-align:center;
        line-height:40px;
        border-radius:5px;
        float:left;
      }
    </style>
  </head>
  <body>
    <div class="container2">
      <div class="box2">1</div>
      <div class="box2">2</div>
      <div class="box2">3</div>
      <div class="box2">4</div>
    </div>
  </body>
</html>
简单理解浮动就是按字面意思，按照值中的要求按方向方块向左边浮了上去，如果是右边自然就是下面这样：
<html>
  <head>
    <style type="text/css">
      .container3{
        height:110px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
      }
      .box3{
        height:40px;
        width:100px;
        background:#2578b5;
        margin:10px;
        text-align:center;
        line-height:40px;
        border-radius:5px;
        float:right;
      }
    </style>
  </head>
  <body>
    <div class="container3">
      <div class="box3">1</div>
      <div class="box3">2</div>
      <div class="box3">3</div>
      <div class="box3">4</div>
    </div>
  </body>
</html>

我们要说的是，这只是最简单的布局排版，我们利用flex不仅可以搭档这些效果，还可以达到更多复杂的效果。   
Flex的基础就是Flex布局是针对`容器`和`成员`的，就是图中的大盒子和小方块，容器包含一个`主轴`（横的）和一个`交叉轴`（竖的），成员默认按主轴排列。我们的Flex布局都是围绕这几个概念展开。我们要实现一个盒模型，首先就需要再容器中声明这是个盒子，里面的布局可以按照flex的规则来，所以就需要：


    .container3{
        height:110px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
        display:flex;
    }

## 容器属性
在container中声明了flex布局，就可以再container中给它赋予这些属性：

    flex-direction
    flex-wrap
    flex-flow
    justify-content
    align-items
    align-content
### 1.flex-direction
flex-direction属性决定主轴的方向（即项目的排列方向）。
```
row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。
```
用flex-direction属性就可以解决上面的布局问题,大家可以尝试一下其他方向。

<html>
  <head>
    <style type="text/css">
      .container4{
        height:110px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
        display:flex;
      }
      .box4{
        height:40px;
        width:100px;
        background:#2578b5;
        margin:10px;
        text-align:center;
        line-height:40px;
        border-radius:5px;
      }
    </style>
  </head>
  <body>
    <div class="container4">
      <div class="box4">1</div>
      <div class="box4">2</div>
      <div class="box4">3</div>
      <div class="box4">4</div>
    </div>
  </body>
</html>

### 2.flex-wrap
默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。
```
nowrap（默认）：不换行。
wrap：换行，第一行在上方。
wrap-reverse：换行，第一行在下方。
```
### 3.flex-flow
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
```css
.box {  
  flex-flow: <flex-direction> || <flex-wrap>;  
}  
```
### 4.justify-content
justify-content属性定义了项目在主轴上的对齐方式。
```
flex-start（默认值）：左对齐
flex-end：右对齐
center： 居中
space-between：两端对齐，项目之间的间隔都相等。
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
```
其中两端对其非常实用,很多应用的顶部栏都是3个元素按照如下排列：
<html>
  <head>
    <style type="text/css">
      .container5{
        height:110px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
        display:flex;
        justify-content:space-between;
      }
      .box5{
        height:40px;
        width:100px;
        background:#2578b5;
        margin:10px;
        text-align:center;
        line-height:40px;
        border-radius:5px;
      }
    </style>
  </head>
  <body>
    <div class="container5">
      <div class="box5">1</div>
      <div class="box5">2</div>
      <div class="box5">3</div>
    </div>
  </body>
</html>

### 5.align-items
align-items属性定义项目在交叉轴上如何对齐
```
flex-start：交叉轴的起点对齐。
flex-end：交叉轴的终点对齐。
center：交叉轴的中点对齐。
baseline: 项目的第一行文字的基线对齐。
stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
```
align-items的属性避免了我们设置高度和字行高相同实现居中带来的很多不可行的情况，也是非常实用。
<html>
  <head>
    <style type="text/css">
      .container6{
        height:110px;
        width:600px;
        background:#ddd;
        padding:1px;
        border-radius:10px;
        display:flex;
        justify-content:space-between;
        align-items:center;
      }
      .box6{
        height:40px;
        width:100px;
        background:#2578b5;
        margin:10px;
        text-align:center;
        line-height:40px;
        border-radius:5px;
      }
    </style>
  </head>
  <body>
    <div class="container6">
      <div class="box6">1</div>
      <div class="box6">2</div>
      <div class="box6">3</div>
    </div>
  </body>
</html>

### 6.align-content
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
```
flex-start：与交叉轴的起点对齐。
flex-end：与交叉轴的终点对齐。
center：与交叉轴的中点对齐。
space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
stretch（默认值）：轴线占满整个交叉轴。
```
## 成员属性
成员属性让我们能够在盒子成员遵循盒子布局的大方向时仍然可以‘搞特殊化’，
```
order
flex-grow
flex-shrink
flex-basis
flex
align-self
```

**order**属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。   

**flex-grow**属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

**flex-shrink**属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。
负值对该属性无效。
**align-self**属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

以上的属性都可以根据最初的代码进行简单的尝试，很快就能理解Flex布局的作用，当然还是阮一峰老师写得详细一些，本文主体知识内容
摘自<http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool>


