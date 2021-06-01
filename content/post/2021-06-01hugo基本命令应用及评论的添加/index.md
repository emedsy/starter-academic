---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 06 01hugo基本命令应用及utterances评论的添加"
subtitle: "hugo的基本应用"
summary: "基本的hugo的博文生成命令;安装utterances;将视频显示在博客中"
authors: [admin]
tags: [hugo，博客]
categories: []
date: 2021-06-01T15:51:12+08:00
lastmod: 2021-06-01T15:51:12+08:00
featured: true
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## 基本的hugo的博文生成命令

---

```
D:\blog\starter-academic>hugo new post/2021-06-01hugo基本命令应用及评论的添加/index.md
D:\blog\starter-academic\content\post\2021-06-01hugo基本命令应用及评论的添加\index.md created

```

目前，hugo academic的主题，官方支持disqus，twitter，commento，三个评论系统。可以在
***config/_default/params.yaml***
文件中更改

```
comments:

  provider: ''
  commentable:
    post: true
    book: true
    project: true
    publication: true
    event: true
  disqus:
    shortname: ''
    show_count: false
  commento:
    url: ''
```
但是，上述三种有的需要fq，有的需要收费，对于我不太适合。根据网上教程尝试了utterances评论。暂时可以使用。




## 安装utterances

---

utterances是一款基于Github Issue的Github工具,优点主要是无广告、加载快、配置简单，轻量开源!

由于utterances是一款Github App，因此安装utterances非常简单，只需要授权utterances给特定repo权限就可以了,注意一个点：授权的这个repo必须是public的，可以选择多个repo，但是建议选择一个就可以了，也比较安全。

[https://github.com/apps/utterances](https://github.com/apps/utterances)


## ***存储库的选择***

---

选择将连接到的存储库(建议连接代码库，对于我来说我连接的theme库，也就是academic，不是生成的repo.github.io库)。

- 确保 repo 是公开的，否则您的读者将无法查看问题/评论。
- 确保在 repo 上安装了utterances 应用程序，否则用户将无法发表评论。
- 如果您的 repo 是一个 fork，请导航到其设置选项卡并确认问题功能已打开。

![image](/image/utterance1.png)

![image](/image/utterances2.png)

```
<script src="https://utteranc.es/client.js"
        repo="[ENTER REPO HERE]"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

```


需要注意的是，在最新版本的academic theme里边，我没有能找到插入这个脚本的模块，只能采取最笨的办法，插入每篇博文的尾部。但好在，将静态网页生成后，评论部分成功显示，并且没有广告。但需要评论者有自己的github账户。



## 将视频显示在博客中：

---
- 将视频上传b站审核
- 审核过的视频在b站生成可以插入博客的分享链接代码
- 插入你想发布的文章当中。

***例如：插入你上传b站的音乐视频***
```
<iframe src="//player.bilibili.com/player.html?aid=930976593&bvid=BV1rK4y1X72F&cid=347412972&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
```


<iframe src="//player.bilibili.com/player.html?aid=930976593&bvid=BV1rK4y1X72F&cid=347412972&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>

<script src="https://utteranc.es/client.js"
        repo="emedsy/starter-academic"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
