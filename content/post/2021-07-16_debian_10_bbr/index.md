---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 07 16_debian 10安装bbr"
subtitle: "bbr安装"
summary: "bbr左右目标主机是有提高带宽的利用率的"
authors: [admin]
tags: [vps]
categories: []
date: 2021-07-17T21:52:04+08:00
lastmod: 2021-07-17T21:52:04+08:00
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

前面有介绍过通过升级 Linux Kernel 内核升级到 4.9 及以上版本实现 BBR 加速的，由于 Debian10 默认的内核就是 4.19 版本的内核而且编译了 TCP BBR 模块，所以可以直接通过参数开启。

新的 TCP 拥塞控制算法 BBR (Bottleneck Bandwidth and RTT) 可以让服务器的带宽尽量跑慢，并且尽量不要有排队的情况，让网络服务更佳稳定和高效。

修改系统变量：

```
echo net.core.default_qdisc=fq >> /etc/sysctl.conf
echo net.ipv4.tcp_congestion_control=bbr >> /etc/sysctl.conf
```


保存生效

```
sysctl -p
```


执行

```
sysctl net.ipv4.tcp_available_congestion_control
```

如果结果是这样

```sysctl net.ipv4.tcp_available_congestion_control
net.ipv4.tcp_available_congestion_control = bbr cubic reno

```

就开启了。 执行


```
lsmod | grep bbr
```


检测 BBR 是否开启。


### 优化 Linux 上的 shadowsocks 服务器
