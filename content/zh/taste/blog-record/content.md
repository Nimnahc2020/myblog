---
title: "Hexo-draft"
date: 2020-04-23T22:57:32+08:00
toc: true
tags: ["Hexo","Blog"]
series: ["notes-on-blog"]
aliases: ["/study/blog/hexo_new_sky/"]
gitinfo: true
dropCap: false
draft: true
---

## 进阶 自定义

### 自定义配置文件

最新的 Next 优化不得不提到这个设定：`custom_file_path`，因为它，我们不用修改主题下的相应文件来完成在`<head>`或`<body>`等部位添加所需代码的任务，这样对网页样式的优化会方便很多。故在此先展示该配置。

```yaml
custom_file_path:
  #head: source/_data/head.swig
  #header: source/_data/header.swig
  #sidebar: source/_data/sidebar.swig
  #postMeta: source/_data/post-meta.swig
  #postBodyEnd: source/_data/post-body-end.swig
  #footer: source/_data/footer.swig
  #bodyEnd: source/_data/body-end.swig
  #variable: source/_data/variables.styl
  #mixin: source/_data/mixins.styl
  #style: source/_data/styles.styl
```

<blockquote class="quote-center">
<p>
Two things fill me with constantly increasing admiration and awe,</br>the longer and more earnestly I reflect on them: </br>the starry heavens without and the moral law within.
</p>
</blockquote>
中文翻译：“有两种东西，我对它们的思考越是深沉和持久，它们在我心灵中唤起的惊奇和敬畏就会越来越历久弥新，一个是我们头顶浩瀚灿烂的星空，另一个就是我们心中崇高的道德法则。”

在此引用这句话只是想说明，