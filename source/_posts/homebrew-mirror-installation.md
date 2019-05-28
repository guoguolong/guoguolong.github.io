---
title: macOS下HomeBrew国内镜像安装
tags: [mac, homebrew]
categories: [IT, homebrew]
---

## 官网安装

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

上面是官网 https://brew.sh/ 安装Homebrew的方法，很遗憾国内网络常常安装失败，于是有了本文。

## 国内镜像安装

将官网安装分解为3步：

1. 下载安装脚本 
2. 修改安装脚本(更换镜像地址)
3. 运行安装脚本

### 下载安装脚本文件

下载 https://raw.githubusercontent.com/Homebrew/install/master/install 另存为文件名，比如命名为：brew_install。

### 修改安装脚本文件

修改 brew_install, 替换成清华大学的镜像，具体如下：

找到如下代码：
```
BREW_REPO = "https://github.com/Homebrew/brew".freeze
```

更改为：

```
BREW_REPO = "https://mirrors.ustc.edu.cn/brew.git".freeze
```

### 再次执行安装脚本

```
ruby brew_install
```

如果此时脚本应该停在

```
==> Tapping homebrew/core

Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...
```

出现这个原因是因为源不通，代码来不下来，解决方法是：要么使用科学上网，要么更换国内镜像源(中科院的镜像)，运行下面的命令：

```
git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1
```

然后把homebrew-core的镜像地址也设为中科院的国内镜像，运行下面的命令：

```
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

## 检查brew是否安装成功(可选)

```
brew update
brew doctor
```

## 更改更多默认源

以下是将默认源替换为国内 USTC 源的方法。 如下：

### 替换核心软件仓库

其实前文已经提及：
```
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

### 替换 cask 软件仓库（提供 macOS 应用和大型二进制文件）

```
cd "$(brew --repo)"/Library/Taps/caskroom/homebrew-cask
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```

### 替换 Bottles 源（Homebrew 预编译二进制软件包）

bash（默认 shell）用户：
```
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile
```

zsh 用户(少见)：

```
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
source ~/.zshrc
```

Done