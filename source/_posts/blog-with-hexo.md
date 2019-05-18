---
title: 用Hexo + Github搭建个人博客
tags: [blog, hexo, git, submodule]
categories: [IT, hexo]
---

* [Hexo](https://hexo.io/zh-cn/)是一个博客框架，基于Node.js，用Markdown创作博客内容，Hexo将其翻译成布局精美的静态HTML。
* [GitHub Pages](https://pages.github.com/)，创建好的博客文章(网页)可以发布到 GitHub Pages。
* [Git](https://git-scm.com/) 一个分布式代码版本控制工具


## 用Github写博客

### github.com上创建账号

在github.com上创建一个账号，比如叫：lixiaobai.

### github.com上创建仓库

创建一个代码仓库，名字必须为：<你的账户名>.github.io 用来存放博客文章。以上面的账户为例，你的仓库名就应该为：lixiaobai.github.io，然后通过浏览器访问 https://lixiaobai.github.io 就可以访问自己的博客了。

最开始，你的访问可能空空如也。向该代码仓库里增加 hello.md，内容为：

```
# Welcome Li Xiaobai.
```
浏览器访问 https://lixiaobai.github.io/hello.html ，看看效果怎么样。

思考一下博客工作的过程：你写了一篇Markdown文件hello.md，但是却通过hello.html访问了它的内容，怎么做到的呢？其实也不难理解，GitHub Pages实际上做了自动翻译工作，预先将hello.md翻译成了hello.html。

## 用Hexo写精美的博客

GitHub Pages官方采用了[Jekyll](https://jekyllrb.com/)博客框架，编译的HTML可以使用各种漂亮的主题，不过功能还不够强大，所以我选择Hexot替代Jekyll。

本文并不打算介绍Hexo的安装和配置，如果你懂Node.js和Markdown，官网 https://hexo.io 的文档已经足够清楚；如果你不懂Node.js，说给你，你也用不了。

用Hexo写完博客，使用hexo g -d命令将其发布GitHub Pages。它实际分成了两步：

* 把博客内容翻译了 html 文件；
* 用git把html发布到名字为 lixiaobai.github.io 的 GitHub 仓库的 master 分支（这一步需要做对应的设置）

## 博客的管理

### 源文件和编译文件

* 你应该为 lixiaobai.github.io 仓库创建一个分支，如 blog，将博客源文件保存到该分支；
* 总是在 blog 分支编写博客，然后通过hexo d -g 发布到 master 分支。

### 更好的主题

hexo 默认主题不合我意，还是：[Next](https://theme-next.org/) 漂亮。 再漂亮的主题也可能需要个性定制。因此将 https://github.com/theme-next/hexo-theme-next fork到自己的账户里，lixiaobai fork出来名字应为： https://github.com/lixiaobai/hexo-theme-next , 便于后续更改保存。

建议使用 git submoudle 管理 Next 主题，进入hexo工程目录运行：

```
git submodule add https://github.com/lixiaobai/hexo-theme-next.git themes/next
```

>下次在其他地方clone项目要使用 git submodule update --init --recursive 更新， 更多关于submodule看[这里](/git/submodule.html)



