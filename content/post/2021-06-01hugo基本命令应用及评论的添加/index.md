---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 06 01hugo基本命令应用及utterances评论的添加"
subtitle: "hugo的基本应用"
summary: ""
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

utterances是一款基于Github Issue的Github工具,优点主要是无广告、加载快、配置简单，轻量开源!

由于utterances是一款Github App，因此安装utterances非常简单，只需要授权特定repo权限给utterances就可以了,注意一个点：授权的这个repo必须是public的，可以选择多个repo，但是建议选择一个就可以了，也比较安全。

[https://github.com/apps/utterances](https://github.com/apps/utterances)
