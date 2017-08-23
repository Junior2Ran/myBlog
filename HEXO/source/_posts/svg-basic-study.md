---
title: SVG动画基础学习
date: 2017-08-29 17:52:02
tags: [svg, 前端]
---
最近看了[文龙的博客](http://www.zhuwenlong.com)，他的主页有几个线条动画构成的 "I AM MOFEI" 字样，我觉得特别好玩，起初我以为是用canvas画的，但是也没想明白这么复杂的线条路程应该怎么画。后来，他告诉我用SVG动画来做的，这就简单的在网上找了一下SVG的动画姿势，整理一下。
未完待续！！
<!--more--> 

# SVG基础形状
SVG 有一些预定义的形状元素，可被开发者使用和操作：
* 矩形 `<rect>`
* 圆形 `<circle>`
* 椭圆 `<ellipse>`
* 线 `<line>`
* 折线 `<polyline>`
* 多边形 `<polygon>`
* 路径 `<path>`

这些基础的我们可以自己查一查资料就能立马上手了，所以这里不会过多的去记录这些知识。今天重点来学习一下要如何让SVG动起来~<i class="em em-horse"></i>

# SVG动画元素
SVG动画有5个标签能实现，他们分别是：
1. `<set>`
2. `<animate>`
3. `<animateColor>`
4. `<animateTransform>`
5. `<animateMotion>`

顾名思义，这5个元素和CSS3动画类比一下，从名字看就能大概知道分别有什么功能。比如`<animate>`元素实现单属性的动画过渡效果，`<animateColor>`元素控制动画效果,不过此属性已经被废弃了<i class="em em-cry"></i>，`<animateTransform>`元素的功能和CSS3中的transform变换一脉相承，自己体会便好，`<animateMotion>`元素可以让SVG各种图形沿着特定的`<path>`路径运动~多帅哦！

# 动画属性

# viewBox属性

`<svg width="500" height="300"></svg>`
有关viewBox属性问题的可以去看张鑫旭写的这篇文章，讲的更加详细：
[理解SVG viewport,viewBox,preserveAspectRatio缩放 by 张鑫旭](http://www.zhangxinxu.com/wordpress/2014/08/svg-viewport-viewbox-preserveaspectratio/)

# 学习资料
- [超级强大的SVG SMIL animation动画详解 by 张鑫旭](http://www.zhangxinxu.com/wordpress/2014/08/so-powerful-svg-smil-animation/)
- [【Web动画】SVG 线条动画入门 by ChokCoco](http://www.cnblogs.com/coco1s/p/6225973.html)
- [【Web动画】SVG 实现复杂线条动画 by ChokCoco](http://www.cnblogs.com/coco1s/p/6230165.html)
- [理解SVG viewport,viewBox,preserveAspectRatio缩放 by 张鑫旭](http://www.zhangxinxu.com/wordpress/2014/08/svg-viewport-viewbox-preserveaspectratio/)
