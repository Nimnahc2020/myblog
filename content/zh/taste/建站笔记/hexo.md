---
title: "Hexo"
date: 2020-04-30T22:57:32+08:00
toc: true
tags: ["Hexo"]
series: ["博客小记"]
aliases: ["/study/blog/hexo_new_sky/"]
gitinfo: true
dropCap: false
draft: true
---

## 前言

<blockquote class="quote">
本文篇幅较长，为了阅读方便，开头加上了可与文章内容相互链接的标题（可双向跳转）
</blockquote>

建立博客对我来说是一件新奇的事物，尤其是还能在原本空空如也的界面内加上许多有意思的功能，而为了实现各种各样的功能，我们需要查阅许多大佬的文章，在这些过程中我们会遇到各种各样的问题，而解决这些问题的过程就是提升的过程。在此尤其要感谢分享自己建站教程的博主大佬们。

对博客的各种折腾是我的一种精神追求，而对我来说，能将我对 Next 主题的个性优化中所用的方法记录并分享出来是一件令人愉悦的事。文中方法源于互联网中的大佬，并依据实际情况有所改动。

---

随着互联网的普及，个人博客的数量也越来越多，网上用来搭建个人博客的框架大多是 [Hexo](https://hexo.io/)，Hexo 有许多主题，其中 [Next ](https://github.com/theme-next/hexo-theme-next) 主题是 Github 上 Stars 最多的主题。我浏览过许多博主的个人博客，发现这些博客大多源于 Next 主题。 Next 背后有着一个专业且默默奉献的团队，主题在不断更新，出现的问题其后的团队也会尽快解决，配合上 Hexo  支持的诸多插件，我们便能利用 Hexo + Next 打造出一个属于自己的个性超赞博客！

本文将为你详细地展现最新的 Hexo 博客的搭建过程和 Next 主题的安装与配置以及现拥有的相关个性优化。值得说明的是，我是一个很白的小白，刚接触 C，对于优化过程所接触到的各种 JavaScript，HTML，CSS 等更是一窍不通，能写出这篇文章的底气不过是源于实际操作得到的结果以及许多大佬的相关详细教程，倘若你也是一个小白，那么不用怕，跟着本文一起做，你也能拥有一个超赞的博客啦！

若有大佬赏阅本文，文中方法有所不足还请见谅！若能指出不足，亦或提出更佳的优化方案，在下感激不尽！

文中所参考的各种方法会给出相关来源链接，由于参考文章过多，有些链接未及时收藏，若有遗漏，欢迎指出。

**在此建议**：将博客每一步所采取的方法步骤大概记录下来，比如添加亦或修改了哪个文件，并把相关文章收藏整理下来，这样以后想修改相关功能时，心中能更明确应改动哪部分文件；此外这还利于进一步调整优化博客，以及博客功能的更新。若在网上发现了令你眼前一亮的个性超赞博客，一定要记得收藏，且这类博客的博主一般会有讲述其博客的搭建历程。

{{< notice notice-note >}}
网上关于 Next 主题优化的好文章有很多，但随着 Next 主题的更新，总有些教程会过时从而失效亦或有更好的优化方法（一些功能会成为 Next 主题自带的一部分，或被主题抛弃）。本文的一些方法同样会因过时或方法本身的错误而导致无法达到预期效果，故而文中内容..仅供参考..。倘若遇到无法解决的问题，请参考 Next [官方文档](https://theme-next.org/)相关说明或前往 Next 的 [Issues](https://github.com/theme-next/hexo-theme-next/issues) 区查询或提交相关问题。
{{< /notice >}}

## 准备工作

搭建 Hexo 需具备 [Node.js](https://nodejs.org/zh-cn/) 和 [Git](https://git-scm.com/) 两种环境，具体安装方法网上有很多，在此给出我遵循的教程：

* [Node.js 安装配置](https://www.runoob.com/nodejs/nodejs-install-setup.html)
* [Git 安装教程（Windows安装超详细教程）](https://www.jianshu.com/p/414ccd423efc)

注意：安装时最好前往官网获取最新版本，否则后续步骤可能出错。（Node.js 使用长期支持版即可）

打开 cmd ，分别输入 `node -v` 和 `npm -v` 以及 `git --version`，确保相关环境搭建成功。如果出错请百度或谷歌相关问题。

下面给出我的操作环境：

```markdown
$ node -v
v12.16.1
$ npm -v
6.13.4
$ git --version
git version 2.25.1.windows.1
```

## 开始 搭建 Hexo 博客

网上关于如何搭建 Hexo 博客的教程有很多，因此我在该节只是简略介绍 Hexo 的搭建，同时附上搭建后的心得。

### 本地安装 Hexo

安装过程可直接参考 Hexo [官方文档](https://hexo.io/zh-cn/docs/)。可输入`hexo v`获取版本信息：

```markdown
$ hexo v
hexo: 4.2.0
hexo-cli: 3.1.0
os: Windows_NT 10.0.18363 win32 x64
node: 12.16.1
v8: 7.8.279.23-node.31
uv: 1.34.0
zlib: 1.2.11
brotli: 1.0.7
ares: 1.15.0
modules: 72
nghttp2: 1.40.0
napi: 5
llhttp: 2.0.4
http_parser: 2.9.3
openssl: 1.1.1d
cldr: 35.1
icu: 64.2
tz: 2019c
unicode: 12.1
```

安装好 Hexo 后，选择一个目录并新建一个文件夹，用来放入有关 Hexo 的所有文件。（因之后需要多次修改其中文件，故建议选择易寻的路径建立文件夹）

比如我准备在`路径:D:\Github\Nimnahc2020\hexo-next`放入我的 Hexo 文件。进入新建好的`hexo-next`，右键单击选择`Git Bash Here`进入 Git 操作界面。输入命令：

```markdown
$ hexo init
```

输入后需稍等一会，若操作界面出现橙色的 WARN 没关系，只要不出现红色的 ERROR 就行。看到提示`INFO  Start blogging with Hexo! `即为 Hexo 初始化成功。
{{< notice notice-note >}}
在哪个文件下执行了 `hexo init`，这个文件就是根目录
{{< /notice >}}
介绍下 Hexo 的三部曲：

```c
$ hexo clean	// 清理缓存
$ hexo g		// 生成静态文件
$ hexo d		// 部署到 Github 上，若只是本地预览则把这一步换为 hexo s
注：hexo d 只有在安装部署插件 hexo-deployer-git 后才可实现
```

在根目录`hexo-next`下输入命令：

```markdown
$ hexo g && hexo s
```

然后点开 [http://localhost:4000/](http://localhost:4000/)，若你面前出现了一个无比简陋的界面，那么恭喜你！你已经在本地搭建好一个博客了，接下来要做的就是部署博客并为你的博客挑选一个好看的主题。

此外，你还会发现根目录下多出来了 `public` 和 `.gitignore` 以及 `db.json` 三个文件。其中`public`存放了生成的页面，`.gitignore` 中记录的文件是 Git 命令上传博客源码至仓库的时被忽略上传的文件。`db.json` 则是 `source` 文件夹解析得到的。

### 配置

在此建议记录下 Hexo 初始后生成哪些文件：[^1]

```c
.
├── _config.yml		// ..站点..配置文件
├── node_modules		// 依赖包
├── package.json		// 项目所需模块项目的配置信息
├── package-lock.json	// 当前安装的库的..具体..来源和版本号
├── scaffolds			// 命令生成文章等的模板
|		└── draft.md
|		└── page.md
|		└── post.md
├── source			// 用命令创建的各种文章
|   	└── _posts
└── themes			// 主题
   		└── landscape
```

初始化后 Hexo 安装所具有的配置为：

```json
"dependencies": {
  "hexo": "^4.0.0",
  "hexo-generator-archive": "^1.0.0",
  "hexo-generator-category": "^1.0.0",
  "hexo-generator-index": "^1.0.0",
  "hexo-generator-tag": "^1.0.0",
  "hexo-renderer-ejs": "^1.0.0",
  "hexo-renderer-stylus": "^1.1.0",
  "hexo-renderer-marked": "^2.0.0",
  "hexo-server": "^1.0.0"
}
```

在之后在根目录下每安装一个插件（安装插件都要先到这个目录），`package.json`中便会更新出该插件的信息，插件的相关文件会放在`node_modules`文件中。建议记录下之后新增的插件信息及其功能。

### 部署博客

### Github Pages

网上有很多关于博客部署在 GitHub Pages 的教程，在此贴出两位大佬的文章：

* [reuixiy | 部署博客到 GitHub Pages](https://io-oi.me/tech/hexo-next-optimization/#contents:部署博客到-github-pages)
* [荷戟独彷徨 | Github-Pages](https://guanqr.com/tech/website/hexo-theme-next-customization/#github-pages)

这两篇文章的讲述都非常详细，大家可参照文中方法实现在 Github Pages 上的部署。

同时还是给出注意事项：

* GitHub 上创建的仓库名应为 `username.github.io`。`username` 为你的 GitHub 账号用户名。
* `repository`有两种设置方式：
  * HTTPS 路径：` https://github.com/username/username.github.io.git`
  * SSH 路径：`git@github.com:username/username.github.io.git`

两种方法大概区别：[Git 中 Https 和 SSH 的 clone 方式区别](https://www.jianshu.com/p/2cced982009f)

### Github + Netlify

#### Netlify

Netlify 有很多优点：

* 具有静态网站托管的功能，能够托管 GitHub，GitLab 等网站上的 Jekyll，Hexo，Hugo 等静态网站。
* 自动启用 CDN 加速
* 实现持续集成（Continuous Integration，CI）和自动部署（当你提交改变到 Git 仓库，它就会自动运行`build command`，进行自动部署）。
* 可以自定义域名
* 可以启用免费的通配符证书 + TLS 1.3,启用 HTTPS
* ......

Github 在国内的访问速度以前的确很慢，但近来 Github 表示要进入中国，访问速度虽说还是较慢，但也属于可接受的范围。网上也有很多通过 Netlify 加速 Github 的教程，而对于 Netlify 的访问速度，我感觉与在 Github Pages 部署时没太大区别，毕竟二者的服务器都不在国内。但由于有 PWA 功能，在访问时我感觉还挺不错，没有太大的卡顿延迟。

现很多博主都转而采用 Netlify 部署博客，主要原因应该在于持续集成以及自动部署。
{{< notice notice-tip >}}
直接通过 Hexo 三部曲同样可以完成 Github + Netlify 的部署，这样做虽然方便，但这样只是将根目录下的`public`文件夹提交到了仓库，这样并不利于博客以后的维护、更新、开发，以及可能的开源开发。若要选择这种方法，可浏览这篇文章：[Hexo + Github + Netlify 部署个人博客](https://juejin.im/post/5cc17ed26fb9a032374f5200)
{{< /notice >}}

接下来介绍直接通过提交根目录文件实现 Github + Netlify 的持续集成部署。

#### 步骤

同样，首先在 Github 上新建一个仓库，这个仓库名可随意取，比如我取的是`myblog`。

接着把本地仓库上传至 Github 的`myblog`中，这里我采用的是 SSH 连接方式，相关方法可浏览我写的一篇文章：[SSH 之 Github（单/多账号）](https://crcrc.me/taste/建站笔记/hugo_hexo/)。

先 Git 初始化根目录：（把根目录变成一个本地仓库→生成`.git`）

```C
$ git init
```

再连接远程仓库：

```C
$ git remote add origin git@WillCAI2020.github.com:WillCAI2020/myblog.git
```

然后提交本地仓库：

```C
$ git add .
$ git commit -m "first commit"
$ git push -u origin master
```



然后登陆 [Netlify](https://www.netlify.com/)，点击`Sign in`，选择 Github 并授权即可。

![注册](/images/兴趣探索/建站笔记/netlify_sign_in.png "注册")

随后点击`New site from Git`，从中选则之前用来存储本地根目录文件的仓库。

![new site](/images/兴趣探索/建站笔记/netlify-github.png )


[^1]:文件相关介绍可浏览这篇文章：[Hexo 的目录结构](https://www.jianshu.com/p/17d55d420d94)
[^2]:[荷戟独彷徨 | 博客通过 Netlify 实现持续集成](https://guanqr.com/tech/website/deploy-blog-to-netlify/)