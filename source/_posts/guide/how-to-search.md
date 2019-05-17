---
title: 程序员入行之素养(三)：寻根问题、追本溯源(如何检索专业知识)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-08 10:00:00
---

如果你有传统文献检索的经验，这里可以看做是互联网时代知识检索的一个新的渠道，内容相当通俗易懂。假设导师刚分配一个你未知计算机领域的课题：”同学们，去了解下DocBook，下个月我们将使用它来书写论文“，想想你会怎么做？

## 尝试搜索
如果你对DocBook一无所知，我想直觉的反应就是打开搜索引擎网站，输入："**什么是DocBook**"，如果你正在使用百度，以下就是搜索结果：

![](https://img-camp.banyuan.club/prep/what-is-docbook-search.png?x-oss-process=image/resize,w_500/sharpen,100)

结果总是优先呈现自家的"百度百科"（如果采用科学上网，wikipedia.org 上DocBook的词条可能更被优先展现）。不论哪个**百科**，你很快获得一种印象：**百科**是个宝库，对世界上很多词条给以正规的、通俗的阐述，百科一般属于三次文献，参考价值自然不错。 

继续向下翻阅搜索结果，如果某个相关标题看起来更易懂，当然也可以点进去看看。但是，这往往需要你仔细甄别目标网站的知名度、作者的水准，有可能作者对问题的表述很业余甚至是错的，耽误了大家宝贵的学习时间，甚至误入歧途。

[知乎](https://zhihu.com)是一个更专业的问答网站，你可以直接进入该网站搜索docbook相关词条或提问，往往能得到更专业回答。

## 追本溯源

计算机技术起源西方，大多用英语阐述，不妨去掉关键字里的中文，直接搜索"DocBook"试试，百度搜索结果如下：

![](https://img-camp.banyuan.club/prep/docbook-search.png?x-oss-process=image/resize,w_500/sharpen,100)

如果关键字涉及某种专业技术，通常第一个搜索结果都是这个技术的官方网站。观察上图显示的第一个搜索结果，对应网址是：https://docbook.org ，从名字上看，貌似该知识的发源。不过打开之后，第一感觉是卖书的，这不符合一般"官方"的格调啊...

![](https://img-camp.banyuan.club/prep/docbook.org.png?x-oss-process=image/resize,w_500/sharpen,100)

仔细阅读官网页面上不的文字（上图所示），里面有句话：

>The definitive guide is the official documentation for DocBook.  
>...  
>but it is still [available online](https://docbook.org/tdg/).

>**《DocBook权威指南》是DocBook的官方文档 ...  你仍然可以从 https://docbook.org/tdg/ 获取...**

误会误会，是李逵，不是李鬼。打开在线文档，名副其实的一本书的内容。看来这个知识可能需要系统地去学习啊。不过当务之急是先快速地了解基础概念才对，点击"What is DocBook"链接，里面又说："DocBook由[OASIS](http://www.oasis-open.org/)维护..."。 进入OSASIS网站，里面清楚地阐述DocBook的发展历史，演进方法，当前最新标准是5.1，打开最新标准文档，里面一句话总结了概念：

>DocBook is a general purpose [XML] schema particularly well suited to books and papers about computer hardware and software (though it is by no means limited to these applications).  
>**DocBook是一个XML Schema，特别适合于书写计算机领域的书和论文（但不限于此）。**

如果很不幸你不了解XML，那么你将不得不开展另一个学习线索。由于我们这里只是以Docbook举例，就不展开了。总之，你现在应该对Docbook个基本印象：**DockBook是用来写书的。**

## 小试牛刀

”Word可以写书、网页也可以写，DocBook为什么被推崇？“ 带着问题去学习，很自然地就会去深入文档了。一旦理解其理念后（原来DocBook格式的文档更容易交换和传播啊），一定是跃跃欲试、摩拳擦掌了。

官网Wiki页面，里面罗列了庞杂的书写工具（软件），挨个试着下载、安额和使用它们，直到找到最顺手的，赶快来试一试吧。下图是我用XMLmind XML Editor制作的一本书的样例：

![](https://img-camp.banyuan.club/prep/xmlmind.png?x-oss-process=image/resize,w_500/sharpen,100)

严肃地学习一个计算机专业知识、特别是系统性的知识，"追本溯源"是必须养成的思维习惯："找到知识的起源——原文出处、官方网站，读第一手资料"。前文提到的**百科**、**知乎**等主要是中文阐述、通俗简短，其全面性、权威性往往不足，只能作为一个辅助手段，用来快速了解问题的概貌。