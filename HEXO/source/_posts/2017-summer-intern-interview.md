---
title: 2017暑期前端实习面经总结
date: 2017-08-23 17:17:42
tags: [前端, 面试]
---
# 周锐JD
## 写出块级元素、行内元素 
块级元素：div, p, form, ul, li, ol, dl, form, address, fieldset, hr, menu, table
行内元素：span, strong, em, br, img, input, label, select, textarea, cite
*注意：`img`标签是一种特殊的可以设置宽和高的行内元素*

## 布局
布局有table布局，盒子布局，flex布局（弹性布局），栅格布局。
**flex布局**
学习flex布局可以通过玩这个小游戏：[FLEXBOX FROGGY](http://flexboxfroggy.com/#zh-cn)
<!--more-->

## position有哪些
* static(静态)： 没有特别的设定，遵循基本的定位规定，不能通过z-index进行层次分级。
* relative(相对定位)： 对象不可层叠、不脱离文档流，参考自身静态位置通过 top,bottom,left,right 定位，并且可以通过z-index进行层次分级。
* absolute(绝对定位)： 脱离文档流，通过 top,bottom,left,right 定位。选取其最近一个最有定位设置的父级对象进行绝对定位，如果对象的父级没有设置定位属性，absolute元素将以body坐标原点进行定位，可以通过z-index进行层次分级。
* fixed（固定定位）： 这里所固定的参照对像是可视窗口而并非是body或是父级元素。可通过z-index进行层次分级。（父元素为可视化窗口的absolute定位）
## icon css spirites
　　CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的"background-image"，"background- repeat"，"background-position"的组合进行背景定位，background-position可以用数字精确的定位出背景图片的位置。
　　在网页访问中，客户端每需要访问一张图片都会向服务器发送请求，所以，访问的图片数量越多，请求次数也就越多，造成延迟的可能性也就越大。所以，CSS Sprites技术加速的关键，并不是降低质量，而是减少请求次数，从而提高网页的加载速度。

## 数组去重
```
/*1.最基础的方法*/
var res = [];
for(var i=0; i<arr.length; i++){
    if(res.indexOf(arr[i])!=-1){
        res.push(arr[i]);
    }
}
return res;

/*2.如果对数组顺序没有要求，得到改进方法（先排序，不用indexOf）*/
var res = [];
arr.sort();
for(var i=0; i<arr.length; i++){
    if(arr[i] != res[res.length-1]){
        res.push(arr[i]);
    }
}
return res;

/*3.时间最优方法（创建hash表，牺牲空间为代价）*/
var res = [];
var hash = [];
for(var i=0; i<arr.length; i++){
    if(!hash[arr[i]]){
        res.push(arr[i]);
        hash[arr[i]] = true;
    }
}
return res;
```

## js跨域通信
见自己的博客 [前端跨域简单理解](http://blog.csdn.net/hdr01/article/details/70141120)
我的收藏 [前端解决跨域问题的8种方案（最新最全）](http://blog.csdn.net/joyhen/article/details/21631833)

## js有哪些兼容性问题
- HTML对象获取问题
FireFox：`document.getElementById("idName")`
ie:`document.idname`或者`document.getElementById("idName")`
解决办法：统一使用`document.getElementById("idName")`

- window.location.href问题
说明:IE或者Firefox2.0.x下,可以使用`window.location`或`window.location.href`
Firefox1.5.x下,只能使用`window.location`
解决方法：使用`window.location`来代替`window.location.href`

- firefox与IE的父元素(parentElement)的区别
IE：`obj.parentElement`
firefox：`obj.parentNode`
解决方法: 因为firefox与IE都支持DOM,因此使用`obj.parentNode`是不错选择.

- event.srcElement问题
问题说明：IE下，`event`对象有`srcElement`属性，但是没有`target`属性；Firefox下，`event`对象有`target`属性，但是没有`srcElement`属性。
解决方法：使用`srcObj = event.srcElement ? event.srcElement : event.target;`

---

# 天丽美团
## 让div垂直水平居中
- **水平居中**
实现起来很简单，直接用margin：0 auto就能完成
```
.mydiv{   
    margin:0 auto;   
    width:300px;   
    height:200px;   
} 
```

- **水平垂直居中**
1. 知道DIV的宽和高
用绝对定位，设置top和left分别为50%，然后将margin的左边和上面分别设置宽高的一半的负数。
```
.mydiv{ 
   width:300px;  
   height:200px;  
   position:absolute;  
   left:50%;  
   top:50%;  
   margin:-100px 0 0 -150px 
}
```
2. 用CSS3中的transform（IE8以上支持）
```
.father{
    position:relative;
}
.son{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
```
3. 用CSS3中的flex布局（IE8以上支持）
```
.vertical-container{
    display: flex;
    align-items: center;
    justify-content: center;
}
```

## 三个div，上下div固定，中间div高度自适应
```
<style>
    html, body{
      height: 100%;
      overflow: hidden;
    }
    .top{
      position: absolute;
      top: 0;
      height: 50px;
      width: 100%;
      background-color: black;
    }
    .bottom{
      position: absolute;
      bottom: 0;
      height: 50px;
      width: 100%;
      background-color: yellow;
    }
    .middle{
      position: absolute;
      top: 50px;
      bottom: 50px;
      height: 100%;
      width: 100%;
      background-color: red;
    }
  </style>
```

## "www.abc.html?a=1&b=jq"中如何得到a和b的值
- 获取url?后的值，利用split('&')将值转换成数组遍历
```
//sArgName表示要获取哪个参数的值 
function GetArgsFromHref(sArgName) 
{ 
    var sHref = window.location.href;
    alert(sHref); 
    var args = sHref.split("?"); 
    var retval = ""; 
    if(args[0] == sHref) /*参数为空*/ 
　　{ 
        return retval; /*无需做任何处理*/ 
    } 
    var str = args[1]; 
    args = str.split("&"); 
    for(var i = 0; i < args.length; i++ ) 
    { 
        str = args[i]; 
        var arg = str.split("="); 
        if(arg.length <= 1) continue; 
        if(arg[0] == sArgName) retval = arg[1]; 
    } 
    //return retval; 
    alert(retval); 
} 
```
- 正则匹配
```
function GetQueryString(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)","i");
    var r = window.location.search.substr(1).match(reg);
    if (r!=null) return (r[2]); return null;
}
alert(GetQueryString("参数名"));
```
- **红宝书上解决办法（比第一种好）**
`location.search` 返回的是url的查询字符串，这个字符串以问号开头。
```
function getQueryStringArgs(){
    //取得查询字符串并去掉开头的问号
    var qs = (location.search.length>0) ? location.search.substring(1) : "");
    //保存数据的对象
    var arg2 = {};
    //取得每一项
    var items = qs.length ? qs.split("&") : [];
    var item=null, name=null, value=null;

    for(var i=0;i<items.length;i++){
        item = items[i].split("=");
        name = decodeURIComponent(item[0]);
        value = decodeURIComponent(item[1]);

        if(name.length) args[name]=value;
    }
    return args;
}
```

## 一个页面www.tao.com/a.html里面有个iframe，这个iframe的src可不可以是www.bai.com/b.html
可以，跨域问题，当主域名不同时，可以用window.name，location.hash等办法

见自己的博客 [前端跨域简单理解](http://blog.csdn.net/hdr01/article/details/70141120)
我的收藏 [前端解决跨域问题的8种方案（最新最全）](http://blog.csdn.net/joyhen/article/details/21631833)

## http请求过程，为什么要建立tcp连接，为什么不能是udp连接
大致过程：
域名解析 --> 发起TCP的3次握手 --> 建立TCP连接后发起http请求 --> 服务器响应http请求，浏览器得到html代码 --> 浏览器解析html代码，并请求html代码中的资源（如js、css、图片等） --> 浏览器对页面进行渲染呈现给用户
![TCP三次握手](http://img.blog.csdn.net/20170104214009596?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2h1c2xlaQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
HTTP使用TCP而不是UDP的原因在于（打开）一个网页必须传送很多数据，而TCP协议是可靠的传输协议，提供传输控制，按顺序组织数据，和错误纠正。TCP发送连接请求不成功就重传，这样的话如果不超时总能保证连接请求被服务器接收，并且不会丢包保证传输无错误。

---

# 焦焦JD
## 事件捕获冒泡
- 事件分为三个阶段：事件捕获 -->  事件目标 -->  事件冒泡（DOM中的事件流）
- 事件捕获：事件发生时（`onclick`,`onmouseover`）首先发生在`document`上，然后依次传递给`body`、`div`；最后到达目的节点（即事件目标）。
- 事件冒泡：事件到达事件目标之后不会结束，会逐层向上冒泡，直至`document`对象，跟事件捕获相反。
- 事件委托：利用事件冒泡的特性，将里层的事件委托给外层事件，根据`event`对象的属性进行事件委托，改善性能。
使用事件委托能够避免对特定的每个节点添加事件监听器；事件监听器是被添加到它们的父元素上。事件监听器会分析从子元素冒泡上来的事件，找到是哪个子元素的事件。
- 事件冒泡、事件捕获阻止：
```
event.stopPropagation( );   // 阻止事件的进一步传播，包括（冒泡，捕获），无参数
e.preventDefault( );        // 阻止事件默认行为。
return false;               // 相当于同时调用e.preventDefault()和e.stopPropagation()
event.cancelBubble = true;  // true 为阻止冒泡（IE下）
```
- 程序员可以自己选择绑定事件时采用事件捕获还是事件冒泡，方法就是绑定事件时通过addEventListener函数，它有三个参数，第三个参数若是true，则表示采用事件捕获，若是false，则表示采用事件冒泡。
支持W3C标准的浏览器在添加事件时用addEventListener(event,fn,useCapture)方法，基中第3个参数useCapture是一个Boolean值，用来设置事件是在事件捕获时执行，还是事件冒泡时执行。而不兼容W3C的浏览器(IE)用attachEvent()方法，此方法没有相关设置，不过IE的事件模型默认是在事件冒泡时执行的，也就是在useCapture等于false的时候执行，所以把在处理事件时把useCapture设置为false是比较安全，也实现兼容浏览器的效果。

## JS数据类型
`String`、`Number`、`Boolean`、`Null`、`Undefined`、`Object`
typeof返回的是字符串有六种可能:`number`、`string`、`boolean`、`object`、`function`、`undefined`

---

# 周锐头条
## 解释一下作用域链、闭包
作用域链：当在函数里找不到某一变量时，会在其父作用域上找该变量有没有声明的值，直到最后都找不到的话输出`undefined`。
闭包：在一个函数里面嵌套另一个函数，内部的函数能够访问到外部函数的变量，这种形式叫闭包。 

## 变量提升题
```
  var a = 1;
  function x(){
    console.log(a);
    var a = 2;
    console.log(a);
  }
  x();
```
输出是undefined，2。因为在函数内有自己的作用域，x函数中定义了a的值，所以不会取到全局变量a=1的值，但是在函数中由于变量声明会提升，所以会输出undefined，2。

## 作用域题
```
var a = 1;
if(true){
   var a =2;
}
console.log(a);
```
输出2。因为在JS里是没有块级作用域的，在if中赋值a=2之后，在循环外a依然等于2。

## 列举你所知道的数组常用方法
1. join()
2. reverse()
3. sort()
4. concat()
5. slice()
6. splice()
7. push() pop() unshift() shift()

## 你知道哪些BOM对象
`window`，`location`，`navigator`，`history`，`screen`

## offsetwidth、scrollwidth、clientwidth的区别
- `scrollWidth`：对象的实际内容的宽度，不包边线宽度，会随对象中内容超过可视区后而变大。 
- `clientWidth`：对象内容的可视区的宽度，不包滚动条等边线，会随对象显示大小的变化而改变。 
- `offsetWidth`：对象整体的实际宽度，包滚动条等边线，会随对象显示大小的变化而改变。
![](http://files.jb51.net/file_images/article/201501/2015011314321833.png)
![](http://files.jb51.net/file_images/article/201501/2015011314321834.png)


## target和currentTarget的区别
event.currentTarget指向事件所绑定的元素，而event.target始终指向事件发生时的元素。

## js如何获取客户使用浏览器、终端、平台信息
`navigator.userAgent`

## 箭头函数的this
```
var obj={
  a:1,
  b:()=>{console.log(this.a)}
}
obj.b();    // 输出1。
```
- 普通函数中的`this`
1. `this`总是代表它的直接调用者, 例如 `obj.func` ,那么`func`中的`this`就是`obj`
2. 在默认情况(非严格模式下,未使用 `'use strict'`),没找到直接调用者,则this指的是 `window`
3. 在严格模式下,没有直接调用者的函数中的`this`是 `undefined`
4. 使用`call`,`apply`,`bind`(ES5新增)绑定的,`this`指的是 绑定的对象
- 箭头函数中的`this`
默认指向在定义它时,它所处的对象,而不是执行时的对象, 定义它的时候,可能环境是`window`

## BFC相关知识
父元素与子元素同时设置`margin-top`是怎样的效果（父子之间无间距，对外部`margin`取父子`margin-top`较大值。）
父元素不设置、子元素设置是怎样的效果（父子无间距，对外部取子元素`margin`值）
子元素不设置、父元素设置是怎样的效果（父子无间距，对外部取父元素`margin`值）
如何实现仅有子元素`margin-top`生效（父元素设置`overflow：hidden`最佳，也可以`padding-top:1px`）。
 
## 伪类选择器
```
<div>
      <p>第一个子元素</p >
      <h1>第二个子元素</h1>
      <span>第三个子元素</span>
      <span>第四个子元素</span>
</div>

<style>
span:first-child{
    background:yellow;
}
 
span:first-of-type{
    background:yellow;
}
</style>
```
哪个css生效么？为什么？（`last-child` 和 `last-of-type`；`nth-child（n）`和`nth-of-type（n）`）
你还知道哪些伪类选择器。
`p:first-child`  匹配到的是p元素,因为p元素是div的第一个子元素；
`h1:first-child`  匹配不到任何元素，因为在这里h1是div的第二个子元素，而不是第一个；
`span:first-child`  匹配不到任何元素，因为在这里两个span元素都不是div的第一个子元素；

`p:first-of-type`  匹配到的是p元素,因为p是div的所有类型为p的子元素中的第一个；
`h1:first-of-type ` 匹配到的是h1元素，因为h1是div的所有类型为h1的子元素中的第一个；
`span:first-of-type`  匹配到的是第三个子元素span。这里div有两个为span的子元素，匹配到的是它们中的第一个。

其他伪类还有 `:focus`, `:active`, `:hover`, `:visited`

## 用纯css实现一个宽度为屏幕50%，水平垂直居中的自适应正方形
```
.middle{
      background: red;
      width: 50%;
      padding-bottom: 50%;
      height: 0;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%,-50%);
}
```
padding是根据父元素的宽度来计算的，这个例子中，父元素为body，刚好是正方形。
 
## 数组去重
```
var ans = (...new Set(arr));
```
## 统计一个字符串中出现最多的字母及其出现次数
`hash`
## A为无序、不重复数组，在其中选出M个数，使其和为N
