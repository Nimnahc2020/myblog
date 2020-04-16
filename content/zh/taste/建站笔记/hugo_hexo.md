---
title: "梦言梦语"
date: 2020-04-02T11:59:34+08:00
tags: ["Hugo","Draft"]
series: ["博客小记"]
aliases: ["/study/blog/hugo_hexo/"]
gitinfo: true
---

**暗夜中，渴望一束光的关怀；在白天却更渴望黑洞的吞噬：因为好奇心，想看看黑暗中有什么。**

——摘抄自[reuixiy](https://io-oi.me/)

<!--more-->

**黑暗是未知之地，但好奇心总是驱使人们前进。**

**因为，我们敢于大声喊出：我们的征途是星辰大海！**

------

这篇文章算是闲聊，记录生活某一小片段。亦是我的学习路上的笔记、草稿。

主要是探寻在一台电脑上同时操作部署两个博客（Hugo、Hexo）的方法历程。

# 前言

当你配置好了（下好了Hugo后），并选择了Hugo主题后，(我选择的MemE),那么你该面临问题，是把这个博客
部署到你之前hexo部署的github账户上还是部署到一个新的账户上。

很明显，我不想放弃我之前花那么多精力干的hexo。（就在昨天我还加了个相册功能界面呢，不过不大美观，完全没有教程的博主们搞出的相册好看）吐槽中！：他们永远在文末加一句：具体样式请个人自行修改，我、我有那本事找你干嘛..
不过我们也不能无理要求人家手把手的教，具体还是要自己去做，才能成为一种历练！
Ps:相册我通过七牛云的链接，是一些暑假和gays们玩的小片片，内存太大，加载不出是常事。

接下来开始正题：（也就是草稿，大概捋一下步骤，之后完善的话就依据这个写教程吧）

# 部署到Github

## 新建Github账户

同hexo一样，新建仓库（仓库名和Github账户名一致），然后...emm..难受！

## 运行命令

前提是你已经安装好了Hugo，选好并下载好了主题。（我选择的是MemE）

```
官方说明：
 hugo --theme=主题 --baseUrl="http://your_name.github.io/"
 作用:通过命令渲染出你所需要的页面等文件，并将其存放在了public文件夹中
（我的：hugo --theme=meme --baseUrl="http://Nimnahc2020.github.io/"）
 Ps:hiahia,谁知道我的这名字怎么读，源于啥呀？
```

紧接着：

```
$ cd public         
//进入public仓库（因为你之前是在hugo根目录下运行的①的命令）
$ git init             
//初始化git
$ git remote add origin https://github.com/your_name/your_name.github.io.git   
//我也还没看出这是干哈的，直译好像就那个意思
$ git add -A      
// 像是把该文件夹所有修改上传上去
$ git commit -m "first commit"       
//就是上传更新的文件所拥有的注释，双引号内即为注释，可修改(自己看得懂啥意思就行)
$ git push -u origin master             
//emm，只有这一步成功才算万事大捷
```

## 发现问题

Bingo!在上面的最后一步遇到问题。（非拥有两个github的忽略这个）

Emm，先谈我对ssh的浅且简的理解，我们运行上诉命令，都是通过计算机的各种运行环境，至今我只用过两种
运行界面：git bash 和cmd命令，当你安装了一些软件，并且成功加入到了计算机的运行环境中后，你就可以调用相关的命令。
（Eg：安装了git 那么就可调用和git相关的命令，hexo、hugo都一样的意思）
而调用有些命令上联网操作的，你能把本地文件上传到Github上当然要联网。
Github又是一个账户，自然需要账号密码。
这个时候就有网站的HTTPS设置和SSH设置了，新建仓库后都看得到这两个设置。
用HTTPS布置网站后，你要输入账号密码，SSH就是能帮你保存账号密码，让你第一次输入账号密码登入后一段时间都不再需要账号密码上传文件。
（我到现在都没搞清楚hexo的repo设置中HTTPS和SSH设置有啥不同，都在输入密码后就不用输了）
总之明白原理就好办事了。

# 解决问题

## SSH操作

上述问题据我了解：好比是你默认用了自己只有自家北极豪宅家门的钥匙，并用它去开你在南极豪宅的家门，完全打不开啊。那么这个时候就需要你更改默认设置了。

### SSH体验

**SSH相关设置：主要参考[这篇文章](https://github.com/jawil/notes/issues/2)**

照着文章的方法做就行。

注意： ①清除 git 的全局设置，上文提到了两种方法，自行查阅
             ②在.ssh文件下创建config,我也不造这是个啥东西，反正改它就是了。

```
这里特别说明config的文本内容：
#该文件用于配置私钥对应的服务器
#Default github user(609514766@qq.com)
Host WillCAI2020.github.com
        HostName github.com
        IdentityFile ~/.ssh/id_rsa_one

Host Nimnahc2020.github.com
        HostName github.com
        IdentityFile ~/.ssh/id_rsa_two
注意缩进，id_rsa_one(two)根据具体名字填
Host 后的东西可更改。
```

还要注意把相应的SSH密钥添加到你的不同的Github账户上，这里不赘述。

```
配置完后运行：
$ ssh -T git@WillCAI2020.github.com
$ ssh -T git@Nimnahc2020.github.com
发现都匹配成功。（但我总觉得SSH好像有没有都差不多）
```

### 处理SSH

接着就是处理钥匙的问题了，多次尝试后，终于发现行得通的方法，如下：

① 就是把你之前删掉的默认用户名、密码加回去。（即前面提到的清除git全局设置不需要做..做了只是提高
你更深的认识）

```
添加命令：
git config --global user.name userA
git config --global user.email userA@Email.com
或着直接找到.gitconfig文件修改即可。
```

② 到相应仓库文件设置该仓库路径的钥匙，这样听说是能在这份文件路径中使用你新设置的钥匙。

表述的有点含糊，引用一篇文章内的话：

```
单独设置每个repo 用户名/邮箱”这个步骤，我就是跑到工程下，执行git config user.email “xxxx@xx.com”和git config user.name “xxxx”命令。看来以后每次我GitHub／GitLab clone一个新的工程下来，都要在clone完成后，在这个工程目录下执行这两条语句来配置。【解决办法】：工作电脑平时使用公司的gitlab比较多，可以把公司的账户设置为全局，然后在单独的需要用别的账号的工程下配置对应的账号。这样就不用频繁地做这个配置。(这个全局设置与单独工程下设置地顺序不做要求)
```

大概就这个意思。

③ **关键步骤，销毁证书（记忆消失大法）**

主要参考[这篇文章](https://blog.csdn.net/klxh2009/article/details/76019742)

你之前的操作让电脑记住了你的默认钥匙，那怎么办，办法简单，把它灭口。
你需要找到“管理Windows凭据”该选项，我的是在：我的电脑—单击属性—控制面板—用户账户—管理Windows—凭据-Windows凭据。
然后找到普通凭据中那把你想消除的记忆，删掉即可。

④ 收尾工作

最后你再去部署，计算机又要你输账号密码，你把该博客仓库对应的Github账号密码输入，以我在hugo文件下为例，我输入了hugo对应的Github数据，这时电脑又会得到这把钥匙，并把它作为默。之后我如果想去更新hexo博客，那就得去丢掉这把钥匙，再输入hexo对应Github的数据，完成推送更新。

```
Hugo推送更新:
首先在hugo根目录下运行： hugo --theme=主题 --baseUrl="http://your_name.github.io/"  
//以此生成最新的public文件。
然后运行：（$ 不是命令，人家就一符号）
$ cd public          //进入该文件
$ git status         //运行后可看到有做修改的文件
$ git add -A       //上传所有修改
$ git commit -a -m "update"         //注释
$ git push origin master -f         //上传文件
```

然后就ojbk了。

# 后语

很明显Hugo的更新和hexo三连比起来复杂太多了，这当然也很可能是我太孤陋寡闻，还不知道快捷方式。

同样，以上提供的操作方法很可能有很多根本不需要，但是我终究是做了这些步骤后解决了问题。
这是我继上述操作成功后就赶忙记录的文章，也算是我在Hugo上的第一篇文章，很大程度也是草稿，语言多显随意。

初次接触Hugo,以及MemE主题，很多功能还不会用，比如上传图片等...(所以该文还未拥有相应图片讲解)

MemE主题还有很多好玩的且简捷的配置，我虽然很有兴趣去探索，但是以我一探索起来啥也顾不着的性格，还是先补补觉，赶一赶催交的作业吧。

很感谢设计并提供这一主题的[reuixiy大佬](https://io-oi.me/)
我昨晚依据meme教程安装后，`hexo server -D`重视出错，大意好像说是什么scss文件找不到，于是我在MemE的Issues某个讨论上弱弱地问出了我在Github上的第一问题，因为感觉想这些大佬都不怎么会注意到这种发言，于是我就去别的页面搞解决方法，结果当我四十分钟筋疲力尽地回到Issues上后，发现reuixiy大佬竟然回了我的问题，

并标注出了对上一位提出该问题地回答。（原来MemE是需要hugo-extened版本安装才完美）
于是我就去下载hugo-extened，我安装了choco并用choco命令下载hugo-extened,但是由于该命令是从外网下载文件，而我并无科学上网的渠道（都好贵），于是就慢慢地等啊等啊等啊（有好多次都是下到一半就gg了）
终于历经千辛万苦，我在今日凌晨的深夜中得到了运行提示：`Web Server is available at http://localhost:1313/` （喜极而泣）

然后就把部署到github上生成网站的任务交给白天的我了。

我发四，再熬夜，我就...我就...就...