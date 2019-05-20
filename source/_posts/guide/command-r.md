---
title: 程序员入行之素养(五)：一生万物、万物归一(命令行”读“电脑资料)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-16 10:00:00
---

现在开始漫游计算机。想象一下你正走进都柏林的圣三一学院图书馆，面对浩瀚的知识海洋，为了找到自己需要的资料，需要经过如下步骤：

1. 确定你要寻找的资料名称
2. 拿到资料目录，查出资料的所在位置
3. 打开目标位置的资料阅读

## 1. 确定你要寻找的资料名称
假设要找的文件是 ***banyuan.txt***

## 2. 拿到资料目录，查出资料的所在位置
此目录非彼目录，这里说的资料目录实际是资料名称（文件名和目录名）列表。英文表达为Catalog而不是Directory。

### ★ ***ls*** 命令
>ls 是Mac操作系统自带的一个命令行程序，用于列出指定目录下文件和子目录。

当然，一切命令行操作的前置操作是：打开**终端**软件。终端窗口也称控制台（Console），在控制台输入命令文字后，按↩（回车键）使运行。

在控制台输入ls命令：
```
ls /
```
输出结果如下：
```
Applications  Users  dev  Library  Volumes  etc  net  tmp  Network  bin  home  opt  sbin  usr  System  cores  private  server  var
```
>命令行输入的文字串第一个空格后面的字符串，称之为程序的**参数**，用来调整程序的具体行为。ls 后面的字符串即 **/** 为ls命令的参数。  
>上面命令的具体含义是：查看 **/** 目录下第一级文件和子目录名称（不包含子目录及下面的文件），逻辑结构如下：
```
/
├── Applications
├── Library
├── Network
├── System
├── Users
├── Volumes
├── bin
├── cores
├── dev
├── home
├── net
├── opt
├── private
├── sbin
├── server
├── tmp
├── usr
└── var
```

如果你想查看整个计算机硬盘里的资料目录，可以运行带-R参数的ls命令，不过这个命令的运行时间可能很长，因为资料目录实在太大，你可以随时按 **⌃ + C** 快捷键（⌃是CONTROL键）停止命令的运行：
```
ls -R /
```

下面摘取了部分输出结果：
```
...
/usr:
bin  lib  libexec  local  sbin  share  standalone

/usr/bin:
as  dns-sd  jarsigner  neqn  renice  topsyscall

/usr/lib:
PN548_API.dylib  libbsm.dylib  libexpat.dylib  libnetsnmp.5.dylib  libsasl2.dylib

/usr/lib/groff:
groffer  site-tmac
...
```
虽然很丑陋，不像前文那么友好的树状图，但终究是罗列出来了一个完整的目录。

因为电脑上的资料实在太多，即便仅展示资料目录也庞大和琐碎得象一本书，而且文件名不象图书馆里的资料那样有约定的分类编号，上述方法实际很少有人使用。通常都是依照目录的层级渐进查找资料。

比如，如果预先知道目标资料在/samples的某个更深层次的子目录，可以先运行命令：
```
ls -l /samples
```
返回 **/samples** 目录下的文件和第一级子目录：

```
drwxr-xr-x  6 AllenGuo  staff  192  4  3 23:05 basic
drwxr-xr-x  4 AllenGuo  staff  128  4  3 18:06 culture
drwxr-xr-x  2 AllenGuo  staff   64  4  3 23:09 important
drwxr-xr-x  8 AllenGuo  staff  256  4  3 18:26 langs
drwxr-xr-x  7 AllenGuo  staff  224  4  3 22:58 os
drwxr-xr-x  8 AllenGuo  staff  256  4  3 22:06 web
drwxr-xr-x  3 AllenGuo  staff   96  4  3 21:02 历史
```

这里增加了 **-l** 参数，可以让列出的文件或目录竖排排版，将条目的诸多属性追加到条目的左侧，上述结果里每行第一个字母d（Directory）表示每个条目都是目录，从而确定计算机 **/samples** 目录下原来有三个子目录，推测 **banyuan.txt** 可能在 **/samples/culture** 目录，继续运行命令：
```
ls -l /samples/culture
```
返回 **/samples/culture** 目录下的文件和子目录：
```
-rw-r--r--@ 1 AllenGuo  staff  39  4  3 18:06 banyuan.txt
```
结果里每行（其实就一行）第一个字符是-，表示该条目是文件（File）。果然，**banyuan.txt** 位于 **/samples/culture** 目录。也可以说：**banyuan.txt** 的全路径是 **/samples/culture/banyuan.txt**

>**提示**：只有预期 /samples 目录下的文件和子目录不是很庞大的时候，才使用上文介绍的-R参数，可以一步到位扫到目标文件所在的位置。

>**小技巧**： 输入 ***ls -l /samples/cul*** 时突然忘记了"文化"这个英文单词后面的字符，按 TAB 键试试看，会有小惊喜。

### ★ ***find*** 命令
>find 说明文件或目录名特征信息，在指定的目录下搜索。

有没有一种类似搜索引擎（百度）的更直接的资料检索方法，只要输入“banyuan.txt”，就可以找到目标资料？试试find：
```
find /samples -name 'banyuan.txt' 
```

>上面的例子含义是：在 **/samples** 目录下（包含所有子目录）搜索名字为 **banyuan.txt** 的文件或目录。再次提醒：这里find后面一串字符 **/samples -name 'banyuan.txt'** 是find程序的参数。

执行后输出结果如下：
```
/samples/culture/banyuan.txt
```
这是搜索到的文件的全路径，即得出结论：**banyuan.txt** 位于 **/samples/culture/** 目录。

**思考**：不管三七二十一，如果find命令指定目标搜索目录是 **/** ， 那么不就可以在整个计算机硬盘里搜索资料了吗？不错，但是尽量不要这样做，因为这会使搜索时间大大变长。

## 3. 阅读资料

### ★ ***cat*** 命令
> cat 显示指定文件的内容，后面第一个参数是文件的全路径名。注意，cat只能显示 **纯文本** 文件（图片文件无能为力）。

```
cat /samples/culture/banyuan.txt
```
>上面的含义是，显示 **/samples/culture/banyuan.txt** 文件的内容。

输出结果如下：
```
半圆学社是持续学习的践行者
```
上面的文字正是 **banyuan.txt** 文件里内容。

## 4. 更好用的tree命令

### ★ ***tree*** 命令
>**tree** 用友好的树形结构列出该计算机的资料目录（Catalog）。

tree不是Mac操作系统自带的命令行程序，也称为**外部命令**，需要依靠[![Homebrew](https://img-camp.banyuan.club/prep/homebrew-logo.png?x-oss-process=image/resize,w_40/sharpen,100)Homebrew](https://brew.sh/)软件来安装。这个工具也将是入学半圆后第一个要学习的软件。同学，要不要现在挑战一下？

一旦安装好tree之后，输入命令（请注意及时按 ⌃ + C快捷键停止命令的运行，因为整个计算机的资料目录太大了☠）：
```
tree -N /
```

>上面命令的含义是：查看 **/** 目录下所有子目录和文件的名称列表（即：Catalog）， **-N** 参数能确保目录或文件名里中文正确显示。

输出部分结果如下图所示：  
![Terminal](https://img-camp.banyuan.club/prep/tree-root.png?x-oss-process=image/resize,w_850/sharpen,100)  

因为计算机上的资料太庞大。可以采用类似ls命令渐进法，输入：
```
tree -N /samples
```

这将仅显示 **/samples** 目录下的子目录和文件，输出结果如下：

![Terminal](https://img-camp.banyuan.club/prep/tree-samples.png?x-oss-process=image/resize,w_850/sharpen,100)  


缩小了搜索范围，将更快地返回资料目录。怎么样，tree工具还不错吧？

>**扩展名** 阅读上面的文件名，会发现一个共同的特点，它们都以.后面加几个字符结尾。我们称之为文件扩展名。这么做的主要目的是分类文件，比如 **全球通史.docx** 以 .docx 结尾，我们很容易就知道，该文件应该是Word文档。用 **访达** 查看该文件，它会显示出一个Word图标，如果系统安装了Office，轻敲该文件还会自动地打开关联的Word软件。所以，建议制作文档命名时，总是给文件命名以合适的扩展名。
