---
title: 程序员入行之素养(五)：一生万物、万物归一(命令行补充知识)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-22 10:00:00
---

下面这些补充的命令行知识不可或缺，只有掌握了，操作手法才能如行云流水。

## Home目录
只要当前正在操作Mac系统，你一定处于某个用户角色。一般在安装Mac系统时会分配给你一个用户名（和密码），并为其创建了一个目录名 ***/Users/\<username>*** ( **\<username>** 替换为为具体的用户名)，该目录被称为Home(家)目录。


Mac系统有一个默认的超级用户root，但是通常不使用。

### ★ pwd命令
>**pwd** 查看用户当前所在的目录，简称当前目录。

当首次打开**终端**的窗口，你就一定处在硬盘的某个目录下，默认处于Home目录，简单输入pwd：
```
pwd
```
我的Mac系统返回输出结果：
>/Users/banyuan

如果系统分配给你的用户名是 lixiaobai，那么返回的结果应该是：
>/User/lixiaobai

## 切换目录
### ★ cd命令
>**cd [目录名]** 进入指定的目录

**▷ 进入 ***/samples/os/*** 目录**  
输入命令：
```
cd /samples/os
pwd
```
返回输出结果：
>/samples/os

从而证明用户当前处于 ***/samples/os*** 目录

**▷ 进入Home目录**  
如果此时要回到Home目录，运行如下命令即可：
>cd /Users/banyuan

不过可以用 ***~*** 代指Home目录，所以键入下面的命令同样可以回到Home目录：
```
cd ~
```
甚至直接输入不带任何参数的cd命令也是一样的。

## 相对和绝对目录

假设现在已经切换到了 ***/samples/os*** 目录 ，想进一步查看子目录 ***unix*** 的内容，用过去学过的方法可以输入：
```
ls /samples/os/unix
```
现在有一个简短的命令：
```
ls unix
```
将得到同样的结果。这是因为ls后面的目录或者文件名如果不以 **/** 符号开头，它将自动认为是从当前目录向下搜索，我们称这种不以 ***/*** 开头的条目为相对目录或相对路径。作为对比，之前我们书写的全路径叫绝对目录或绝对路径。理解相对路径至关重要，学会它会大大简化命令行的操作。

**▷ .和..目录**  

.（一个点）代指当前目录：***ls unix*** 也可写作  ***ls ./unix*** ；  
..（两个点）代指上级父目录：假设当前在 **ls /samples/os** 目录（用pwd命令确定当前所在目录），想查看上级目录的 **basic** 子目录下有什么文件，可以输入下面的命令：
```
ls ../basic
```
另外，如果执行带-a参数的ls命令：
```
ls -la
```
将返回出结果
```
drwxr-xr-x   7 AllenGuo  staff    224  4  3 22:58 .
drwxr-xr-x  13 AllenGuo  staff    416  4  3 23:35 ..
-rw-r--r--@  1 AllenGuo  staff  28113  4  3 18:20 linux-guide.jpg
-rw-r--r--@  1 AllenGuo  staff  17183  4  3 18:22 linux-intro.docx
-rw-r--r--@  1 AllenGuo  staff   1469  4  3 18:25 mac os.html
drwxr-xr-x   4 AllenGuo  staff    128  4  3 23:01 unix
```
除了 **历史教育**，.和..也显示出来了，即表示逻辑上存在 . 和 .. 目录（如果你实验时候看到其他以.开头的条目，它们是隐藏文件或目录，以后会用到）。

**小实验**：大家尝试一下 ***cd .*** 和 ***cd ..*** 再执行 pwd命令，看看自己身在何处？

### ★ clear命令
>**clear** 清除屏幕文字，使光标回到屏幕顶部
 
进行了大量的命令行操作后，屏幕上的文字乱得一团糟，输入clear后，是不是感觉世界瞬间清静了？不过有个更好的清屏快捷键操作： ***⌘ + K*** ，两者有什么区别，可以自己去体会。

## 批处理

有些命令如mkdir创建目录、echo创建一个文本文件，如果成功不返回任何输出结果。如果想进一步操作成功与否，最好再执行以下ls、cat命令进一步去验证。我们可以把这一系列操作写到一个文本文件里，使这个文件运行完成上述所有任务。

1. 创建文本文件 batch.sh （文件名任意，但建议遵循惯例，用.sh作为扩展名）
```
echo 'mkdir -p /samples/movie/action'>/samples/batch.sh
echo 'echo "Friendship is everything.">/samples/movie/action/godfather.txt'>>/samples/batch.sh
echo 'ls -l /samples/movie/action'>>/samples/batch.sh
echo 'cat /samples/movie/action/godfather.txt'>>/samples/batch.sh
```

2. 用sh命令运行batch.sh文件
```
sh /samples/batch.sh 
```
返回输出结果：
```
total 8
-rw-r--r--  1 AllenGuo  staff  26  4  4 00:06 godfather.txt
Friendship is everything.
```

说明mkdir、ls、echo等几个命令执行成功。我们称这样的文本文件为[Shell脚本](https://www.shellscript.sh/)文件（Shell Scripts）。Shell脚本不但可以运行命令，还可以指定逻辑分支、循环，是一门完整的编程语言。我们常常可以使用Shell脚本批处理预定的一系列操作任务，应用十分广泛，值得学习。

### ★ chmod命令
>**chmod** 改变文件或目录的属性（可读、写、运行等）

可以赋予脚本文件batch.sh可运行属性，使用chmod命令：
```
chmod +x /samples/batch.sh
```
这样能像运行普通命令一样去运行batch.sh：
```
/sample/batch.sh
```
它将返回前面同样的输出结果。

如果 **/samples/os** 目录下有数个 .sh 脚本文件都要一起设置为可执行(x)属性，那么运行chmod 命令：
```
chmod -R +x /samples/os
```
不仅仅.sh，该命令也把 **/samples/os/** 目录下所有文件设置为可执行(x)属性，即便有些文件不具备执行能力。使用-R参数（R是递归的意思）进行递归处理所有子目录。

### ★ export命令
>**export** 设置系统搜索可执行命令的路径（目录）

有个问题，为什么不是直接键入 batch.sh，而是要输入 batch.sh的全路径才能正确执行脚本？为此要再次谈及路径（Path），Mac通过export命令指定一个叫PATH的条目的值，其值为一组路径（目录），目录之间用 **:** 分隔。如果 batch.sh 所在的目录在这个路径列表里，就可以直接输入 batch.sh 运行之，否则就不能。

先键入 export ，返回结果有一行（每个人的执行export返回结果可能有所不同）：
```
declare -x PATH="/usr/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin
```
这组目录有：
```
/usr/local/sbin
/usr/local/bin
/usr/bin
/bin
/usr/sbin
/sbin
```
显然，/samples不在这个列表里，执行命令：
```
export PATH=$PATH:/samples
```
这个命令的含义就是：在原有路径（$PATH代指）的基础上再添加一个目录/samples。执行完 export PATH=$PATH:/samples 命令后，你可以在再次执行 export 命令，看看PATH是否变化了。


好了，现在试试直接输入 batch.sh，看看输出结果是否正确？

## 附:常用命令行

|命令名|释义|
|---|---| 
|ls|查看目录和文件信息|
|find|查找名字为指定特征的文件或目录|
|tree|显示目标目录的结构（需要单独安装才能使用）|
|cat|查看文件内容|
|mv|移动文件或目录到目标位置|
|cp|复制文件或目录到目标位置|
|mkdir|创建目录|
|echo|输出文本到屏幕或目标文件|
|touch|创建一个空文件|
|rm|删除文件或目录|
|pwd|查看当前或指定目录的绝对位置|
|cd|进入指定目录|
|chmod|改变文件或目录的属性(读、写、运行)|
|export|设置系统变量|
|sh|运行脚本文件|
|vi/vim|一个文本编辑软件|