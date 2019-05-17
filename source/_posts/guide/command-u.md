---
title: 程序员入行之素养(五)：一生万物、万物归一(命令行”更新“电脑资料)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-15 10:00:00
---

## 更新目录
### ★ mv命令
>**mv** 对给定的目录或文件更名或移动

**▷ A. 更名目录"/samples/langs" 为 "/samples/languages"**
```
mv /samples/langs /samples/languages
```
如果命令运行正确，则不返回任何输出结果。

**▷ B. 验证更名成功与否**

1. 输入命令：
```
ls -l /samples/langs
```
返回输出结果如下：
```
ls: /samples/langs: No such file or directory
```

2. 输入命令：
```
ls /samples/languages
```
返回输出结果如下：
```
c.pdf  css.pdf  java  python.pdf
```

**思考：languages和Languages是一个目录吗？**  
>在Mac和Window操作系统里，文件和目录名不区分大小写，所以是一个目录。但是，Linux和Unix系列操作系统则区分大小写。未来大家写的程序分发到Unix Like系统里的场合很多，建议大家养成不使用大小写字符区分文件和目录的习惯。

mv命令不但可以更改目录名，其实对文件名同样使用，这个大家自己去实验。

## 更新文件
### ★ echo命令
>**echo** 组合>>参数追加文本到目标文件

**▷ A. echo组合>>符号**

这里，我们要学习如何对文件的内容进行更新操作。

前文创建的 /samples/database/rdb/mysql.txt 有内容 "MySQL is a open-source database"，现在我们运行命令：

```
echo 'but it is not free.'>>/samples/database/rdb/mysql.txt
```
这将追加>>符号前面双引号里的文字内容到mysql.txt（文件里原来的内容保留）。

**▷ B. 验证mysql.txt内容是否更新**
```
cat /samples/database/rdb/mysql.txt
```
返回如下输出结果：
>MySQL is a open-source database  
>but it is not free.

**▷ C. 不合法的命令**

现在想在mysql.txt里再追加一行文字：MySQL isn't Free.，仍然使用echo命令：
```
echo 'MySQL isn't Free.'>>/samples/database/rdb/mysql.txt
```
结果屏幕会显示>符号，光标停留在>后面
```
MagicLife:/ banyuan$ echo 'MySQL isn't Free.'>>/samples/database/rdb/mysql.txt
> ▌
``` 
合法的命令执行完一般是显示程序执行结果，然后回到提示符下（我的电脑是MagicLife:/ banyuan$，每个人依用户名不同，提示有所不同），可以继续输入下一条命令。

上述提示表明前面的命令行不完整（合法），因为你既无法看到echo命令的的返回结果。也不能输入下一条命令，怎么办呢？简单按 ***\^ + C*** （^是CTRL键）强制放弃当前程序的执行，回到提示符下。

仔细看echo命令后面用 ***'*** （单引号）包裹起来的字符串本身也有一个单引号，这将让echo命令无所适从，它无法判定哪个单引号表示字符串的结束还是文字内容本身的 ***'*** 。还记得前文说echo后面的字符串可以 ***'*** 或者 ***"*** 包裹吗？因此，可以修改后的echo命令如下：
```
echo "MySQL isn't Free.">>/samples/database/rdb/mysql.txt
```

**▷ D. 字符转义**

现在 ***'*** 换成了 ***"*** ，可以在文本里包含'字符了。思考一下，如果字符串本身包含一个"怎么办呢？比如想在mysql.txt里追加一行文本： ***Hi guys, " is a special character.*** 

这就需要在文本 **" is a ...** 的 ***"*** 前面添加一个\字符进行转义，让echo明确理解 ***"*** 不是字符串的包裹，而是的的确确的双引号字符。因此，修改后的echo命令如下：
```
echo "Hi guys, \" is a special character.">>/samples/database/rdb/mysql.txt
```
返回输出结果如下：
```
MySQL is a open-source database
but it is not free.
MySQL isn't Free.
Hi guys, " is a special character.
```


### ★ vim命令
**▷ 没人使用echo编辑文字**

大家都有过写Word文件的的体验吧？通过它的图形化界面，一切都是那么理所当然：创建文件，编辑文件使加粗文字、插入图片，存储文件...

反观echo的局限则太多，首先它只能用来编辑文字，而且貌似也无法容易地修改文字（上面的例子都在用>>来追加文字）。

那么命令行下有没有可以易用的文字编辑软件（命令）呢？有，这个就是大名鼎鼎的vi，包括它的升级版[![](https://img-camp.banyuan.club/prep/vim-logo.png?x-oss-process=image/resize,w_30/sharpen,100)](https://www.vim.org/) 也都内置在Mac系统中。虽然半圆入学考试暂时不要求vi的使用，但是它确是接下来操作Linux服务器软件——必知必会！

## 移动/复制文件或目录
### ★ mv命令
>**mv** 移动给定的目录或文件

**▷ A. 移动目录**

如果依次实验完前面的例子，当前 /samples 文件目录结构如下（部分）：
```
/samples/
├── database
│   └── rdb
│       ├── mysql.txt
│       └── oracle.txt
...
├── os
│   ├── linux-guide.jpg
│   ├── linux-introduction.docx
│   ├── mac os.html
│   └── unix
│       ├── unix-intro.pdf
│       └── what-is-bash.pdf
......
```

运行mv命令：
```
mv /samples/database /samples/os
```

文件目录结构将变更为：
```
/samples/
...
├── os
│   ├── database
│   │   └── rdb
│   │       ├── mysql.txt
│   │       └── oracle.txt
│   ├── linux-guide.jpg
│   ├── linux-introduction.docx
│   ├── mac os.html
│   └── unix
│       ├── unix-intro.pdf
│       └── what-is-bash.pdf

...
```
对比一下上述变化，能理解mv移动目录的用法了吗？

**▷ B. 移动文件**

同理，移动文件到指定目录留给大家自己实践：试试将 **/samples/os/unix/what-is-bash.pdf** 移动到 **/samples/web** 目录？

最后让我们试试下面的命令：
```
mv /samples/os/linux-introduction.docx /samples/os/linux-intro.docx
```
再运行ls命令检查上面操作成功与否：
```
ls -l /samples/os
```
返回输出结果：  
```
drwxr-xr-x  4 AllenGuo  staff    128  4  3 22:15 database  
-rw-r--r--@ 1 AllenGuo  staff  28113  4  3 18:20 linux-guide.jpg  
-rw-r--r--@ 1 AllenGuo  staff  17183  4  3 18:22 linux-intro.docx  
-rw-r--r--@ 1 AllenGuo  staff   1469  4  3 18:25 mac os.html  
drwxr-xr-x  4 AllenGuo  staff    128  4  3 23:01 unix
```

咦？linux-introduction.docx 文件不见了，取而代之的是 linux-intro.docx，这就是文件名更名操作嘛！

### ★ cp命令
>**cp** 复制存在的目录或文件

**▷ A. 复制文件**   
当前目录结构：
```
/samples/
...
├── basic
│     ├── algorithm.pdf
│     ├── compiling.pdf
│     └── math
│            └── linear.algebra.pdf
├── [important]
...
```

如果 /samples/basic/math/linear.algebra.pdf 是份重要的文件，想复制到 **/samples/important** 目录，执行命令如下：
```
cp /samples/basic/math/linear.algebra.pdf /samples/important
```
操作后文件目录结构如下：
```
/samples/
...
├── basic
│     ├── algorithm.pdf
│     ├── compiling.pdf
│     └── math
│            └── linear.algebra.pdf
├── [important]
│      └── linear.algebra.pdf
...
```

**▷ B. 复制目录**

接前面的实验：复制 /samples/basic 目录下的文件和子目录到目标目录，但保持原目录结构：
```
cp -r /samples/basic /samples/important
```
操作后目录结构如下：
```
/samples/
├── [basic]
│      ├── algorithm.pdf
│      ├── compiling.pdf
│      └── [math]
│             └── linear.algebra.pdf
├── [important]
│      ├── linear.algebra.pdf
│      └── [basic]
│             ├── algorithm.pdf
│             └── compiling.pdf
│             └── [math]
│                     └── linear.algebra.pdf
...
```

为了方便实验，先删除上面复制出来的 /samples/important/basic 的目录，再执行cp命令，不过这次cp命令参数中 **源目录路径** 最后多了 **/** ，如下：
```
cp -r /samples/basic/ /samples/important
```
操作后目录结构如下：
```
/samples/
├── [basic]
│      ├── algorithm.pdf
│      ├── compiling.pdf
│      └── [math]
│             └── linear.algebra.pdf
├── [important]
│      ├── algorithm.pdf
│      ├── compiling.pdf
│      ├── linear.algebra.pdf
│      └── [math]
│              └── linear.algebra.pdf
```
注意到差异了吗？源目录路径中最后一级目录 **basic** 本身没有被创建到目标目录，仅按源目录布局复制了其子目录和文件。

**提示**：rm命令的-i -f参数对于cp同样适用，大家可以亲自去试试。另外，前面用过的几乎所有命令如果不带参数，都会返回该命令的用法，比如：
```
cp
```
屏幕返回输出结果：
```
usage: cp [-R [-H | -L | -P]] [-fi | -n] [-apvXc] source_file target_file
       cp [-R [-H | -L | -P]] [-fi | -n] [-apvXc] source_file ... target_directory
```