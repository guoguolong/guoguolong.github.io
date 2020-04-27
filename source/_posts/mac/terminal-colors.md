---
title: Mac自带的终端ls命令下文件与文件夹颜色单一的调整
tags: [mac]
date: 2018-11-037 14:00:12
categories: [IT]
---

macOS自带的终端是款非常好用的ssh工具，但ls命令下文件与文件夹都是单一的颜色，为了更好区分，作出修改。  
终端默认背景颜色为白色，(终端->偏好设置->描述文本)，可修改背景颜色与字体大小。  
运行下面的命令：

```
echo "echo export LS_OPTIONS='--color=auto'" # 如果没有指定，则自动选择颜色">>~/.bash_profile
echo "export CLICOLOR='Yes' #是否输出颜色">>~/.bash_profile
echo "export LSCOLORS='CxfxcxdxbxegedabagGxGx' #指定颜色">>~/.bash_profile

source ~/.bash_profile
```

ls目录颜色修改到这就ok了。其中绿色为文件夹。

详细说下LSCOLORS='CxfxcxdxbxegedabagGxGx'中的值代表的意思，这22个字母2个字母一组分别指定一种类型的文件或者文件夹显示的字体颜色和背景颜色。从第1组到第11组分别指定的文件或文件类型为：

```
directory #  文件夹目录
symbolic link
socket
pipe
executable
block special
character special
executable with setuid bit set
executable with setgid bit set
directory writable to others, with sticky bit
directory writable to others, without sticky bit
```

下面是颜色的字母对照：

```
a 黑色
b 红色
c 绿色
d 棕色
e 蓝色
f 洋红色
g 青色
h 浅灰色
A 黑色粗体
B 红色粗体
C 绿色粗体
D 棕色粗体
E 蓝色粗体
F 洋红色粗体
G 青色粗体
H 浅灰色粗体
x 系统默认颜色
```

所以，如果我们想把文件夹目录显示成红色，就可以把LSCOLORS设置为bxfxaxdxcxegedabagacad就可以了。

绿色粗体'CxfxcxdxbxegedabagGxGx'  
蓝色粗体'ExfxcxdxbxegedabagGxGx'