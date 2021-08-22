---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 08 22在xray使用cloudflare中转流量解决节点去回程绕道"
subtitle: "xray使用中的结点优化"
summary: "xray+cloudflare CDN及中转的问题"
authors: [admin]
tags: ["xray","中转"]
categories: []
date: 2021-08-22T22:18:55+08:00
lastmod: 2021-08-22T22:18:55+08:00
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

### 前言
由于xray的使用早期，由于cloudflare cdn的早期，速度流畅，cdnIP不断优化改变，xray走cdn的方法被大家广泛使用，就逐渐出现了高峰期明显变慢，而且由于我的do 新加坡节点回程路由改变，绕美，直接处于半残废状态。即使某移动中转，也效果不好。今天，按着某位大神的思路，将中转节点和cdn结合使用，目前效果满意。



### 环境

do 新加坡节点debian 10 系统
某移动节点 debian 10 系统


### Cloudflare设置信息

1. 回到cloudflare网页上，点击”done, check nameservers”按钮，界面进入证书选择界面，按图中选“full(strict)”：

![image](/image/24.png)


2. 接着点页面下方的“next”，进入加速选项页面。按照图中所示把勾选上：

![image](/image/25.png)


3. 接着点页面下方的“Next”，设置就完成了。如果需要对dns进行解析，点击页面上方的”DNS“进入dns解析设置页面。例如要添加新的解析，先点击“add record”，然后选择解析类型、填写记录名、值，TTL用默认的即可(auto表示600s，比namesilo的3600强了60倍！)。如果的vps使用网页服务，可以选择过代理（即显示黄色的云），仅做dns解析则要点掉黄色的云。信息填写好后点击“save”按钮保存：

![image](/image/26.png)





### 安装xray脚本，选择vmess-ws-tls

```
bash <(curl -sL https://s.hijk.art/v2ray.sh)
```


![image](/image/21.png)
我个人选择5，为了过cdn

![image](/image/22.png)


![image](/image/23.png)


```
IP(address):  123.123.123.123
 端口(port)：443
 id(uuid)：1acae00b-275f-4d9d-8d0f-9068f97dadd2
 流控(flow)：无
 加密(encryption)： none
 传输协议(network)： ws
 伪装类型(type)：none
 伪装域名/主机名(host)：your-domain
 路径(path)：/伪装路径
 底层安全传输(tls)：TLS
```
上述是xray脚本生成的结果

使用Android手机termux，或者本地服务器测试电信，联通，移动脚本联通性

```
curl https://proxy.freecdn.workers.dev/?url=https://raw.githubusercontent.com/badafans/better-cloudflare-ip/master/shell/cf.sh -o cf.sh && chmod +x cf.sh && ./cf.sh
```

将ip改为测试线路最优ip



第五步：设置客户端
打开手机，一般使用v2rayng，在”ip/address”一栏中的ip填写cdn ip，然后，request host 填写伪装域名，/path填写伪装路径，sni填写伪装域名。测试是否能访问谷歌。



经过上述设置，v2ray的web+websokcet+tls+cdn的配置就完成了！快试试能不能打开外网吧！

在上网连通测试完成后，登录你的中转服务器，测试中转服务器对cdn节点的访问速度

```
 ./gost -L=tcp://:中转端口/cdnip:443
```

再次修改ip，改成中转节点ip，端口改成中转节点端口。

这样你的中转节点-----cloudflare cdn-----到你ip xray服务的搭建就完成了，继续快乐的冲浪吧


### 声明
由于本人小白，本文图片部分采用威龙大佬发布v2ray科技文章。不足及错误之处，望大家指正。


<script src="https://utteranc.es/client.js"
        repo="emedsy/starter-academic"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>
