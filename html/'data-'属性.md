# HTML5的data-*自定义属性
HTML5增加了一项新功能是自定义数据属性，也就是data-*自定义属性。在HTML5中我们可以使用以data-为前缀来设置我们需要的自定义属性，来进行一些数据的存放。当然高级浏览器下可通过脚本进行定义和数据存取。在项目实践中非常有用。目前采取这样的做法的框架也有很多，最常见的当属jQueryMobile。
具体使用方法例下：
```html
<div id = "head" data-home = "http://blog.csdn.net/xmtblog" data-author = "伪专家"></div>  
```
在传统的做法中我们可以配合jquery使用，如下：
```javascript
$("#head").attr("data-home");  
$("#head").attr("data-home","new");  
```
或者纯js做法：
在IE浏览器里，我们通过获取对象后直接调用就可以了
```javascript
document.getElementById("head").["data-home"];  
document.getElementById("head").["data-home"] = "new";  
```
在火狐和谷歌浏览器里，我们可以通过getAttribute方法来实现调用：
```javascript
document.getElementById("head").getAttribute("data-home");  
document.getElementById("head").setAttribute("data-home","new"); 
``` 
在HTML5中的简洁操作方法：（dataset属性存取data-*自定义属性的值）
这种方式通过访问一个元素的 dataset 属性来存取 data-* 自定义属性的值。这个 dataset 属性是HTML5 JavaScript API的一部分，用来返回一个所有选择元素 data- 属性的DOMStringMap对象。
使用这种方法时，不是使用完整的属性名，如data-home来存取数据，应该去掉data-前缀。
还有一点特别注意的是：data-属性名如果包含了连字符，例如：data-date-of-birth ，连字符将被去掉，并转换为驼峰式的命名，前面的属性名转换后应该是：dateOfBirth。
```html
<div id = "head" data-home = "http://blog.csdn.net/xmtblog" data-author = "伪专家" data-date-of-birth>QQ群：135430763</div>  
<script type="text/javascript">  
    var el = document.querySelector('#head');  
    console.log(el.id);   
    console.log(el.dataset);//一个DOMStringMap  
    console.log(el.dataset.home);   
    console.log(el.dataset.author);   
    console.log(el.dataset.dateOfBirth);   
    el.dataset.dateOfBirth = '1985-01-05'; // 设置data-date-of-birth的值.  
    //判断属性  
    console.log('testAttr' in el.dataset);//false  
    el.dataset.testAttr = 'testAttr';  
    console.log('testAttr' in el.dataset);//true  
</script> 
``` 
如果你想删掉一个 data-属性 ，可以这么做： delete el.dataset.home ;  或者 el.dataset.home = null;。
这样操作起来是不是非常的方便。但有些浏览器可能还不支持。所以在此期间最好用的getAttribute和setAttribute来操作或配合jquery进行使用。
data-属性选择器
在实际开发时，可以根据自定义的data-属性选择相关的元素。例如使用querySelectorAll选择元素：
//选择所有包含'data-div'属性的元素
document.querySelectorAll ('[data-div]') ;
//选择所有包含'data-a-href' 属性值为red的元素
document.querySelectorAll ('[data-a-href="#"]') ;
同样的我们也可以通过data-属性值对相应的元素设置CSS样式，例如下面这个例子：
```html
<style type ="text/css">  
    .head {  
         width : 256px ;  
         height : 200px ;  
     }  
   
    .head[data-a='btn-a'] {  
         color : brown  
    }  
   
    .head[data-a='btn-color'] {  
         color : red  
    }  
</style>  
<div class = "head" data-qq = "QQ群：135430763" data-a = "btn-a" > button按钮 </div>  
<div class = "head" data-qq = "QQ群：135430763" data-a = "btn-color" > button按钮</div>
```