---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 04 30snap生成shadowsocks-libev"
subtitle: ""
summary: "这篇教程记录了如何安装，配置并维护一台Shadowsocks-libev服务器。"
authors: [admin]
tags: []
categories: []
date: 2021-04-30T10:41:37+08:00
lastmod: 2021-04-30T10:41:37+08:00
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

## 安装Snap应用商店
通过Snap应用商店安装Shadowsocks-libev是官方推荐的方式, debian:9
```
sudo apt update
sudo apt install snapd -y
sudo snap install core
```

## 安装 ss-libev 开发版

```
sudo snap install shadowsocks-libev --classic --edge
```

## 配置 ss

配置文件 config.json 一定要放在 /snap/bin/ 中, 也可以放在 /root 根目录下

配置文件
```
{
  "server": "0.0.0.0",
  "nameserver": "8.8.8.8",
  "server_port": 443,
  "password": "你的密码",
  "method": "chacha20-ietf-poly1305",
  "timeout": 600,
  "no_delay": true,
  "mode": "tcp_only",
  # 可以省略"plugin": "v2ray-plugin",
  # 可以省略"plugin_opts": "server;tls;fast-open;host=xxxxxxx.com;cert=/证书目录/fullchain.cer;key=/证书目录/xxxxxxx.com.key;loglevel=none"
}
```
注意，你需要把里面的ExamplePassword替换成一个更强的密码。 强密码有助缓解最新发现的针对Shadowsocks服务器的Partitioning Oracle攻击。 你可以用以下命令在终端生成一个强密码：

```
apt install openssl
openssl rand -base64 16
```
snap 启动的 ss 的命令 (开机自启文件)

```
cd /etc/systemd/system/
touch ss.service
vi ss.service
```

```
[Unit]
Description=Shadowsocks Server
After=network.target
[Service]
Restart=on-abnormal
ExecStart=/snap/bin/shadowsocks-libev.ss-server -c /snap/bin/config.json
[Install]
WantedBy=multi-user.target
```
就是 ss-server 变成了 shadowsocks-libev.ss-server ； 然后就是配置文件存放的目录变了

systemctl enable ss
systemctl start ss
systemctl status ss
```
