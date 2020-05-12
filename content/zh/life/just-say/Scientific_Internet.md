---
title: "上网那些事"
date: 2020-05-11T23:45:30+08:00
dropCap: false
displayCopyright: false
toc: false
gitinfo: true
slug: "someways-about-science-surf-the-internet"
---
<blockquote class="quote-center">
<p>
<font class = "colorfulfont">
Two things fill me with constantly increasing admiration and awe,</br>the longer and more earnestly I reflect on them: </br>the starry heavens without and the moral law within.
</font>
</p>
</blockquote>

中文翻译：“有两种东西，我对它们的思考越是深沉和持久，它们在我心灵中唤起的惊奇和敬畏就会越来越历久弥新，一个是我们头顶浩瀚灿烂的星空，另一个就是我们心中崇高的道德法则。”

我没学过哲学，也探讨不出这句话的深意，但谈到科学的上网，那还是把它放着镇楼🙃。

话摆在前面：懂得什么能做，什么不能做，这很重要。宇宙深邃不见底，令人心生敬畏，网络世界也是如此，愿你我在..谨守初心..的基础上，持着好奇心去探索未知世界。

同时也摆出两篇文章，建议浏览：[文章一](https://qiangwaikan.com/gfw/)、[文章二](https://cnodejs.org/topic/5b0fc85b5cd02be640901047)。

前者请具备科学上网能力后再看，后者请先看文末..须知部分..。

<font class = "colorfulfont"> **说明**：本文不适合传播。</font>

倘若你对此还有想法，那接下来就来看看免费的科学上网的方法吧。

## 桥梁

首先安装谷歌浏览器（推荐这个），当然其它支持插件的浏览器均可、如星愿浏览器。下面步骤全部以谷歌浏览器为例。

先点击[这个](https://gateway.pinata.cloud/ipfs/QmetpuozsRGL4GQA9ysfuatfwyMhmRU3EaVCmAJK75KwTj/gocklaboggjfkolaknpbhddbaopcepfp.zip)下载谷歌访问助手，下载后解压文件夹，得到文件 `谷歌访问助手_2.3.0_chrome.zzzmh.cn.crx` 。

然后进入谷歌扩展程序管理界面，打开开发者模式。

![Chrome Extension](/images/随笔/chrome_extension.png "路径")

![Chrome Extension](/images/随笔/chrome_extension_explore.png "开发者模式")

然后将解压后的 `谷歌访问助手_2.3.0_chrome.zzzmh.cn.crx` 拖入谷歌扩展程序界面。

![chrome pull.png](/images/随笔/chrome_pull.png "拖入")

若出现错误信息（正常）：`无法从该网站添加应用、扩展程序和用户脚本` 或 `程序包无效:"CRX_HEADER_INVALID"`，那么把 `谷歌访问助手_2.3.0_chrome.zzzmh.cn.crx` 的扩展名改为 `zip`。这里提一下扩展名：

![扩展名](/images/随笔/chrome_extension_name.png "查看扩展名")

然后再拖入即可成功。成功后会自动跳转到界面：

![成功](/images/随笔/chrome_attend.png "安装成功")

此时便可成功访问谷歌的服务，接下来需要用到[谷歌应用商店](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)，以此摆脱谷歌访问助手。

进入[谷歌应用商店](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)，搜索 `Astar VPN`，点击「添加至 Chrome」安装此插件。

![Astar VPN](/images/随笔/chrome_astar.png "Astar VPN")

这个 VPN[^1] 有许多地区供选择，开启后可实现科学上网。至于科学上网的原理是什么我也不清楚[^2]。

再附上一款插件：集装箱。

![集装箱](/images/随笔/chrome_box.png "集装箱")

这款插件同样可从[谷歌应用商店](https://chrome.google.com/webstore/category/extensions?hl=zh-CN)中下载，它的功能也很强大，第一个功能即为支持谷歌加速服务（也可称阉割版的科学上网，和谷歌访问助手一样），它只支持访问谷歌相关的服务，如谷歌搜索、谷歌邮箱、谷歌翻译等。其它三个功能可安装后自行探索。

## shadowsocksR

ShadowSocksR 也被称为 ssr、酸酸乳、小飞机。它是目前最成熟的自建科学上网技术，在国内网民尤其是程序员群体中有着极其广泛的应用。优缺点可以浏览[这篇文章](https://www.wallmama.com/)，需科学上网后查看。与 VPN 的比较可查看[这篇文章](https://reezon.github.io/2018/05/23/关于ss(酸酸)和ssr(酸酸乳)，还有vpn和socks5/)。

先下载 [ShadowSocks](https://github.com/shadowsocks/shadowsocks-windows/releases)。选择最新版本的 Releases 版本即可，这里以版本 4.1.10.0 为例。

![shadowsocks](/images/随笔/shadowsocks.png "Shadowsocks")

请在科学上网的情况下下载，否则速度慢得令人发指。

下好并解压后，双击运行 `Shadowsocks.exe` 启动小飞机。

利用小飞机实现科学上网需要有 SSR 节点，有人会自建机场，提供一堆 SSR 节点，其中有收费的也有不收费的，自然收费的体验感会更好，但有些免费的节点也足以满足正常需求了。

免费 SSR 节点资源可前往 Github 搜索，有很多，但是尝试过都不咋地。

这里推荐一个网站 ：[免费S账号](https://free-ss.site/)，该网站需要科学上网后才能访问，也可以通过修改 `hosts` 记录来访问：

![直连](/images/随笔/direct_access.png "直连")

`hosts` 文件所在路径：`C:\Windows\System32\drivers\etc\HOSTS`。

进入后选择一个 SSR 节点（箭头上升越多，且数值越大的即网速越好），点击最右侧的二维码图标，然后会跳出二维码图片，然后点击小飞机的 `扫描屏幕上的二维码` 即可。

![扫描](/images/随笔/code.png "扫描二维码")

此外注意要开启 `系统代理 → pac 模式` ，`pac 模式` 可以做到访问国内的网站就用国内流量，访问国外网站就用国外流量，全局模式即为全部都用国外流量，但这样会导致访问国内网站的访问很慢。

这里和 Astar VPN 一样，不好用时就换地区（节点），换到好用为止🙃。

在这也比较下小飞机和 Astar ，前者实现的科学上网是整个电脑的，即只要开启并节点有用，那么整台电脑的流量均由小飞机代理。而 Astar 仅限于安装了这个插件的浏览器才能使用代理来实现科学上网。相较来说，小飞机采用的协议更保险，但由于我们使用的是免费 ssr 节点，节点经常波动，导致网速不稳定，Astar 相比之下更稳定一些。

无论采用哪种方式，都是为了一个崇高的目标：不花钱😂。

最后..说明..：心中知道何可为，何不可为，自然敢去也能去做了。
以及..注明..：觉得需要自行食取，不适合传播！

[^1]:VPN 原理可以看[这篇文章](https://zhuanlan.zhihu.com/p/71536075)
[^2]:有兴趣可以看[这篇文章](https://hengyunabc.github.io/something-about-science-surf-the-internet/)

