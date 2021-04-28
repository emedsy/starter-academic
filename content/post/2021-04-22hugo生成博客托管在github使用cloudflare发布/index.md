---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021-04-22hugo生成博客托管在github使用cloudflare page发布"
subtitle: "Hugo"
summary: "配置hugo"
authors: [medsy]
tags: [blog]
categories: [网络]
date: 2021-04-22T18:12:43+08:00
lastmod: 2021-04-22T18:12:43+08:00
featured: false
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

---
&#8194;&#8194;&#8194;作为一个非专业的小白，非常希望自己能有机会机会搭建一个自己的博客，wordpress虽然有现成的可以租用，免维护，但是，还是希望把所有的控制权都把握在自己手里，最终，通过hugo生成博客，生成了html静态网页，存放在github上，可以使用gitpage发布，如果想添加自己的域名可以使用cloudflare page 发布。

## Hugo 安装 / 更新
&#8194;&#8194;&#8194;[hugo](https://gohugo.io/)是使用<font color="#dd0000">Go</font>语言开发的静态站点生成器。不过无需准备 <font color="#dd0000">Go</font> 语言环境，可以直接通过二进制编译包进行跨平台部署。

### 以下均以 debian 10 为例

&#8194;&#8194;&#8194;前往[github](https://github.com/gohugoio/hugo/releases)下载最新版本，这里我们下载hugo_extended_0.82.1_Linux-64bit.deb
由于我们使用academic的主题，需要hugo的扩展版本。
### 安装hugo
```
dpkg -i hugo_extended_0.82.1_Linux-64bit.deb
```
同时，需要安装go环境


### 常用命令
hugo：编译项目生成静态网站，默认位置在项目的 public 目录下
hugo server： 启动你的网站服务，可以通过浏览器访问
http://127.0.0.1:1313/ 访问站点
hugo new {folder}/{name}.md: 创建新文章，使用 markdown 进行排版，一般默认放在 post 文件夹下
一般情况下用这三个命令就够了

### Academic 安装 / 更新

Academic 是一个 Hugo 主题，从名字就可以知道这个主题比较学院派，适合科研 / 学术人员发布个人信息 / 介绍科研项目，当然，拿来做个人博客也是没问题的

### 安装


通过 git 安装的话，首先建议你在 GitHub 上 fork 成你自己的项目，默认的话，通过 git clone https://github.com/your_repo/academic-kickstart.git My_Website 将代码克隆到本地文件夹 My_Website

进入文件夹，初始化项目：
```
git submodule update --init --recursive
```
完成安装

### 自动更新

说是自动，还是需要手动执行一条命令：
```
git submodule update --remote --merge
```
这么做的前提条件是你是 install 的，也就是 git submodule update --init --recursive 过的，而不是直接把 academic 给 clone 到 themes 文件夹

## 部署到 Github Pages
原理
网上介绍的办法很多，但核心其实就一句：

将 hugo 命令生成的 public 文件夹上传到 GitHub pages 项目下。

public 文件夹相当于编译完成的静态网站，你在本地打开其实就能看。换句话说，你每次手动将这个目录下的内容上传到你的 GitHub page 项目也是可以的。

然后为了达到这个目的，Academic 给出的做法是利用 git submodule 将你的 GitHub page 项目作为 My_Website 项目的子模块存放到 public 目录。那么当你更新你的文章之后，只提交 public 文件夹内的变更到 GitHub page 项目即可。
![images](/image/1.png)

官方教程 (缩减版)
原教程 看这里；

在 GitHub 上创建两个项目，一个是 fork 的 academic-kickstart，也就是你前面 clone 到本地的 My_Website，另一个即是以你用户名 / 组织名开头、以 .github.io 结尾的 GitHub page 项目。

在 My_Website 目录下执行 git submodule update --init --recursive 将子模块更新到最新状态；

将 config.toml 中的 baseurl 设置为你的 GitHub page 地址；

(实质) 删除 public 文件夹 (如果有的话)，将 GitHub page 项目添加为子模块：git submodule add -f -b master https://github.com/<USERNAME>/<USERNAME>.github.io.git public;

这时候你的 My_Website 项目实际上有两个子模块：作为主题依赖的 themes/academic 和作为网站的 <USERNAME>.github.io；

有意思的是一般是子模块 themes/academic 更新了之后，你更新主项目 My_Website 的依赖；

而你更新主项目 My_Website 的文章之后，再会手动的更新子模块 <USERNAME>.github.io，刚好反过来。

新增 / 编辑文章后，更新 academic-kickstart 项目：
```
git add .
git commit -m "Initial commit"
git push -u origin master
```

更新 GitHub page 项目：
```
cd public
git add .
git commit -m "Build website"
git push origin master
```
当然，如果你换一台机器，你更新项目时候，别忘了子项目的更新
```
cd public
git clone --recurse-submodules https://github.com/your_repo/your_repo.github.io.git .
git submodule update --remote
git add .
git commit -m "git submodule updated"
```
这样，子模块里边的和仓库是同步的

如果在其他机器想编辑博客
```
git pull
git merge
```
