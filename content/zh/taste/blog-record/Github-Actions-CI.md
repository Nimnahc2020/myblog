---
title: "利用 Github Actions 实现持续集成"
date: 2020-05-02T18:37:47+08:00
dropCap: false
displayCopyright: true
tags: ["Blog", "Git"]
series: ["notes-on-blog"]
aliases: ["/study/blog/Github-Actions/"]
toc: false
gitinfo: true
---

本文以 Hexo 博客为例，浅显地为你展现利用  Github Actions[^1] 来实现博客的持续集成（CI）以及持续部署（CD）[^2]。相信当你看完本文，了解文中各个步骤的具体含义后，其他类型博客的部署也会啦😎。

首先还是先聊一聊为什么要博客部署要用到 CI / CD，以及为何使用  Github Actions 来实现这个功能。

对我来说，捣鼓博客有关 CI / CD 的功能主要还是我始终秉持着以发现并实现新功能为乐的折腾精神🙃。但也不得不说，实现 CI / CD 功能后的确能为我们提供很多便利。那有哪些便利之处呢？一般我们部署 Hexo 博客时，得先通过`hexo g` 将写好的 Markdown 文件转化为 HTML 文件，然后再`hexo d` 把生成的 `public` 文件推送到 Github 仓库中，这样做真的很方便😳。..但是..，直接将生成的可以运行的实际代码（生产版）推送到 GitHub 仓库上，而不是博客源码（开发版），那这样便无法利用 GitHub 来对源码进行版本控制，也就不利于博客未来的维护、更新、开发，以及可能的开源开发。[^3]

大概意思就是：如果只把生成的可以运行的文件提交到你的博客仓库中，那么你就无法清楚地知道你过去对你的博客项目做了些什么！每一次提交代码的 `commit` 都会被 Github 记录下来，故而当你把源码储存在仓库中后，每一次的修改在以后都能找到相关档案，而且若有人抱着求知的心前往仓库查询你的相关设置时，源码能为其提供很大的便利，利人又利己，何乐而不为？😁

网上关于博客源码实现 CI / CD 的方法也有很多，我对这些方面也就一小白。最先接触到的就是通过 [Netlify](https://www.netlify.com/) 实现该功能[^4]。后面慢慢了解到了还有 [Travis CI](https://travis-ci.org/) 以及本文所涉及的 [Github Actions](https://github.com/marketplace?type=actions)。既然是把源码存放在 Github 的仓库上，那么就用 Github Actions 来实现呗！😝

谈了这么多，下面就开始吧！

## Github Actions

![Github Actions](/images/兴趣探索/建站笔记/Github-Actions.png "Github Actions")

[GitHub Actions](https://github.com/features/actions) 是 GitHub 于 2018 年 10 月[推出](https://github.blog/changelog/2018-10-16-github-actions-limited-beta/)的持续集成服务。

它的工作原理即为：当我们提前设置好需要自动化执行的任务（`.github/workflows` 下的文件）后，GitHub Actions 会监控当前仓库的某一个操作（如：`push`），一旦有此操作，就自动化执行这些任务。

我们设置的任务即为 `Action` ，它存放在博客根目录的 `.github/workflows` 下，后缀为 `.yml`。一个 Action 相当于是一个工作流 workflow，一个工作流则可以有多个任务 (`job`)，而每个任务又能分成几个步骤(`step`)。任务、步骤会依次执行。

现在代入 Hexo。我们把源码提交到了仓库的一个分支上，GitHub Actions 监听到了该分支的提交操作(`push`)，便会开始执行我们在 `.github/workflows` 下放置的文件中的代码。我们需要 GitHub Actions 执行的任务即为我们在根目录下执行的命令（如`hexo g`）。
{{< notice notice-info >}}
GitHub Actions 并没有我们的操作环境，我们得给它设置亦或是通过有关命令安装配置所需的环境。通过后面给出的任务文件内容可看出
{{< /notice >}}

## 准备工作

首先我们得获取 [GH_TOKEN](https://github.com/settings/tokens)，这东西能让 GitHub Actions 所构建得虚拟系统也可以对你的仓库进行操作。

![获取 GH_TOKEN](/images/兴趣探索/建站笔记/gh-token.png "获取 GH_TOKEN")

接下来添加仓库的变量（没啥好解释的），如图：

![添加变量](/images/兴趣探索/建站笔记/add_secrets.png "添加变量")

要添加的变量有：

* GIT_EMAIL（变量名）
* GH_TOKEN（变量名）

## Github 仓库

仓库设置有几点很重要。

先准备放代码的仓库。因为是使用 GitHub Actions 来完成 CI / CD，故部署平台即为 Github Pages，这里..强烈建议..仓库名设置为`username.github.io`。（我尝试过以 myblog 为仓库名，部署后得到的网址`https://willcai2020.github.io/myblog/`打开有很大问题[^5]）这样部署后你会得到一个形如：`https://username.github.io`的网址。

## 本地仓库—双分支

通常我们在`git init`后会有一个沉睡的 `master` 分支，一般我们之后的命令是唤醒`master`分支并把它提交给 Github 仓库（新建好后的仓库有指引`git push -u origin master`，就是默认先上传 `master` 分支）。在这里我们需要新增一个分支 `hexo` 用来存放源码，另一个分支用来存放经自动化任务内的`hexo g` 生成的 `public` 内的文件。

若你的根目录还未成为一个仓库，那么先执行：

```C
$ git init
```

然后关联远程仓库：（这里我用到了 SSH 多账号连接 Github 仓库的方法，具体可看我的[这篇文章](https://crcrc.me/taste/建站笔记/hugo_hexo/)）

```C
$ git remote add origin git@WillCAI2020.github.com:WillCAI2020/WillCAI2020.github.io.git
```

接着创建本地 `master` 分支（我的理解是 `git` 初始化后本地仓库还没有任何分支，那这个时候要先唤醒主分支 `master`，这样才能新建另外的分支。即先有主干后有枝干，至于最后谁逆袭成了主干那令当别论🙃）：

```
$ git add .
$ git commit -m "你想说明的信息"
```

然后执行命令 ` git branch` 就能发现项目中有了 `master` 分支。

这里为省去一点点麻烦，先唤醒远程仓库中的 `master`分支：

```C
$ git push -u origin master
```

然后新建并转到 `hexo` 分支：

```C
$ git checkout -b hexo
// 该命令相当于 git branch hexo 以及 git checkout hexo，前者是创建分支 hexo，后者是切换到 hexo分支。
```

最后把新创建的将新创建的分支信息推送到 Github：

```C
$ git push origin HEAD -u
```

推送后会发现仓库中有两个分支，一个为默认的`master`分支，另一个新建的`hexo`分支，且由于之前命令为`git add .` ，即把根目录中所有文件提交到暂缓区中，故而最终 `push`的文件是根目录中所有未被`git`忽视的文件。（之后自动化任务中的`git push --force --quiet "https://$GH_TOKEN@$REPO" master:master`能让生成的文件覆盖`master`分支中的文件，这样`master`分支中便是我们需要的`public`内的文件了）

## Actions 设置

在根目录下新建 `.github`，在其下面再新建 `workflows`，最后在其下新建任务文件（该任务是关于部署的，于是命名为 `deployment.yml`）就 OK 了。

```yaml
# 文件路径 .github/workflows/deployment.yml
name: Deployment

on:
  push:
    branches: [hexo] # only push events on source branch trigger deployment

jobs:
  hexo-deployment:
    runs-on: ubuntu-latest
    env:
      TZ: Asia/Shanghai

    steps:
    - name: Checkout source
      uses: actions/checkout@v2
      with:
        submodules: true

    - name: Setup Node.js
      uses: actions/setup-node@v1
      with:
        node-version: '12.x'
        
    - name: Install dependencies & Generate static files
      run: |
        node -v
        npm i -g hexo-cli
        npm i
        sed -i '18s/imageLink/imageLink.replace(\/\![0-9]{3,}x\/,"")/' themes/next/source/js/utils.js
        hexo clean
        hexo g
    - name: Deploy to Github Pages
      env:
        GIT_NAME: WillCAI2020
        GIT_EMAIL: ${{ secrets.GIT_EMAIL }}
        REPO: github.com/WillCAI2020/WillCAI2020.github.io
        GH_TOKEN: ${{ secrets.GH_TOKEN }}
      run: |
        cd ./public && git init && git add .
        git config --global user.name $GIT_NAME
        git config --global user.email $GIT_EMAIL
        git commit -m "Site deployed by GitHub Actions"
        git push --force --quiet "https://$GH_TOKEN@$REPO" master:master
```

该文件中的参数信息请查阅[这个文档](https://help.github.com/cn/actions/reference/workflow-syntax-for-github-actions)（是中文文档哦😁）。

为使该文件有更好的扩展性（也为了我这健忘的脑子），我这说明下其中一些操作的目的：

* `branches: [hexo]`：只监听`hexo`分支中的变动
* `npm i -g hexo-cli`：给虚拟机装上`hexo`操作环境
* `npm i`：安装 `package.json` 中所记录的插件
* `sed i`：[^6]查看[斑斑碎碎念 | 持续集成与缩略图](https://mirror.zdl.one/posts/44/)
* `hexo g`：通过这种方法生成`public`，若安装了`gulp`相关插件，则可替换为`gulp build`，其它类似。
* `REPO`：仓库地址一定要写对

最后提交修改：

```C
$ git add .
$ git commit -m "利用 Github Actions 持续集成"
$ git push origin hexo
```
{{< notice notice-warning >}}
在哪个分支下就`push`哪个分支，不要弄混`git push origin hexo`和`git push origin master`
{{< /notice >}}

最后前往仓库的 Actions，即可看到自动化任务正在进行，等待一会即可成功！🥂

若部署失败，请自行进入失败的任务项目，浏览部署日志，查找问题所在！💪

![寻找问题](/images/兴趣探索/建站笔记/Github-Actions-error.png "寻找问题")

本文属于我最先写的教程之一，有些地方可能讲解不清晰，亦或太过啰嗦，还请见谅！倘若觉得本文对你有所帮助，请把它转发给更多需要它的人，当然，不要忘了注明出处喔😄！

## 参考文章

[Git 创建新分支并提交到 Github](https://blog.csdn.net/daerzei/article/details/79530418)

[使用 GitHub Actions 实现 Hexo 博客自动部署](https://juejin.im/post/5e4ba6056fb9a07cbc268eed)

[GitHub Actions部署Hexo博客](https://note.junyangz.com/2019/GitHub-Actions-depoly-Hexo/)

[^1]: 关于 Github Actions 的介绍可浏览[这篇文章](http://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)
[^2]: CI / CD 的有关介绍可浏览[这篇文章](http://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)。
[^3]: 引于：[荷戟独彷徨 | 博客通过 Netlify 实现持续集成](https://guanqr.com/tech/website/deploy-blog-to-netlify/)
[^4]: 关于 Netlify 实现 CI /CD 可浏览我[这篇文章](https://crcrc.me/taste/建站笔记/Hexo+Next+Netlify打造个性超赞博客)，其中包含了一些大佬就 Netlify 写的文章。

[^5]:这大概率是我水平不够，毕竟[这位大佬](https://github.com/lei2rock/blog/tree/hexo)也是采用的这种方法。
[^6]:关于`sed i`的用法可浏览[这篇文章](https://www.cnblogs.com/xiaoliu66007/p/11059527.html)

