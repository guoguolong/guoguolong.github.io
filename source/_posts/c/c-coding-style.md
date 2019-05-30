---
title: Google C Style和Sublime Text的C插件
tags: [C]
categories: [IT, C]
---

代码风格：C代码风格遵从 [Google C Style](https://google.github.io/styleguide/cppguide.html) 事半功倍。

工具：我用Sublime Text写C代码，其格式化插件，几乎只能使用 [SublimeAStyleFormatter](https://packagecontrol.io/packages/SublimeAStyleFormatter)，不过已经足够了，而且足够的好。

## 安装Sublime下的SublimeAStyleFormatter插件

SublimeAStyleFormatter 主要关注在C、Java代码格式化。

Mac OS下打开Sublime Text，按CMD + SHIFT + P，弹出窗口输入install，下拉列表第一个显示的条目是："Package Control: Install Package"，选中按回车键，输入 SublimeAStyleFormatter ，甚至只输入部分文字就会下拉列出该插件的名字，选中然后按回车键，稍等片刻，安装完毕。

>***1. 什么？按CMD + SHIFT + P，输入install的时候就卡住，你没有看到这个下拉条目？***   
>这是你应该去 https://packagecontrol.io 首先安装 Sublime Text 的插件的管理工具。
>
>***2. 什么？按CMD + SHIFT + P完全没有反应？***  
>Terrible，你不得不先学会科学上网！

## SublimeAStyleFormatter的基本用法

写一段C代码
```
#include <stdio.h>

int main(void)
{
printf ("Hello World\n") ;
int sum =3+4;
return 0;
}}Ï
```

打开右键菜单 AStyleFormater->Format（快捷键：CMD + OPTION + F），点击确认后格式成：
```c
#include <stdio.h>

int main(void)
{
    printf ("Hello World\n") ;
    int sum = 3 + 4;
    return 0;
}
```

的确好看了不少，不过还不足够，比如prinf函数和(之间有一个多余的空格，另外缩进是TAB，不是我想要的4个spaces。怎么办？

分别打开插件设置：Preferences->Package Settings->SublimeAStyleFormatter->Settings - Default 和 Settings - User，将Settings - Default里项修改的项复制到Settings - User里进行修改，如下：

``` json
{
    "options_default": {
        "indent": "spaces",
        "indent-spaces": 4,
    }
}
```
保存后再格式化一次，看看缩进的TAB是不是变成了4个spaces。

## SublimeAStyleFormatter使用Google C Style

我的项目代码遵从了 [Google C Style](https://google.github.io/styleguide/cppguide.html)(Google的代码风格指南开源在 https://github.com/google/styleguide )，Oops，那么多代码格式设定看来都要在 SublimeAStyleFormatter 里设置。

参考 SublimeAStyleFormatter文档（开源在 https://github.com/timonwong/SublimeAStyleFormatter ），文档介绍极其简单，原来它是基于 [Artistic Style](https://sourceforge.net/projects/astyle/)，其实是要学会 Artistic Style 如何设置代码风格，然后将设置参数存成一个文本文件，如 .astylerc，然后被 SublimeAStyleFormatter 引用即可。

符合Google C Style的Artistic Style参数设置如下：
```
--style=google

--indent=spaces=4

--attach-namespaces
--attach-classes
--attach-inlines

--add-brackets

--align-pointer=name
--align-reference=name

--max-code-length=200
--break-after-logical

--pad-oper
--unpad-paren

--break-blocks
--pad-header
```
文件存储为.astylerc，放到家目录，插件的Settings - User再次修改为：

```
{
    "options_default": {
        "indent": "spaces",
        "indent-spaces": 4,
    },
    "options_c": {
        "additional_options_file": "$HOME/.astylerc"
    },    
}
```
>注：$HOME就指代你的家目录

再按快捷键 CTRL + OPTION + F格式化代码，看看是不是变成下面这样：
```c
#include <stdio.h>

int main(void) {
  printf("Hello World\n") ;
  int sum = 3 + 4;
  return 0;
}
```

DONE，完美！
