---
title: macOS下Sublime Text3的Linter插件配置
tags: [SublimeText]
date: 2019-06-04 13:07:09
categories: [IT]
---

Linter工具主要用来检查语言的代码风格和代码里的坏味道。这些工具通常可以独立或跟随构建工具一起使用，也可以集成到代码编辑器里使用。
Sublime Text3的 [SublimeLinter](https://packagecontrol.io/packages/SublimeLinter)插件功能强大，基于它开发的各种语言Lint插件功能卓越，本文主要介绍 ESLint、stylelint、htmlint 的插件使用。

## 前置知识

假设你已经安装了Sublime Text（包括SublimeLinter插件）、Node.js 8以上环境，熟悉node、npm以及现代Web前端开发工程组织（并已经有一个实验的前端项目工程），熟悉Sublime Text3的插件管理，否则阅读下文会比较吃力。

## ESLint

ESLint主要用于检测ECMAScript/JavaScript的代码风格和语法合规性，类似JSLint或者JSHint，不过后面两者已经不再流行。
官网 https://eslint.org/ 关于如何独立使用ESLint，介绍得相当通俗易懂，我们这里着重介绍其Sublime Text插件的用法。

### 安装[SublimeLinter-ESLint](https://packagecontrol.io/packages/SublimeLinter-contrib-eslint)

在工程目录下安装ESLint先：
```
npm install eslint --save-dev
```

然后安装SublimeLinter-ESLint插件。

打开 Preferences->Package Settings->SublimeLinter->Settings，输入内容如下：

```
{
    "lint_mode": "save",
    "paths": {
        "osx": [
            "/usr/local/bin"
        ]
    },
    "linters": {
        "eslint": {
              "selector": "text.html.vue, source.js - meta.attribute-with-value"
        }
    }
}
```
* lint_mode:save：意为仅在js文件存储的时候，才进行lint检查，否则打开工程只要发现lint配置，就会整个工程检查所有Js文件的，那可耗时了。
* paths:osx:/user/local/bin 是指向node所在的目录。
* linters:eslint:selector：这里的说明使lint支持vue文件。

### 使遵从airbnb的JavaScript规范

安装[Airbnb JavaScript规范](https://github.com/airbnb/javascript)非常时髦，安装其lint插件：
```
 npm i eslint-config-airbnb-standard --save-dev
```

在实验工程目录下创建 .eslintrc （或者.eslintrcjs）文件，内容如下：

```
{
    "extends": ["airbnb-standard"]
    "rules": {
        "indent": ['error', 4]
    }
}
```

写一个JavaScript文件试试，存储时ESLint将遵从airbnb-standard检查，rules里可以定制项目自己的规则，比如上面的例子：大部分规则都遵从airbnb，但是缩进空格是四个（airbnb缩进的两个空格）。

## stylelint

跟ESLint很类似， 官网 https://stylelint.io/ 的独立使用直接了当，我们重点仍然放在Sublime Text的插件使用。

### 安装 [SublimeLinter-stylelint](https://packagecontrol.io/packages/SublimeLinter-stylelint) 插件

在实验工程目录下安装stylelint先：
```
npm install postcss stylelint --save-dev
```

然后安装SublimeLinter-stylelint插件。

### 配置项目使用[stylelint-config-recommended](https://github.com/stylelint/stylelint-config-recommended) css规范

在实验工程目录下安装 stylelint-config-recommended 

```
npm install stylelint-config-recommended --save-dev
```

在项目根目录下创建文件 .stylelintrc，内容如下：

```
{
    "extends": "stylelint-config-recommended"
    "rules": {
        "at-rule-no-unknown": [ true, {
          "ignoreAtRules": [
            "extends"
          ]
        }],
        "block-no-empty": null,
        "unit-whitelist": ["em", "rem", "s"]
    }
}
```
上面例子规则是：默认使用 stylelint-config-recommended 规则，然后在此基础上定制项目自有规则，如：尺寸单元只能使用em、rem、s等，如果设置width: 20px；这个px就是不合规的。

在Sublime Text里写一个css文件，存储一下试试，看上面的规则是否生效。

>注：如果存储文件时，Sublime Text状态条显示err，总是按照ctrl + \`打开控制台看详细错误信息。

## htmllint

未完待续...

