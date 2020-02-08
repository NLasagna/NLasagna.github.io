---
title: 深色模式吗？
date: 2020-02-05 16:55:19
tags: 
	- tutorial
---

## 起

大概是从 2019 年开始，各大操作系统纷纷支持了深色模式（Dark Mode），自 iOS 13、Android 10 到 Windows、macOS（Catalina 支持了依靠日光时间来开关），都是在解决人机交互中长久以来的一个重要问题：白天屏幕全亮，模拟纸张，抵抗反光都很好，晚上就像举着照妖镜一般。除了与环境高对比度的自发光光源会对我们的眼睛造成伤害之外，这样的屏幕也逐渐和功耗与美学唱起了反调。于是有人说，来吧，我们用黑纸白字吧，按照这一面面「黑镜」的物理特性，早该这样了。所以早在系统们动手之前，很多人就开启了「反色模式」来做一定的替代。

这里又是那个老问题，深色模式不就是反个色吗？有什么难的？iPad 不就是个[大号的 iTouch](http://tech.sina.com.cn/n/2010-01-28/10401232617.shtml) 吗？有什么区别？<!-- more -->

不就是吗？就是吗？我在实际行动中思考了一下。

## 承

刚刚为整个站点部署完成了深色模式。脑海里虽然有要逐个颜色调整的概念（开玩笑说做好了「Jony Ive 附身的准备」），但是依然花费了六七个小时（不止）来实现。此文作为分享整个有趣的过程，比起作为实际的教程要名副其实，也重要的多。

之前使用了 [hexo-next-nightmode](https://github.com/1v9/hexo-next-nightmode) 插件，但后来发现本质其实很简单，用 CSS 里的 prefers-color-scheme 即可搞定，它可以对接并支援前面提到的所有现代操作系统的深色模式接口，随着你切换而改变，让网页和你的系统统一而行。

```css
/*深色模式*/
@media (prefers-color-scheme: dark) {
    body {
        color: #fff;
        background: #0c0c0c;
    }

    a {
        color: #8BB4F9;
    }
}
```

从我一个外行看来，这段代码对于普通人也是很友好的。即：

> 当你的媒介（media）在（at）深色（dark）偏好的颜色计划（prefers-color-scheme）时，把下面我提到的东西特别「处理」（即渲染）： 
>
> ​	把网页主体内容（body）的文字染成白色（RGB 颜色代码 #FFFFFF），背景（background）染成接近黑色（#0C0C0C）
>
> ​	把链接（a）染成这个色（#8BB4F9）
>
> 完事

看上去似乎逐个替换就好了。甚至网上有人基本完成，只要把代码整段复制下来就好了。

## 转

在 _layout.styl 里贴上代码，本地实验，一切看起来都好，但是经不住第二眼。

![截屏2020-02-04下午7.51.15](https://tva1.sinaimg.cn/large/006tNbRwgy1gbljy1ydi4j31780u0aeg.jpg)

### 1

首页 logo 在深色下显得很亮，失去了原先浅色时那种「不纯黑的黑」的感觉。这不难，只是因为黑色环境衬托而已。在深色下稍微降低明度，绝对颜色变了，但是回归了之前的感觉。

![图像 36](https://tva1.sinaimg.cn/large/006tNbRwgy1gbljy56wu5j30ty0m4dge.jpg)

### 2

第二个问题涉及了 personal 审美和取舍。我注意到，深色化之后的文字与链接密集混排时，显得过于「耿直」—— 说白了就是对比度过高。白色文字已经反差很强，加上为了表示链接的下划线，整体有些凌乱。

![图像 37](https://tva1.sinaimg.cn/large/006tNbRwgy1gbljy1dr8ej31uc0rcn85.jpg)

右边浅色界面显得不「耿直」的原因，是文字本身没有用纯黑色而是略灰（和 logo 想要表达的目的一样），而且即使用了，它也是自然地接近我们平时看到的书本纸张 —— 当然这也有人们不习惯黑底白字的惯性思维影响。我在盘算把文字向灰色调整的同时，也在考虑其他出路。因为一直没有找到合适的链接颜色，我想先尝试改变它看看。

我首先想到 iOS 13 更新的[人机界面指导方针的「色彩」](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/color/#dynamic-system-colors)一章提到一件很重要的事，即在黑白两种背景中，你使用的同一个颜色会出现「对比度和透明度」上的差异。方针建议开发者准备两套颜色以应对两种情况，并且提供了系统级的自适应颜色接口供使用。

![图像 35](https://i.imgur.com/3WQl1sM.jpg)可以看到黄色和蓝色笔触在两种背景下有不同的发色倾向。同时 iOS 备忘录使用的这种自适颜色机制也保证了观感上的统一。

所以我打算先把 systemBlue，也就是「iOS 蓝」应用到我的博客中。

<img src="https://i.imgur.com/sI6XRQ7.png" alt="截屏2020-02-05上午11.14.27"  style="display: inline-block" />


实际我并不满意。比起链接，它们每一个长得更像 iOS 中的按钮了，并且由于对比度并不够高，有碍观瞻。深色模式下，下划线依旧显得累赘；浅色模式反倒弄巧成拙，原本的下划线链接已经够直观和美观了。这时我想到了另一种颜色， Android 10 中深色模式的浅蓝：

<img src="https://i.imgur.com/anWS0F4.png" alt="Screenshot_20200205-111608" style="zoom: 25%;" />

这个颜色乍看并不感觉能和浅色模式里动人的「Android 蓝」呼应，反而让人感觉有些纯粹为了和深色背景提高对比度的工具性考量。但是既然是地球上仅有的几个设计优先些的大公司的选择，那么我也不不妨一试。

<img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gbljy3rnuxj311g0u0qcf.jpg" alt="截屏2020-02-03下午6.46.02" style="zoom: 33%;" />

我喜欢。在去掉了下划线后，整体观感我很满意。我认为它与浅色时整个站点的风格兼容性很高。很不错的链接色（；有点问题的系统按钮色）。

### 3

其实在翻阅各种设计指南时，维基百科[指导编纂的页面](https://zh.wikipedia.org/wiki/Help:链接颜色)里面有一句话很是受用：

> ……颜色可能看起来比相同文字的颜色更深；同样加大或加粗的文字看起来也会更深。

这很好理解，文字本质上就是其中混入了背景的色块，看起来自然会受到影响，但是要察觉这一点却不容易。一检查这里就有现成的例子：

![图像 38](https://tva1.sinaimg.cn/large/006tNbRwgy1gbljy5pgg6j318z0i1jt3.jpg)

本来在浅色下与引用文字协调的引用块头，在深色模式却显得过亮，过于凸显自己，改变了「引用」的含义。

改它。

<img src="https://tva1.sinaimg.cn/large/006tNbRwgy1gbljy47ba7j30jo0cywf9.jpg" alt="截屏2020-02-04下午5.03.24" style="zoom:50%;" />

这样协调多了。

其实最先解决的纯黑色背景的问题还没提到。有人说（搜索那篇文章中……）在 OLED 屏幕上完全关闭的像素启动时间很长，这样就会造成在纯黑色背景上移动的图像产生拖影。如果您使用的是 iPhone X 以后机型（除 iPhone XR 和 11 外）或是近两年的大部分 OLED 屏幕的 Android 手机，应该都能察觉到这个问题。

![ezgif-1-4a6a580724c5](https://i.imgur.com/5UAGPON.gif)

<center><a href="https://twitter.com/marcedwards/status/1053519077958803456">Marc Edwards（@marcedwards）在啁啾会馆的示例图片</a></center>

深灰色方框周围是已关闭的像素，移动拖沓，而里面浅色方框周围像素被深色方框提前「开机」了，移动就正常了。实际上在 LCD 屏幕上两个方框在同速移动。拖影问题是其一，其二是纯黑色造成的大反差太过突兀。因此我把背景颜色提亮了一点点，避免了这两个问题。



## 合

再进行了一些小修补后，本站 1.0 版本的深色模式就完工了。您可以通过 Android/iOS 以及 macOS/Windows 系统的深色模式开关切换来体验两者。

开头的问题，很显然，好的深色模式并不好做，甚至需要重新规划浅色的部分来调整。其意义也远不止于「注重外表美化」（我妈讲），而是通过修缮和增补让机器更适应人性和大自然的运作。对于未来人机更高效更舒适的互动，深色模式将是对人们重要到难以察觉，却无法离开的技术之一。

*（发稿时，国民聊天软件微信自 iOS 13 更新至今 139 天仍未适配深色模式，甚至八个月前在 WWDC 19， 苹果市场团队已经为微信设计好了[大概的模版](https://twitter.com/ilbkiki/status/1178319509725171712?s=20)。）*
<br>
### 附录：参考

[Colour – Visual design – iOS – Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/ios/visual-design/color/#dynamic-system-colors)

[帮助：链接颜色 - 维基百科](https://zh.wikipedia.org/wiki/Help:链接颜色)

[prefers-color-scheme - CSS: cascading style sheets](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)

[The Color System - Material Design](https://material.io/design/color/the-color-system.html#)

[让网页支持深色模式 | Vigorous Pro](https://www.wevg.org/archives/add-darkmode-support/)

