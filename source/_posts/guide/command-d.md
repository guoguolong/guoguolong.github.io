---
title: 程序员入行之素养(五)：一生万物、万物归一(命令行“删除”电脑资料)
tags: [入行, 预备课]
categories: [IT, 预备课]
date: 2019-01-18 10:00:00
---

## 删除文件
### **rm**命令
>**rm** 删除文件或目录

**▷ A. 删除文件**

```
rm /samples/culture/banyuan.txt 
```

**▷ B. 验证删除成功与否**

```
cat /samples/culture/banyuan.txt 
```
系统返回如下输出结果，表示rm操作成功：  
>cat: /samples/culture/banyuan.txt : No such file or directory

**▷ C. 删除文件前确认**

为谨慎起见，如果删除文件时想系统给出提示，用户确认后再决定删除与否，可以使用-i参数，运行命令：
```
rm -i /samples/langs/web.html
```
系统返回如下结果，输入Y或者N确认删除或不删除：
>remove /samples/langs/web.html

## 删除目录
### **rm**命令
>**rm** 删除文件或目录。 删除目录也使用rm命令，只是后面的的参数不同（-d或-r等）。

**▷ A. 删除目录**

```
rm -d /samples/web/orm
```
如果什么也没有返回，表明操作成功。

**▷ B. 验证删除成功与否**

```
ls /samples/web/orm
```
系统返回如下输出结果，表示rm操作成功：
>ls: /samples/web/orm: No such file or directory

**▷ C. 删除非空目录**

如果删除的目录下存在子目录或文件，执行rm -d会给出错误提示，如：
```
rm -d /samples/web/build
```  

>rm: /samples/web/build: Directory not empty

自然的想法是倒过来依序删除目标目录下的文件和子目录，然后再重新执行目标目录的删除。有一种更简单的方法是：使用-r参数，将直接将把目标目录及其下的所有子目录和文件删除：
```
rm -r /samples/web/build
```
如果命令执行正确，将不显示任何输出结果。

到这里，敏锐的读者可能已经想到：如果同时应用多个命令参数会有什么的结果？比如rm -ir ...，不妨自己行做个实验。

注：有些版本Mac系统运行rm时，默认给出确认提示（即：默认启用了-i），所以如果想取消确认提示，可以使用-f提示，-f不但支持文件，也支持目录。

**▷ D. 删除多个文件或目录**

rm命令后面说明多个 文件或目录全路径即可，如：
```
rm -f /samples/web/framework/expressjs.pdf f /samples/web/framework/springio.pdf
```

有个更简便的方法达到同样的目的，即使用正则表达式（Regular Expression），如：
```
rm -rf /samples/web/*.pdf
```
"*" 是正则表达式的规则之一，表示任意字符，上面命令行的含义是：删除 **/samples/web/** 目录下名字满足"任意字符加上.pdf字符"的条目。举一反三，find命令也是支持正则表达式的。