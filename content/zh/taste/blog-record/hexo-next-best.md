---
title: "Hexo"
date: 2020-04-23T22:57:32+08:00
toc: true
tags: ["Hexo","Blog"]
series: ["notes-on-blog"]
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

#### Github Pages

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

#### Github + Netlify

##### Netlify

Netlify 有很多优点：

* 具有静态网站托管的功能，能够托管 GitHub，GitLab 等网站上的 Jekyll，Hexo，Hugo 等静态网站。
* 自动启用 CDN 加速
* 实现持续集成（Continuous Integration，CI）和自动部署（当你提交改变到 Git 仓库，它就会自动运行`build command`，进行自动部署）。
* 可以自定义域名
* 可以启用免费的通配符证书 + TLS 1.3,启用 HTTPS
* 自带 CI、支持自定义页面重定向、自定义插入代码、打包和压缩 JS 和 CSS、压缩图片、处理图片
* ......

Github 在国内的访问速度以前的确很慢，但近来 Github 表示要进入中国，访问速度虽说还是较慢，但也属于可接受的范围。网上也有很多通过 Netlify 加速 Github 的教程，而对于 Netlify 的访问速度，我感觉与在 Github Pages 部署时没太大区别，毕竟二者的服务器都不在国内。但由于有 PWA 功能，在访问时我感觉还挺不错，没有太大的卡顿延迟。
{{< notice notice-tip >}}
直接通过 Hexo 三部曲同样可以完成 Github + Netlify 的部署，这样做虽然方便，但这样只是将根目录下的`public`文件夹提交到了仓库，这样并不利于博客以后的维护、更新、开发，以及可能的开源开发。若要选择这种方法，可浏览这篇文章：[Hexo + Github + Netlify 部署个人博客](https://juejin.im/post/5cc17ed26fb9a032374f5200)
{{< /notice >}}

接下来介绍直接通过提交根目录文件实现 Github + Netlify 的持续集成部署。

##### 操作步骤

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

完成 Github 代码仓库的相关操作后，我们开始进行 Netlify 的相关操作。

登陆 [Netlify](https://www.netlify.com/)，点击`Sign in`，选择 Github 并授权即可。

![注册](/images/兴趣探索/建站笔记/netlify_sign_in.png "注册")

随后点击`New site from Git`，从中选则之前用来存储本地根目录文件的仓库。

![new site](/images/兴趣探索/建站笔记/netlify-github.png "create new site")

![选择仓库](/images/兴趣探索/建站笔记/netlify-repo.png "选择仓库")

最后一步即设置部署信息，Netlify 能自动识别出你的博客属于 Hexo 框架，故而`Build command`与`Publish directory`已自动填充好。其中`Build command`可根据博客实际情况设定，由于刚开始我们并未有什么插件命令需运行，故这里设置为`hexo clean && hexo generate`即可。

最后点击`Deploy site`，Netlify 将会对你的博客进行第一次部署，若出现错误，可根据部署日志中出错的相关提示寻找原因，自己无法解决则可谷歌出错信息。

部署完成后，Netlify 会自动给你随机生成一个很丑的域名，当然，这个域名是可修改的：

![修改域名](/images/兴趣探索/建站笔记/netlify_site.png "修改域名")

还可设置压缩 css，js，图片以加速访问：

![压缩](/images/兴趣探索/建站笔记/netlify-compress.png "压缩")

到此为止，关于 Github + Netlify 部署的操作基本完成了，至于有关 HTTPS 功能则需要拥有个人域名才可完成相关设置。

{{< notice notice-info >}}
Github 近来访问速度快了很多，个人感觉甚至比 Netlify 还要快😂。所以如果对博客的代码开源以及相关的修改记录没什么感觉的话，可以直接采用 Github Pages 部署博客。🙃
{{< /notice >}}

关于 Netlify 的深层次操作，可参考文章：

* [reuixiy | 将 Hexo 静态博客部署到 Netlify](https://io-oi.me/tech/deploy-static-site-to-netlify/)
* [荷戟独彷徨 | 博客通过 Netlify 实现持续集成](https://guanqr.com/tech/website/deploy-blog-to-netlify/)
* [知乎 | 博客写作攻略--Hexo+Github+Netlify+CMS](https://zhuanlan.zhihu.com/p/77651304)

## 基本功能配置

部署后即意味着别人能通过网址访问你的网站，接下来就应该将该网站的相关标识变成与你有关的了。

配置信息需要在..根目录..的的`_config.yml`文件中修改，作为站点配置文件，`_config.yml`有点像一个中央控制台，利用它可以实现主要信息的修改以及相关功能的开闭，故而对这个文件一定要重视。`_config.yml`文件相关配置我会在下面贴出来。

<blockquote class="quote">
在网上很多教程中，都有提到分清..站点..配置文件以及..主题..配置文件，这两个文件名都是 _config.yml，只不过存放目录不同而已。
</blockquote>

此外还要选出你心仪的主题，Hexo 支持的主题有很多，而起初 `hexo init` 后生成的 `themes` 文件夹下的 `landscape` 便是一种主题，若想寻找更多主题，可前往 [Hexo themes](https://hexo.io/themes/index.html) 慢慢寻找。也可以前往 Github 搜索 `hexo theme`，从 stars 最多的开始浏览，直到找到你心仪的主题。

![hexo-themes](/images/兴趣探索/建站笔记/hexo-theme.png "hexo-themes")

而在这我推荐 Hexo 博客选择 [Next](https://github.com/theme-next/hexo-theme-next) 主题，毕竟人家的背后是一个团队，主题不仅简洁还功能齐全，而且更新维护速度也快。

### 更换主题：Next

Next 主题在 Github 上有两个仓库。一个是 `v 6.0.0` 之前版本的[个人仓库](https://github.com/iissnan/hexo-theme-next)，而由于主题原作者停止维护该主题，所以有大佬们另起炉灶，联合创立了一个 NexT 团队，目前最新版本的主题便在这个[仓库](https://github.com/theme-next/hexo-theme-next)中。当然东西还是新的好，所以建议大家下载 Next [最新版本](https://github.com/theme-next/hexo-theme-next)的主题。

下载方式有两种：

① 直接`clone` 主分支（master）的最新版本主题文件到 Hexo 的主题文件夹（`themes`）

由于 Next 主题经常更新，故建议利用子模块[^2]来添加 Next 主题，这样有利于跟进主题的更新。
```C
$ git submodule add --depth 1 https://github.com/theme-next/hexo-theme-next.git themes/next
```
执行完后会在 themes 文件家下生成 next 文件，next 文件中便存放着 Next 主题的所有相关文件。

② 到 Releases 中下载每月月初发布的[发行版](https://github.com/theme-next/hexo-theme-next/releases)主题，将压缩文件中的内容解压至主题文件夹下的 `next` 文件夹中。

然后在根目录下新建`.gitmodules`文件，以设定`themes`文件夹下的 `next `文件为子仓库，子仓库即为 NexT 主题的仓库：`[submodule "themes/next"]`。

安装完 Next 主题后，修改站点配置文件 `_config.yml`：

```diff
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
- theme: landscape
+ theme: next
```

在根目录下的`.git`文件中找到`config`，增加以下内容：

```C
[submodule "themes/next"]
	url = https://github.com/theme-next/hexo-theme-next.git
	active = true
```

而这两方法究竟选哪种好，视自己喜好而定吧🤪。[^3]

此后主题便已经替换为了 next，且 themes 下的 landscape 文件夹可删除（毕竟主题也不是它了🙃）。

{{< notice notice-note >}}
Next 近来的更新，使得我们对博客的各种优化朝着以注入的方式完成。即站点下的文件内容能加入亦或覆盖 Next 文件下相应文件的内容，这能让我们无需修改 Next 主题内的相关文件，而完成新样式的设置，同时也利于直接更新主题，不用担心因大幅度修改主题而导致无法更新。总而言之：不要轻易修改 Next 文件中的内容。
{{< /notice >}}

### 站点配置文件

请查阅 [Hexo 官方文档](https://hexo.io/zh-cn/docs/configuration.html)，文档中有对站点配置各个参数非常详细的介绍。这里也贴出我的站点配置文件，可作为一参考。若对其中一些参数比较迷糊，可 [Google](https://www.google.com/) 查找。当然也没必要全部看懂，把必须要设定的参数看懂即可。

..注意..：该文件内各项参数名称后的 `:` 为半角字符，其后需要一个..空格..再写内容。另外除非是已安装的插件需要在该文件进行一些参数的设定，否则不要随意添加或删除任何内容，因为这类操作可能会影响到博客的生成。

```yaml
# 因为 hexo 版本不同,hexo init 得到的文件内容也会有所不同
# 本文件基于 Hexo version: v4.2.0，其他版本设置类似。

# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
## 网站标题、副标题、网站描述、关键词、作者、语言等基本信息的配置
title: ruchan
subtitle: 'Just go'
description: '一个精神追求者'
keywords:
author: Ruchan
language: zh-CN
timezone: ''

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
## 博客的网址及文章 URL 结构，默认在根目录
## 如果你想要将博客设定在一个子目录，如 'http://yoursite.com/blog'，则将 root 设定为该子目录的名称 '/child/'
## 建议博客的 URL 结构在博客建立初期就规划好，因为当你写的文章被搜索引擎收录以及被读者收藏后，再更改结构，会对你的网站访问造成一定影响
url: http://crcrc.me/
root: /
## 详细参数请查看：https://hexo.io/zh-cn/docs/configuration.html#网址
## 这里默认的路径太不利于 SEO，因为 title 中的汉字经过转义会变得很长。
## 可以考虑使用一些插件，直接生成永久链接，如 hexo-abbrlink 插件：https://github.com/rozbo/hexo-abbrlink
permalink: :year/:month/:day/:title/
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks

# Directory
## 这里是设定一些基本文件夹的名称，如资源文件夹等。
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
## skip_render 是为了避免在执行 'hexo generate' 命令后将一些你不想转义的文件转成 HTML 格式。
## 比如 README.md，你可以将这些文件名填写在括号内，格式为 [README.md, Post1.md, Post2.md]
skip_render:

# Writing
new_post_name: :title.md # File name of new posts
default_layout: post
titlecase: false # Transform title into titlecase
external_link:
  enable: true # Open external links in new tab
  field: post # Apply to the whole site or post
  exclude: ''
filename_case: 0
render_drafts: false
## post_asset_folder 设置为 true 后，当你新建一个 post 的时候，会在同级目录生成一个相同名字的文件夹，结合插件hexo-asset-image可在文章内插入本地图片。
post_asset_folder: false
relative_link: false
future: true
## 代码高亮设置
highlight:
  enable: true
  line_number: true
## 代码自动高亮
  auto_detect: false
  tab_replace: ''
## 没看懂
  wrap: true
  hljs: false

# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: -date

# Category & Tag
default_category: uncategorized
## URL 中的分类和标签「翻译」成英文
## 参见：https://github.com/hexojs/hexo/issues/1162
category_map:
tag_map:

# Metadata elements
## https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta
## Meta generator 标签。值为 false 时 Hexo 不会在头部插入该标签
meta_generator: true

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss
## Use post's date for updated date unless set in front-matter
use_date_for_updated: false

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Include / Exclude file(s)
## include:/exclude: options only apply to the 'source/' folder
## 详细说明见：https://hexo.io/zh-cn/docs/configuration.html#包括或不包括目录和文件
include:
exclude:
ignore:

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next

# Deployment
## Docs: https://hexo.io/docs/deployment.html
## Dependency: https://github.com/hexojs/hexo-deployer-git
## 设定执行 'hexo deploy' 命令后提交的代码仓库地址
## 这里由于我直接用 Netlify 部署，且没安装hexo-deployer-git，故而未设置该项
deploy:
  type: ''
```

## 主题配置文件

之前提过，next 文件中的内容尽量不要修改，对此 next 也提出了相关的解决方法：

* 从主题的 `/themes/next/_config.yml` 文件中复制你需要的 NexT 配置项到 `/_config.yml` 中：
  * 所有这些配置项右移两个空格（在 Notepad ++ 中：选中这些文字，`TAB` 键即可缩进两格）
  * 在这些参数最上方添加一行 `theme_config:`

参考文章：

* [Hexo 官方文档 | 覆盖主题配置](https://hexo.io/zh-cn/docs/configuration.html#覆盖主题配置)
* [Next 方案提供](https://github.com/theme-next/hexo-theme-next/blob/master/docs/zh-CN/DATA-FILES.md)

比如：

```yaml
theme_config:
    override: false

    # Console reminder if new version released.
    reminder: false

    # Allow to cache content generation. Introduced in NexT v6.0.0.
    cache:
      enable: true

    # Remove unnecessary files after hexo generate.
    minify: false
.....
```

因主题配置文件太长，故在此只展现一部分，完整的配置文件请前往我的代码仓库获取。

[^1]:文件相关介绍可浏览这篇文章：[Hexo 的目录结构](https://www.jianshu.com/p/17d55d420d94)

[^2]: 关于子模块可浏览：[Git Submodule 的反思](https://forcemz.net/git/2018/03/22/GitSubmoduleRethinking/) 以及 [Git Submodule 完整用法整理](https://blog.csdn.net/wkyseo/article/details/81589477)
[^3]:两种方法大体区别可浏览：[荷戟独彷徨 | 安装 NexT 主题](https://guanqr.com/tech/website/hexo-theme-next-customization/#安装-next-主题) 的末尾说明。