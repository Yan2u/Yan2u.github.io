---
layout: article
title: Neumorphism UI： 新拟态设计
tags: 
- Web
- UI
mode: immersive
header:
  theme: dark
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: 'https://s2.ax1x.com/2019/04/06/AWRHC4.jpg'
---
<!--more-->

## 新拟态设计：Neumorphism UI

### Neumorphism UI

> 新拟态设计（Neumorphism UI）是 2020 年 UI 设计的主要趋势之一，你可以在 dribbble 上看到很多作品，新拟态是基于New+Skeuomorphism 英文单词的拼写。它是一种使用对象阴影的模糊、角度和强度来突显出对象的样式。由于其柔和的阴影和整体的外观，使该设计看起来更加的逼真、未来、现代、真实、有吸引力。

拟态，在[生物学](https://baike.baidu.com/item/拟态/472739)中指的是**一种生物模拟另一种生物或模拟环境中的其他物体从而获得好处的现象**，用在 UI 设计上，即是让 UI 元素模拟生活中的物体的形状与特征（就像桌面的垃圾桶图标那样），从而让 UI 元素具有生活中物体的层次感和辨识度

新拟态结合目前比较流行的扁平化设计和卡片式设计和拟态的设计风格，起源于一套在 dribbble 上走红的设计方案：

![pic0](http://image.woshipm.com/wp-files/2020/02/7xWL5aZvTPRPxHStcRP9.jpeg)

设计师 alexplyuto 发表了这套设计方案，获得数千点赞，之后类似风格的新拟态设计大量出现，可以说他的作品开创了 UI 设计的一个新趋势

个人感觉这套设计方案很有现代感，简洁的同时有富含层次感，可以感觉到每一个元素仿佛都是雕刻在了背景上



### Neumorphic UI & Modern UI

![pic1](http://image.woshipm.com/wp-files/2020/02/GbiMEQ69KwHRIxL9vFZC.jpeg)

上图体现了新拟态的卡片设计和传统的 Material 卡片设计的差别，其中 Material 的卡片阴影设计，让人感觉它是漂浮在空中，主要是在元素下方出现阴影，这样使得元素与背景之间产生一种空间纵深感，**而新拟态的卡片式设计通过2个正负阴影叠加，让卡片看起来更像是雕刻在了背景上，成为背景的一块突起**，但是两者在与背景颜色的对比上都不是很明显



### 只能用来设计卡片吗？

Neumorphic UI 并不仅限于卡片设计，只要把原来正负的阴影对调，很容易就可以实现一个按钮被点击的效果：

![pic3](http://image.woshipm.com/wp-files/2020/02/zOgX616cuHwLoWl7L5j4.jpeg)

但是这样会充分暴露出 Neumorphic UI 中元素和背景颜色对比度不足的问题，使得点击效果看起来不明显，UI 首先应确保易用性，因此可考虑以改用如下设计：

![pic4](http://image.woshipm.com/wp-files/2020/02/BBOUvTfvqWGcZs3tevhf.jpeg)



### 编程实现

Neumorphic UI 主要通过控件左上边缘的正阴影和右下边缘的负阴影实现，当然你也可以改变正负阴影的位置：

![pic4](http://image.woshipm.com/wp-files/2020/02/iVjcJsSflJkHLykgr07W.jpeg)

如果要设计一个按钮，在 hover 样式里，对调这两个阴影即可（或者加上 inset）

下面是一个例子：

```css
border-radius: 50px;
background: #ffffff;
box-shadow:  35px 35px 71px #d9d9d9, 
             -35px -35px 71px #ffffff;
```



### 总结

> 这一设计趋势的出现，无疑激发了许多设计师的灵感，与以前使用的卡片组件的可用性问题相比，它的问题其实并不是那么严重。
>
> 所以疯狂大胆的去尝试吧！顺应这一趋势，并对其进行调整，使它成为你自己的风格。UI设计师的工作就是在拖动方块，因此每次方块出现“差异”和“新奇”时，都会带来一些喜悦之感。如果没有这种不断的探索的精神，那么所有的产品看起来都是一毛一样。
>
> 让我们找点乐子！
>
> 但同时也要记住，每个新趋势都有一些潜在的陷阱，必须谨慎对待，才能让它得以使用。

Neumorphic UI 毕竟是新出现的设计风格，肯定还有不成熟的地方，但是它的简洁和层次感的结合使得整个界面非常具有现代感

另一方面，Neumorphic UI 的缺点其实也比较明显，例如：

- 色调单一，对视力低下、失明、色盲的用户来说，可辨识性较差
- 区分度较差，可以发现 Neumorphic UI 作为区分标志的只有阴影，因为它卡片的材质纹理和背景是一样的，如果失去了阴影效果，整个界面就会变成一片
- 突出的元素密集，Neumorphic UI 主要呈现元素的方式便是类似于突出的两个阴影，但若界面上元素密集，这样的突出效果会使得元素之间失去主次性，导致用户不能把注意集中到某个需要与之交互的元素上
- 造成一定的混乱，在 Neumorphic UI 设计下，被 Disable 的元素和被 Enable 的元素将不易于区分

对此，我的理解是，如果界面上的元素简洁大气，可以考虑采用这种设计方法，如果界面上元素密集丰富，则在采用之前需要优化或改进



### 样图

以下是采用 Neumorphic UI 设计的概念图：

> 个人简介页面 & 航班查询页面

![example0](https://image.uisdc.com/wp-content/uploads/2020/02/uisdc-hw-20200222-4.jpg)



>拟遥控器，这应该是最能体现 Neumorphic UI 设计风格的了，它的阴影效果好像就是在模仿遥控器按键的效果

![example1](https://image.uisdc.com/wp-content/uploads/2020/02/uisdc-hw-20200222-7.jpg)



>智能家居仪表盘

![example2](https://image.uisdc.com/wp-content/uploads/2020/02/uisdc-hw-20200222-3.jpeg)



> 智能家居仪表盘 2

![example3](https://image.uisdc.com/wp-content/uploads/2020/02/uisdc-hw-20200222-1.jpeg)



>智能家居仪表盘 3

![example4](https://image.uisdc.com/wp-content/uploads/2020/02/uisdc-hw-20200222-5.jpg)



> 拟播放器

![example 4](https://image.uisdc.com/wp-content/uploads/2020/02/uisdc-hw-20200222-6.jpg)



### 最后

白嫖了 Neumorphic UI 的一点点代码，我写了一个能在 QQ 音乐上搜歌的网页：[QQMusicSearcher](http://wuyanxi.top/QQMusicSearch.html)

个人感觉，Neumorphic UI 在简洁的场合下使用会有意想不到的效果，也希望这套设计方案能逐渐改进，走向成熟并流行起来



2020 - 03 - 17

感谢阅读~~

---

本文中部分内容摘取自：

1. [新拟态——国外设计师分析的全新UI趋势](http://www.woshipm.com/pd/3386232.html)
2. [为什么2020年初爆火的新拟物化设计，完全无法落地使用？](https://www.uisdc.com/neumorphism-ui)

---

