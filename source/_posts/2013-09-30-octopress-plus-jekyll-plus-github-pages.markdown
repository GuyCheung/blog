---
layout: post
title: "Octopress + Jekyll + Github Pages 搭建个人Blog"
date: 2013-09-30 22:33
comments: true
categories: 'CoolSkill'
---

最近心血来潮，在一年不写Bolg后（虽然之前也不怎么写）突然又有了写Blog的冲动。先自勉一个，希望这次能坚持下去！

第一篇就写写怎么用题目的里东东搞个个人博客吧～

### Github Page

简单说这东西就是一个静态网页托管，那这么简单为什么要用呢？我列几条你就坐不住了：

* **免费！！！**而且不像其它免费空间那样漫天广告
* 无限流量，而且稳定！(Github宕机？！)
* 版本管理，只需要git push一下就能生效

怎么样，还不错吧？

网上这东西怎么用的很多我就不写了，不过还是推荐官方Doc：[Github Pages Help](https://help.github.com/categories/20/articles)

### Jekyll

由于官方文档里有说支持这东东，加上之前也有耳闻这东东可以用帅气的Markdown写网页。所以就很快去搞了一把～

```bash
gem install jekyll
jekyll new blog
cd blog
jekyll serve
```

正常情况下就可以在 http://localhost:4000 上访问jekyll的Demo了

OK，继续部署到Github上去。我Github的用户名为guycheung，所以先在Github上建立仓库：guycheung.github.io
*仓库名一定要<username>.github.io这种形式*

然后在终端操作

```bash Push Blog to Github
git init
git remote add git@github.com/GuyCheung/guycheung.github.io.git
git add -A .
git commit -a -m 'init blog'
git push origin master
```

OK，可以休息几分钟了。Github说的是10分钟内将页面部署上去，就可以通过guycheung.github.io访问博客啦～

### Octopress

可以访问后不得不说后面还有好多工作。当然第一就是**找个像样的主题**

一开始也知道有Octopress这东西，所以就直接找 Jekyll 模板什么的，发现好多<https://github.com/mojombo/jekyll/wiki/Sites>

看了半天最后找到<http://travisswicegood.com/>这个看起来还不错，可是不知道怎么使用。。。痛苦

好在提供了源码<https://github.com/tswicegood/domain51.com.git>，clone下来看了看发现了Octopress这么个神奇的工具

于是找官方之<http://octopress.org/>

随便google了一把octopress的theme（也就是模板咯），发现这几个网站还不错：

* <https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes>
* <http://opthemes.com/>
* <http://octopressthemes.com/>

自己挑一个用吧哈哈

### Disqus

写博客当然不能没有评论，不过就算没人看没人评论也得坚持写Blog啊！

Disqus这东东就是第三方评论专用的了，很nice的东西。Octopress里已经默认集成这东西了，只需要我们简单在_config.yml里配置一下：

```yaml _config.yml
# Disqus Comments
disqus_short_name: guycheungsblog
disqus_show_comment_count: true
```

这里要注意的是`disqus_short_name`是在disqus网站上注册后才写的，而不是随便写的名字。。被这个坑大了

到目前，一个比较像样的Blog已经出来啦！

### 部署

使用Octopress后比较方便地跑一下：

```bash
rake new_post["title"] # 这样就可以生成新blog文件，然后直接vim这个文件就可以写博客啦！Markdown的爽吧～
rake generate
rake preview # 这样就可以在<http://localhost:4000>看预览了～写博客的时候可以一直开着，这样保存文件就更新了
rake deploy # 部署到github上去
```

另外，由于现在octopress没有版本管理了，还是觉得心有点虚，所以又搞了个git仓库来放octopress这个目录的东西

