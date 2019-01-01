# swiper使用指南
## 使用场景
首先我们就要知道swiper这个东西能帮我们解决什么以至于我们要去学习使用它，这是我们学习的动力。大致介绍一下场景：

    1.头部的广告自动轮播效果；
    2.移动端网页粘附式滚动效果；
    3.简单的画廊。
这些都可以通过swiper轻松实现，所以本片的目的就是在学习swiper的基础上实现这几个效果！
## 基本用法
Swiper是纯javascript打造的滑动特效插件，面向手机、平板电脑等移动终端。
Swiper能实现触屏焦点图、触屏Tab切换、触屏多图切换等常用效果。
Swiper开源、免费、稳定、使用简单、功能强大，是架构移动终端网站的重要选择！
以上是swiper中文网首页的介绍，就是这么牛逼轰轰。     
第一步：要使用swiper就需要加载swiper的js和css文件：swiper.min.js和swiper.min.css文件。
```html
<!DOCTYPE html>
<html>
<head>
    ...
    <link rel="stylesheet" href="path/to/swiper.min.css">
</head>
<body>
    ...
    <script src="path/to/swiper.min.js"></script>
</body>
</html>
```
第二步：按照下面的结构使用swiper.min.css中的样式装饰你的div：
```html
<div class="swiper-container">
    <div class="swiper-wrapper">
        <div class="swiper-slide">Slide 1</div>
        <div class="swiper-slide">Slide 2</div>
        <div class="swiper-slide">Slide 3</div>
    </div>
    <!-- 如果需要分页器 -->
    <div class="swiper-pagination"></div>
    
    <!-- 如果需要导航按钮 -->
    <div class="swiper-button-prev"></div>
    <div class="swiper-button-next"></div>
    
    <!-- 如果需要滚动条 -->
    <div class="swiper-scrollbar"></div>
</div>
<!-- 导航等组件可以放在container之外 -->
```
第三步：初始化Swiper：写在html内容后面或者是等页面加载完后初始化：
```javascript
//第一种方式
<script>        
  var mySwiper = new Swiper ('.swiper-container', {
    direction: 'vertical',
    loop: true,
    
    // 如果需要分页器
    pagination: '.swiper-pagination',
    
    // 如果需要前进后退按钮
    nextButton: '.swiper-button-next',
    prevButton: '.swiper-button-prev',
    
    // 如果需要滚动条
    scrollbar: '.swiper-scrollbar',
  })        
</script>
</body>

//第二种方式
<script type="text/javascript">
window.onload = function() {
  ...
}
</script>
```

## 应用1：广播自动轮播
我们遵照上面的方法可以快速地实现一个广告轮播地效果：
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>SwiperDemo</title>
    <link rel="stylesheet" href="./swiper-3.4.2.min.css">
    <style type="text/css">
        html,body{
            height: 100%;
            width: 100%;
            overflow: hidden;
            margin: 0;
            padding: 0;
        }
        #ad_container{
            height: 100px;
            width: 100%;
            background: #666;
        }
        #ad1{
            background:#4390ee;
        }
        #ad2{
            background:#ca4040;
        }
        #ad3{
            background:#ff8604;
        }
        .swiper-slide{
            height: 100px;
            line-height: 100px;
            text-align: center;
            color: #fff;
            font-size: 20px;
        }
    </style>
</head>

<body>
    <div id="demo">
        <div id="ad_container" class="swiper-container">
            <div class="swiper-wrapper">
                <div id="ad1" class="swiper-slide">Slide 1</div>
                <div id="ad2" class="swiper-slide">Slide 2</div>
                <div id="ad3" class="swiper-slide">Slide 3</div>
            </div>
        </div>
    </div>
    <script src="./swiper-3.4.2.min.js"></script>
    <script>        
  var mySwiper = new Swiper ('.swiper-container', {
    direction: 'horizontal',
    autoplay: 1000
  })        
</script>
</body>

</html>
```
想要设置广告自动切换，swiper切换等样式，就要通过在Swiper对象实例的参数上来做文章：
```
initialSlide:0
direction:horizontal
speed:300
autoplay:0
autoplayDisableOnInteraction:true
autoplayStopOnLast:false
grabCursor:false
parallax:false
hashnav:false
hashnavWatchState:false
history: replaceState:false
setWrapperSize:false
virtualTranslate:false
a11y:false
width:
height:
roundLengths:false
breakpoints:
autoHeight:false
nested:false
```
这些属性不做细讲，自己去试。在每个swiper-slide中插入你想要的广告图片或者是设置div的背景都可以实现广告效果。

## 应用2：粘附式滚动效果
干脆在原来的基础上做吧，请把网页调整移动式，效果好一些。这样的话我们就把轮播广告作为我们这个网页第一页的子页面，这就要用到上面nested的属性了。
```html
<body>
    <div id="demo">
        <div id="page_container" class="swiper-container">
            <div class="swiper-wrapper">
                <div id="page1" class="swiper-slide">
                    <div id="ad_container" class="swiper-container">
                        <div class="swiper-wrapper">
                            <div id="ad1" class="swiper-slide">Slide 1</div>
                            <div id="ad2" class="swiper-slide">Slide 2</div>
                            <div id="ad3" class="swiper-slide">Slide 3</div>
                        </div>
                    </div>
                </div>
                <div id="page2" class="swiper-slide"></div>
                <div id="page3" class="swiper-slide"></div>
            </div>
            
        </div>
    </div>
    <script src="./swiper-3.4.2.min.js"></script>
    <script>        
  var mySwiper = new Swiper ('#ad_container', {
    direction: 'horizontal',
    autoplay: 1000,
    nested:true
  });
  var mySwiper2 = new Swiper ('#page_container', {
    direction: 'vertical'
    
  });          
</script>
</body>
```
样式就不写了，主要还是看一下这个html结构，这就是嵌套最简单直观的结构了。

## 应用3：画廊
其实画廊也没啥做的必要了，就是在给应用2加一个子页面，添加一下画廊的控件来控制一下照片的切换
```html
<body>
    <div id="demo">
        <div id="page_container" class="swiper-container">
            <div class="swiper-wrapper">
                <div id="page1" class="swiper-slide">
                    <div id="ad_container" class="swiper-container">
                        <div class="swiper-wrapper">
                            <div id="ad1" class="swiper-slide">Slide 1</div>
                            <div id="ad2" class="swiper-slide">Slide 2</div>
                            <div id="ad3" class="swiper-slide">Slide 3</div>
                        </div>
                    </div>
                </div>
                <div id="page2" class="swiper-slide"></div>
                <div id="page3" class="swiper-slide">
                    <div id="photo_container" class="swiper-container">
                        <div class="swiper-wrapper">
                            <div id="photo1" class="swiper-slide">Photo 1</div>
                            <div id="photo2" class="swiper-slide">Photo 2</div>
                            <div id="photo3" class="swiper-slide">Photo 3</div>
                        </div>
                    </div>
                    <div class="swiper-pagination"></div>
                </div>
            </div>
            
        </div>
    </div>
    <script src="./swiper-3.4.2.min.js"></script>
    <script>        
  var mySwiper = new Swiper ('#ad_container', {
    direction: 'horizontal',
    autoplay: 1000,
    nested:true
  });
  var mySwiper2 = new Swiper ('#page_container', {
    direction: 'vertical'
    
  });
  var mySwiper3 = new Swiper ('#photo_container', {
    direction: 'horizontal',
    nested:true,
    pagination: '.swiper-pagination',
    paginationClickable: true
  });            
</script>
</body>
```
想实现更多的效果，自己去查Swiper中文网的API,参见[Swiper中文网](http://www.swiper.com.cn/)，我写了一下就发现这个插件还是很容易上手的，但是当你真正在工作中遇到的话，会发现里面有很多的坑，所以在学校装装逼，平时玩玩可以拿过来用，没吃透这个插件的兼容性即一系列的坑，紧急的项目还是别用了，别问我怎么知道的。