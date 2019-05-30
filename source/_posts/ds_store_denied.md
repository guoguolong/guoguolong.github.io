---
title: 禁止.DS_store生成
tags: [mac]
categories: [IT]
---

.DS_Store，英文全称 Desktop Services Store，是Mac OS中保存文件夹自定义属性的隐藏文件，目的在于存贮文件夹的自定义属性，例如文件图标位置、视图设置，或背景色等，相当于Windows下的 desktop.ini。.DS_Store 默认放在每个文件夹的下面，这给我们带来了诸多不便，例如：

* 压缩包里每个文件夹都带有.DS_Store文件，在windows系统里面成了垃圾文件；
* git、svn之类的版本管理工具要额外的对这种文件进行忽略处理；
* 如果是要发布到服务器的文件夹，可能会形成文件泄露漏洞。

在 macOS High Sierra 之后，我们看到苹果对此做出了优化，即使你在finder中使用快捷键 Shift + Command (⌘) + . 来显示隐藏文件 ，finder也不再显示隐藏的.DS_Store文件，但是在终端中，我们还是可以用 ll命令看到它的身影，苹果这是要掩耳盗铃吗？
那我们有什么办法来禁止.DS_Store的生成呢？网上流传的禁止.DS_Store生成方法是使用命令：

>defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE

但是这个命令只有在网络共享的时候有效，也就是在本地无效。比如拖动一下图标的位置或者标记一下就会自动生成了，不是我们所理想的禁止生成，所以还是需要针对本地进行处理。

**是时候出动 Asepsis 这把瑞士军刀了！**

一直以来，Asepsis 都是我在mac OS 上必装工具之一，它会阻止Finder将.DS_Store文件写入文件夹。 Asepsis的工作原理是拦截所有.DS_Store文件的创建或写入，并将它们重定向到 /usr/local/.dscage。 这样 Finder 如常工作，且不会有这种无用文件污染文件系统。
不幸的是，在 OS X 10.11 El Capitan 发布之后，Apple 启用了 [System Integrity Protection (SIP)](https://en.wikipedia.org/wiki/System_Integrity_Protection)，它会阻止 Asepsis 的安装和正常运行。Asepsis 的作者已经放弃了对它的后续支持，因为他不希望用户为了使用这个工具而禁用系统关键安全服务。

那有什么办法呢？

**事实上我们可以在保持SIP启用的情况安装 Asepsis ！**

## 1) 安装 Asepsis
首先，打开终端并运行以下命令：

```
touch ~/.no-asepsis-os-restriction
touch ~/.asepsis-suppress-update-errors
```

目的是绕过Asepsis的内置兼容性检查，因为它不能识别 El Capitan 之后的版本。

现在 你可以从[官网](http://asepsis.binaryage.com/)安装最新版本的Asepsis（截至2016年2月为1.5.2）。 运行安装程序，它提示你重新启动，这时SIP会阻止工具的运行。

## 2) 进入恢复模式并禁用 SIP

重启电脑，按住 Command (⌘) + R 键进入 恢复模式。

看到 macOS 实用工具 屏幕后，转到屏幕顶部的 实用工具 下拉菜单，然后选择 终端 ，输入：

```
csrutil disable; reboot
```

等待电脑重启。

## 3) 安装 Asepsis

返回非恢复模式后，打开终端并运行以下命令安装Asepsis

```
asepsisctl install
```

>如果发现警告 wrapper already existing，有可能之前已经安装过Asepsis，此时尝试运行 asepsisctl uninstall_wrapper 然后重新运行 asepsisctl install。

## 4) 重新启用 SIP
重启并按住 Command (⌘) + R 进入恢复模式，运行命令：

```
$ csrutil enable; reboot
```

## 5) 验证 Asepsis 是否工作

重启后运行命令：

```
$ asepsisctl diagnose
```

如果正常的话你会看到：Your Asepsis installation seems to be OK.

>赠送命令：

```
# 删除系统所有.DS_Store文件  
sudo find / -name ".DS_Store" -depth -exec rm **{}** \;  
# 删除当前目录以及子目录的DS_Store文件  
find . -name ".DS_Store" -delete  
```

转自： https://www.jianshu.com/p/f83e85443c50