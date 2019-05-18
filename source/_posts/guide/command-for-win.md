---
title: 程序员入行之素养(五)：一生万物、万物归一(Windows命令行)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-28 10:00:00
---

Windows系统是操作系统中的异类，它使用英文字符(A~Z)将磁盘换分为多个逻辑区域，可以根据喜好像下面这样，把磁盘分为3个逻辑盘，命名分别为C、D、E：

![](https://img-camp.banyuan.club/prep/win-disk.png?x-oss-process=image/resize,w_630/sharpen,100)


前文的文件和目录分散到了C、D、E三个（逻辑）盘里。



可以想象Windows系统有一个虚拟的根（**/**）目录：
```
[/]
 |_ [C:\]
 |   |_ [文科]
 |   |     |_ [历史教育]
 |   |            |_ 全球通史.docx
 |   |            |_ 中国古代简史.pdf
 |   |            |_ 中国近代史1840-1949.txt
 |   |            |_ 中国史纲要.html
 |_ [D:\]
 |   |_ [教育理念]
 |         |_ 半圆文化.txt
 |_ [E:\]
     |_ [计算机专业]
           |_ 编译原理.pdf
           |_ 核心Java卷I.pdf
           |_ C语言程序设计.pdf
```

Windows系统也自带命令行工具，在运行窗口输入 cmd，即可进入命令行操作窗口。

现在想访问D盘的 **半圆文化.txt** 文件，操作命令是：

```
type D:\教育理念\半圆文化.txt↩
```
如果要进入D盘的 **教育理念** 目录，操作命令是：
```
D:\↩
cd 教育理念↩
```

注：Windows下的 目录分隔符是 \ 不是 /。

附：下面是Windows和Mac常用命令的对比：

|Mac命令|Windows命令|释义|
|---|---|---| 
|ls|dir|查看目录和文件信息|
|find|find|查找名字为指定特征的文件或目录|
|tree|tree|显示目标目录的结构（需要单独安装才能使用）|
|cat|type|查看文件内容|
|mv|move|移动文件或目录到目标位置|
|mv|rename|改变文件名|
|cp|copy|复制文件到目标位置|
|cp -r|xcopy|复制目录到目标位置|
|mkdir|md|创建目录|
|echo|echo|输出文本到屏幕或目标文件|
|touch|/|创建一个空文件|
|rm -d|rmdir|删除目录|
|rm|delete|删除文件|
|pwd|pwd|查看当前或指定目录的绝对位置|
|cd|cd|进入指定目录|
|chmod|attrib|改变文件或目录的属性(读、写、运行)|
|export|set|设置系统变量|
|sh|识别.cmd或.bat结尾<br/>的文件为脚本文件|运行脚本文件|
|Bash语法|Windows语法|脚本语言语法|