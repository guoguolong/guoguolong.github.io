---
title: 程序员入行之素养(四)：好记性不如烂笔头(怎样记读书笔记)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-12 10:00:00
---

○ 需要记读书笔记吗？  
○ 电子的还是纸质？  
○ 易于创作、易于传播！  
○ 在哪里创作？  

**能用纯文本写的知识，绝不用Word来写！**  

这句话的涵义在于：**知识应易于创作**，纯文本就是用键盘码出来的字。一个轻巧的文本编辑器就可以书写；如果用Word，你很可能纠缠于各种文本格式调整，甚至心中暗暗得意呢。但此时你已经偏离**写作**很远了；

**能用HTML(网页)传播的知识，绝不用其他途径！**  

这句话的涵义在于：**知识应易于传播**， 每台个人电脑和每部现代手机都内置了浏览器软件，只要获知网页的URL地址就可以访问网页里的内容了。反观用Word书写的文档传播给他人时，阅读者还必须下载并安装Office之类的软件才能查看Word。

HTML文件通过浏览器阅读，也是用纯文本书写，接近完美。

## 初识Markdown
但对于作为**读书笔记**的记录方法，HTML仍然不够简洁，否则软件专业培训就不会有一门课叫”网页制作“了。结论是：**使用[Markdown](https://daringfireball.net/projects/markdown/syntax)书写笔记文档，写完后编译成网页（HTML）供自己或分享给他人阅读。**

下面让我们快速浏览一下Markdown的书写格式：

````markdown
## 初探HTML
顾名思义，HTML是一种标记语言。其标记以应用于文档内容（例如文本）的元素为其存在形式。

## 初探CSS
CSS（层叠样式表）用来规定HTML文档的呈现形式（外观和格式编排）。

### 定义和应用样式
CSS样式由一条或多条以分号隔开的样式声明组成。每条声明包含着一个CSS属性和该属性的值，二者以冒号分隔。下面是一条简单的CSS样式。

```
background-color:grey; color:white;
```

### CSS中的颜色
颜色在网页中的作用非常重要。在CSS中设置颜色有好几种方法。

**CSS颜色选编**  

|颜色名称|十六进制|十进制|
|---|---|---|
|black|#000000|0,0,0|
|silver|#C0C0C0|192,192,192|
|gray|#808080|128,128,128|

## 初探JavaScript
JavaScript过得挺不容易。出生不顺，青春期更满是苦涩。直到近年来，它才开始树立起一种实用的灵活语言的形象。JavaScript能做的事很多，尽管它还称不上完善，但也值得认真对待。
> **Atwood定律**: "任何可以使用JavaScript来编写的应用,并最终也会由JavaScript编写。"
````
  
通过Markdown编译工具翻译成HTML后如下显示：

![](https://img-camp.banyuan.club/prep/markdown-sample.png?x-oss-process=image/resize,w_800/sharpen,100)

Markdown格式极其收敛，只用了有限的几个语法标注，就可以做出上图这种简洁的书写效果，让作者专注于内容创作本身。任何Markdown无能为力的格式，都可以直接混合书写HTML（HTML无所不能）。不过，你应该总是把格式美化工作留到创作结束的时候。

## 云笔记工具

[![](https://img-camp.banyuan.club/prep/youdao-note-logo.png?x-oss-process=image/resize,w_20/sharpen,100)](http://note.youdao.com) **有道云笔记** 可能不是最好的Markdown编辑器，但是它是最好的支持Markdown格式编辑的云笔记软件。

![](https://img-camp.banyuan.club/prep/youdao-note-sample.png?x-oss-process=image/resize,w_800/sharpen,100)  

有道云笔记有可视化添加Markdown语法的操作按钮，有即时网页预览功能。另外，之所以称为“云”笔记，是因为可以随时随地通过手机、电脑、网页等多种方式编辑和分享笔记内容。你应该总是在移动设备上安装有道云笔记。

学习未知领域的知识，特别是对于系统性的知识，学习过程中有大量的实践总结和归纳、还有存疑处，都应记录到云笔记软件里，常常整理回顾，直到知识已经深深烙印在脑海里，把那些毫无价值的笔记内容再删除掉，使笔记内容总是有效。

根据个人喜好你也可以选择[大象笔记](https://evernote.com)、[为知笔记](http://www.wiz.cn/)等其他云笔记软件，甚至直接注册登陆 jianshu.com 网站(支持Markdown)，将愿意公开的内容发布到网站上分享给大众。

## 学习Markdown

### Markdown是什么

* Markdown是Aaron Swartz 跟[John Gruber](https://daringfireball.net/)共同设计的排版语言。
* Markdown的目标是实现「易读易写」。
* Markdown 语法的目标是：成为一种适用于网络的书写语言。
* Markdown 不是想要取代 HTML，
* Markdown 的理念是，能让文档更容易读、写和随意改。
* HTML 是一种发布的格式，Markdown 是一种书写的格式。

### Markdown扩展

Markdown由[John Gruber](https://daringfireball.net/)发布在https://daringfireball.net ，也可以浏览[Markdown中文网](http://www.markdown.cn/#) 快速了解Markdown的所有基本语法。

Markdown基础功能尚不完备，因此衍生了一系列版本，用于扩展Markdown的功能（如表格、脚注、内嵌HTML等等），Markdown增强版中比较有名的有[Markdown Extra](https://michelf.ca/projects/php-markdown/extra/)、[MultiMarkdown](https://fletcherpenney.net/multimarkdown/)、 [Maruku](https://github.com/bhollis/maruku/blob/master/docs/markdown_syntax.md)等。这些衍生版本要么基于工具如，如[Pandoc](http://pandoc.org)、[有道云笔记](http://note.youdao.com)(前文提及)；要么基于网站，如[GitHub](https://github.com)和[Wikipedia](https://www.wikipedia.org/)。它们在语法上基本兼容，但增强的语法使渲染效果更生动。

### 好用的Markdown工具


**有道云笔记** 可以用Markdown格式记录笔记。其实编辑和编译Markdown的工具很多，[Macdown](https://macdown.uranusjr.com/) 值得一试；对于Windows用户，推荐安装 [typora](https://typora.io/)。如果你坚持用Sublime Text，插件Markdown Preview小巧轻便。
