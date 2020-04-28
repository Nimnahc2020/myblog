---
title: "Gitbook"
date: 2020-04-27T19:55:03+08:00
dropCap: false
displayCopyright: false
tags: ["Gitbook"]
toc: false
gitinfo: false
draft: true
---

## 安装 Gitbook 
```C
$ npm install gitbook-cli -g	# 全局安装 Gitbook
```
安装后即可调用 Gitbook 的相关命令。可`cmd`下输入`-v`查看 Gitbook版本，以此确定成功安装：
```C
$ gitbook -V
CLI version: 2.3.2
GitBook version: 3.2.3
```
成功安装后，选择一个存放你的 GitBook 书籍的文件夹，在该文件夹下打开 Git 命令行：
```C
$ gitbook init		# 初始化书籍目录
```
初始化后，该文件夹中会生成两个文件，分别是`README.md`和`SUMMARY.md`，这是两个必要文件。其中`README.md`是对书籍的简单介绍,`SUMMARY.md`则是书籍的目录结构。

初始`README.md`内容：
```C
$ cat gitbook/README.md 
# Introduction
```
初始`SUMMARY.md`内容：
```C
$ cat gitbook/SUMMARY.md
# Summary

* [Introduction](README.md)
```

## README 的书写格式
```C
# README

This is a book powered by [GitBook](https://github.com/GitbookIO/gitbook).
```
其中`README`以及其后的内容自行编辑即可。

## SUMMARY 的书写格式
`SUMMARY.md`是一本书的目录结构：
```C
# SUMMARY

* [Chapter1](chapter1/README.md)
  * [Section1.1](chapter1/section1.1.md)
  * [Section1.2](chapter1/section1.2.md)
* [Chapter2](chapter2/README.md)
```
可以通过使用..标题..或者..水平分割线..标志将 GitBook 分为几个不同的部分：
```C
# Summary

### Part I

* [English](README.md)
* [English_one](part1/one.md)
* [English_two](part1/two.md)

### Part II

* [Math](README.md)
* [Math](part2/one.md)
* [Math](part2/two.md)

----

* [Last part](part3/README.md)
```

## 了解 GitBook 命令
```C
gitbook init    //初始化目录文件
gitbook help    //列出gitbook所有的命令
gitbook --help  //输出gitbook-cli的帮助信息
gitbook build   //生成静态网页
gitbook serve   //生成静态网页并运行服务器
gitbook build --gitbook=2.0.1   //生成时指定gitbook的版本, 本地没有会先下载
gitbook ls  //列出本地所有的gitbook版本
gitbook ls-remote   //列出远程可用的gitbook版本
gitbook fetch 标签/版本号   //安装对应的gitbook版本
gitbook update  //更新到gitbook的最新版本
gitbook uninstall 2.0.1     //卸载对应的gitbook版本
gitbook build --log=debug   //指定log的级别
gitbook builid --debug  //输出错误信息
```
注意：gitbook serve 命令长久以来被发现不稳定，时常产生 ENOENT 错误。解决办法:将`copyPluginAssets.js`文件最后一个`fs.copyDir`中`confirm`项的值由`true`改为`false`。Windows 上该文件的路径通常形如:`C:/Users/[用户名]/.gitbook/versions/[Gitbook 版本号]/lib/output/website/lib/output/website/`。

## 预览 GitBook
当你在自己的电脑上编辑好相关内容后，你可以使用 GitBook 的命令进行本地预览：
```C
$ gitbook serve
```
运行命令后会启动一个端口为`4000`用于预览的服务器：http://localhost:4000。

且该文件夹下会生成一个名为`_book`的文件，而这个文件中的内容，即是生成的静态网站内容。

## 配置 Gitbook
这需要一个文件`book.json`，该文件包含了你编写的这本书中的基本信息。在 GitBook 项目根目录下新建`book.json`即可。

`book.json`包含的主要内容有：
* `title`：书籍名称
* `author`：作者
* `description`：书籍描述
* `language`：当前书籍语言
* `gitbook`：欲调用的 GitBook 版本号
* `links`：设置主页链接，显示在侧栏
* `styles`：页面 CSS 样式
* `structure`：关键文件位置
* `plugins`：插件加载
* `pluginsConfig`：插件参数

例如：
```C
{
    "title": "Study",
    "author": "ruchan",
    "description": "note for everything",
    "language": "zh-hans",
    "gitbook": "3.2.3",
    "links": {
        "sidebar": {
            "我的主页": "https://crcrc.me"
        }
    },
    "styles": {
        "website": "./styles/website.css"
    },
    "structure": {
        "readme": "README.md"
    },
     "plugins": [
        "-sharing","sharing-plus",
        "highlight",
        "-lunr", "-search", "search-pro",
        "splitter",
        "collapsible-menu",
        "katex",
        "code",
        "github", "github-buttons",
        "tbfed-pagefooter",
        "back-to-top-button",
        "anchors"
    ],
    "pluginsConfig": {
        "theme-default": {
            "showLevel": true
        },
        "sharing": {
            "douban": false,
            "facebook": false,
            "google": false,
            "hatenaBookmark": false,
            "instapaper": false,
            "line": false,
            "linkedin": false,
            "messenger": false,
            "pocket": false,
            "qq": false,
            "qzone": false,
            "stumbleupon": false,
            "twitter": false,
            "viber": false,
            "vk": false,
            "weibo": false,
            "whatsapp": false,
            "all": [
                "douban","qzone","weibo","facebook", "google", "twitter"     
            ]
        },
        "github": {
            "url": "https://github.com/Nimnahc2020"
        },
        "github-buttons": {
            "buttons": [{
                "user": "Nimnahc2020",
                "repo": "gitbook",
                "type": "star",
                "size": "small",
                "count": true
                }
            ]
        },
        "tbfed-pagefooter": {
            "copyright":"&copy ruchan",
            "modify_label": "最后修改于：",
            "modify_format": "YYYY-MM-DD"
        },
    }
}