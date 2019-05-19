---
title: 程序员入行之素养(五)：一生万物、万物归一(命令行与计算机资料)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-15 10:00:00
---

>笔者根据个人二十年从业经验，总结了在开始编程之前，应系统性地准备一系列工作，形成了“程序员入行必备之素养”系列。谨此，献给有志于从事软件开发职业的浩浩青年。

这是本系列文章唯一有**专业技术**要求的一篇，但是，没那么遥不可及。计算机好比一个图书馆，无论作为计算机专业人员还是业余爱好者，都要学会如何存取计算机这个大图书馆。

简单说，Mac电脑用户必须熟练使用 **访达(Finder)** 来存取计算机里的数据资料（与 ***访达*** 对应的Windows软件叫 ***文件管理器***）。  
![Finder](https://img-camp.banyuan.club/prep/finder.png?x-oss-process=image/resize,w_750/sharpen,100)

## 文件和目录概念
电脑里所有的资料都存在一个名字叫**硬盘**的硬件设备里，断电后数据不会丢失。计算机采用了图书馆类似的概念：把数据组织成 **文件(File)** 和 **目录(Directory)** 放在硬盘里。

**文件之于目录，犹如图书之于书架**。和图书馆有所不同的是，计算机里文件和目录是一个二维的树型结构，例如：

```
[/]
 |_[samples]
      |_ [计算机专业]
      |    |_ 编译原理.pdf
      |    |_ 核心Java卷I.pdf
      |    |_ C语言程序设计.pdf
      |_ [教育理念]
      |    |_ 半圆文化.txt
      |_ [文科]
           |_ [历史教育]
                |_ 全球通史.docx
                |_ 中国古代简史.pdf
                |_ 中国近代史1840-1949.txt
                |_ 中国史纲要.html
```

上图用 **[]** 扩起来的条目是目录，即资料所在的位置，其他条目则是文件，是资料本身。

下面是几个重要的有关目录的概念：

* 根目录(Root)   
  名字为 **/** 的目录是计算机的 **根目录**，就像图书馆的大门口，一切资料的位置都要循着 **/** 目录去定位和检索。比如，可以说：**"编译原理.pdf"** 这份资料位于 **/samples/计算机专业** 目录；**"全球通史.docx"** 的位于 **/samples/文科/历史教育** 目录。

* 子目录(Sub)  
相比之下，**"文科"** 、**"计算机专业"** 是 **/** 和 **samples** 的子目录（Sub），**"历史教育"** 是 **"文科"** 的子目录。

* 父目录(Parent)  
反之，**"文科"** 是 **"历史教育"** 的父目录，**/** 是所有目录的父目录。

文件 **"全球通史.docx"** 存在于 **/samples/文科/历史教育** 目录下，我们把 **/文科/历史教育/全球通史.docx** 称为该文件的全路径（Path）。描述文件或目录的路径时，每个条目之间用 **/** 分隔。

## 命令行工具
对于专业选手，除了要熟练用 **访达** 存取文件和目录，还必须学会使用 **命令行** 完成同样的操作。

相信大家都很熟悉在Windows系统里点击QQ、Word图标启动程序；启动程序的另一种方式是：通过输入相应的程序名(约定的文字)，敲击回车键来启动程序的运行，我们称之为命令行操作。

![Terminal](https://img-camp.banyuan.club/prep/terminal-logo.png?x-oss-process=image/resize,w_40/sharpen,100) Mac系统使用 **终端(Terminal)** 进行 **命令行** 操作，点按桌面相应图标即可启动**终端**，也可以通过 Spotlight(还记得快捷键**⌘ + 空格**吗？) 输入文字 ***terminal*** 后敲击回车键快速打开**终端**。

![Terminal](https://img-camp.banyuan.club/prep/terminal-main.png?x-oss-process=image/resize,w_750/sharpen,100)

## 例子准备

为方便实验，我们精心准备了一个例子，目录和文件名主要用英文表示，具体结构如下：
```
/samples/
├── [basic]
│     ├── algorithm.pdf
│     ├── compiling.pdf
│     └── [math]
│           └── linear.algebra.pdf
├── [culture]
│     └── banyuan.txt
├── [important]
├── [langs]
│     ├── c.pdf
│     ├── css.pdf
│     ├── [java]
│     │     ├── core-java-i.pdf
│     │     ├── core-java-ii.pdf
│     │     └── java8-guide.pdf
│     ├── python.pdf
│     └── web.html
├── [os]
│     ├── linux-guide.jpg
│     ├── linux-introduction.docx
│     ├── mac os.html
│     └── [unix]
│           ├── unix-intro.pdf
│           └── what-is-bash.pdf
├── [web]
│     ├── apache.pdf
│     ├── [build]
│     │     └── webpack4.jpg
│     ├── [framework]
│     │     ├── expressjs.pdf
│     │     └── springio.pdf
│     ├── nginx.pdf
│     └── [orm]
└── [历史]
       └── 中国古代简史.pdf
```
请点击 [samples.zip](https://img-camp.banyuan.club/prep/samples.zip) 下载并解压缩，并将其拖动到 **/** 目录（根目录）下。

为完成该操作，首先需要使用 **访达(Finder)** 定位到 **/** 目录，打开 **访达(Finder)**，窗口左侧有一个 **Macintosh HD**，点击后，右侧主窗口显示的即是 **/** 目录，如下图所示：

![](https://img-camp.banyuan.club/prep/root-dir.png?x-oss-process=image/resize,w_750/sharpen,100)

>注：如果 **Finder** 窗口左侧没有看到 **Macintosh HD** 怎么办？  
>
>打开 **Finder** 菜单：前往->电脑（或者按快捷键 ⌘ + ⇧ + C），拖动右侧窗口的 **Macintosh HD** 到左侧窗口 **位置** 下面。


其次，你要知道你下载的 samples.zip 位于**下载** 目录， **访达(Finder)** 窗口左侧有个 **下载**，点击后在右侧主窗口看到samples.zip，将解压缩的 samples 目录复制到 **/** ，复制时系统弹出对话框，要求输入Mac用户的密码（这个在你安装Mac系统时，系统分配给你的用户和密码），输入密码后，例子准备工作就做好了。

接下来我们就以前面图示的文件和目录为例，一起实践吧！

>一个悖论是：**我只有Windows没有Mac电脑，所以无法实践命令行操作；不实践命令行操作我无法通过入学面试；不入学半圆我就没有Mac电脑（入学半圆就送全新Mac电脑）。** 即便如此，你仍然要读完接下来的内容，在最后，我们列出了Windows下命令行操作的对应方法和规则，祝你能从Mac的操作教程中汲取灵感，更好地在Windows下展开实践。