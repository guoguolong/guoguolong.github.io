---
title: 程序员入行之素养(五)：一生万物、万物归一(命令行“创建”电脑资料)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-17 10:00:00
---

## 创建目录
### ★ **mkdir** 命令
>mkdir 用来创建目录

**▷ A. 创建目录"/samples/bigdata"**  
```
mkdir /samples/bigdata
```
如果命令运行正确，则什么也不返回。

**▷ B. 验证目录是否被正确创建**  
```
ls -l /samples/
```
输出结果如下：
```
drwxr-xr-x  6 AllenGuo  staff  192  4  3 23:05 basic
drwxr-xr-x  2 AllenGuo  staff   64  4  3 23:31 bigdata
drwxr-xr-x  4 AllenGuo  staff  128  4  3 18:06 culture
drwxr-xr-x  2 AllenGuo  staff   64  4  3 23:09 important
drwxr-xr-x  8 AllenGuo  staff  256  4  3 18:26 langs
drwxr-xr-x  7 AllenGuo  staff  224  4  3 22:58 os
drwxr-xr-x  8 AllenGuo  staff  256  4  3 22:06 web
drwxr-xr-x  3 AllenGuo  staff   96  4  3 21:02 历史
```
"bigdata" 这一行是新增的条目，第一个字母是d，表示这是一个目录。

**▷ C. 级联创建目录**  
如果想创建 **/samples/database/rdb** 目录（假设 **/samples/database** 不存在），通常要依序执行命令：
```
mkdir /samples/database
mkdir /samples/database/rdb
```
不过，你可以使用-p参数，直接说明要创建最深层次的目录，mkdir会自动依次建立依赖的父目录，如：
```
mkdir -p /samples/database/rdb
```

## 创建文件
大家可能都有过写Word文档文件的经验，在图形操作系统下这不是什么问题，但是在简陋的命令行窗口里，创建文件就不是件容易的事了。我们这里仅展示文本文件的创建。
### ★ **echo** 命令
>echo 一般是向控制台（窗口）输出文字（用'或"括起来）。但是，如果结尾添加>符号，后面指定文件全路径，则可以创建该文件，文件内容即为>符号前面的字符串。

**▷ A. 创建mysql.txt**

```
echo 'MySQL is a open-source database'>/samples/database/rdb/mysql.txt
```
如果命令运行正确，则什么也不返回。

**▷ B. 检查文件是否正确创建**

```
cat /samples/database/rdb/mysql.txt
```
返回输出结果如下，表明文件创建完全正确：
>MySQL is a open-source database


### ★ **touch** 命令
>touch 创建一个空文件

用 touch 创建一个名字为 oracle.txt 的文件到 **/samples/database/rdb/** 目录
```
touch /samples/database/rdb/oracle.txt
```
再用cat命令查看 oracle.txt ，如果什么也没返回（没有任何报错信息），即证明该文件存在，并且内容为空。