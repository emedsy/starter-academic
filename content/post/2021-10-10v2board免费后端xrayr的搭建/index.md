---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 10 10v2board免费后端xrayr的搭建"
subtitle: "XrayR-project对接v2board"
summary: "一个基于Xray的后端框架，支持V2ay,Trojan,Shadowsocks协议，极易扩展，支持多面板对接。
项目地址: https://github.com/XrayR-project"
authors: [admin]
tags: []
categories: []
date: 2021-10-10T10:10:18+08:00
lastmod: 2021-10-10T10:10:18+08:00
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


#### <mark>项目地址: https://github.com/XrayR-project<mark>

现在下载解压xrayr后端：

```
mkdir /opt/xrayr && cd /opt/xrayr
wget https://github.com/XrayR-project/XrayR/releases/download/v0.7.2/XrayR-linux-64.zip
wget https://github.com/XrayR-project/XrayR/releases/download/v0.7.2/XrayR-freebsd-arm64-v8a.zip

 unzip XrayR-linux-64.zip
```

编辑xrayr配置文件：
```
nano config.yml
```

改为如下配置，需要改动的重要部分都写了注释：

```
Log:
  Level: debug
  AccessPath: ./access.log
  ErrorPath: ./error.log
DnsConfigPath: ./dns.json
Nodes:
  -
    PanelType: "V2board" // 面板类型
    ApiConfig:
      ApiHost: "https://v2board.ohshit.club/" // v2board面板的地址，域名结尾一定要加/
      ApiKey: "imlalaimlalaimlala" // v2board面板内配置的通讯密钥
      NodeID: 1 // v2board面板内对应节点的id
      NodeType: V2ray // 节点类型
      Timeout: 30
      EnableVless: false
      EnableXTLS: false
    ControllerConfig:
      ListenIP: 0.0.0.0
      UpdatePeriodic: 60
      EnableDNS: false
      CertConfig:
        CertMode: dns
        CertDomain: "node1.ohshit.club" // 节点域名
        Provider: cloudflare
        Email: example@lala.im // 你的邮箱
        DNSEnv:
          CF_DNS_API_TOKEN: cwPZEBAvIXUcxCdy4v2ib5j8uK-KwnRMDuNPxE-n // 你之前申请的cloudflare域名api
```


 新建supervisor配置文件用于守护xrayr：     
  ```
  apt install supervisor
  nano /etc/supervisor/conf.d/xrayr.conf
  ```

  写入如下配置：
  ```
  [program:xrayr]
directory=/opt/xrayr
command=/opt/xrayr/XrayR -config
config.yml
autostart=true
autorestart=true
```

启动xrayr：
```
supervisorctl update
supervisorctl status
```

至此所有配置就全部完成了。如果部署遇到了问题，下面的这些日志可能会有帮助：
```
/var/www/v2board/storage/logs/laravel-xxxx-xx-xx.log
/var/www/v2board/storage/logs/queue.log
/opt/xrayr/access.log
/opt/xrayr/error.log
```
将程序写入守护进程之前，可以使用命令调试，直接读取回报结果
```
root@1977:/opt/xrayr# ./XrayR -config config.yml
XrayR 0.7.2 (A Xray backend that supports many panels)
2021/10/10 02:32:43 Start the panel..
2021/10/10 02:32:43 Xray Core Version: 1.4.5
2021/10/10 02:32:45 Added 11 new users
2021/10/10 02:32:46 Start monitor node status
2021/10/10 02:32:47 0 user deleted, 0 user added
2021/10/10 02:32:47 Start report node status
```   
