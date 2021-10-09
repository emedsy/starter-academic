---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 10 09V2board搭建的尝试"
subtitle: "V2board面板"
summary: "在结点的分享和使用中，v2board采用aapanel搭建"
authors: [amin]
tags: []
categories: []
date: 2021-10-09T22:22:18+08:00
lastmod: 2021-10-09T22:22:18+08:00
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

对于，小白自建结点，结点的设置经常改变，对于结点的分享尤其多个人的分享，需要一个方便可行的方法
所以，我采用机场的面板，通过相对固定的分享链接，使分享及调整结点简单化。本文主要采用v2board面板作为前端，对接xrayr作为后端对接。
### <mark>安装宝塔aapanal<mark>


### <mark>aapanal的手动部署<mark>

### ~~<mark>后端的xrayr的对接<mark>~~



---



### <mark>安装宝塔aapanal<mark>

最低配置要求为1Core/512M RAM
php>=7.3，nginx>=1.17，mysql	5.x，redis

#### Ubuntu/Deepin安装脚本
```
wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh
```

### <mark>管理宝塔aapanal<mark>
#### 宝塔工具箱(包含下列绝大部分功能 直接ssh中执行bt命令 仅限6.x以上版本面板)
```
bt
```
#### 停止
```
/etc/init.d/bt stop
```
#### 启动
```
/etc/init.d/bt start/restart
```
#### 卸载

```
/etc/init.d/bt stop && chkconfig --del bt && rm -f /etc/init.d/bt && rm -rf /www/server/panel
```
[详细操作可见https://www.bt.cn/btcode.html](https://www.bt.cn/btcode.html)

选择使用LNMP的环境安装方式勾选如下信息

☑️ Nginx 1.17
☑️ MySQL 5.6
☑️ PHP 7.3

选择 Fast 快速编译后进行安装。
#### 安装Redis、fileinfo

aaPanel 面板 > App Store > 找到PHP 7.3点击Setting > Install extentions > redis,fileinfo 进行安装

#### 解除被禁止的函数

aaPanel 面板 > App Store > 找到PHP 7.3点击Setting > Disabled functions 将 putenv proc_open pcntl_alarm pcntl_signal 从列表中删除。

#### 添加站点

aaPanel 面板 > Website > Add site。

在 Domain 填入你指向服务器的域名
在 Database 选择MySQL
在 PHP Verison 选择PHP-73

#### 安装V2Board
通过SSH登录到服务器后访问站点路径如：/www/wwwroot/你的站点域名。

以下命令都需要在站点目录进行执行。

```
# 删除目录下文件
chattr -i .user.ini
rm -rf .htaccess 404.html index.html .user.ini
```

#### 执行命令从 Github 克隆到当前目录。

```
git clone https://github.com/v2board/v2board.git ./
```

#### 执行命令安装依赖包以及V2board

```
sh init.sh
```
根据提示完成安装


#### 配置站点目录及伪静态
添加完成后编辑添加的站点 > Site directory > Running directory 选择 /public 保存。

添加完成后编辑添加的站点 > URL rewrite 填入伪静态信息。
```
location /downloads {
}

location / {  
    try_files $uri $uri/ /index.php$is_args$query_string;  
}

location ~ .*\.(js|css)?$
{
    expires      1h;
    error_log off;
    access_log /dev/null;
}
```
#### 配置定时任务
aaPanel 面板 > Cron。

在 Type of Task 选择 Shell Script
在 Name of Task 填写 v2board
在 Period 选择 N Minutes 1 Minute
在 Script content 填写 php /www/wwwroot/路径/artisan schedule:run

根据上述信息添加每1分钟执行一次的定时任务。

#### 启动队列服务

V2board的邮件系统强依赖队列服务，你想要使用邮件验证及群发邮件必须启动队列服务。下面以aaPanel中nodejs的PM2服务来守护队列服务作为演示。

aaPanel 面板 > App Store > Deployment

找到PM2 Manager 4.2.2进行安装，安装完成后按照如下填写

在 Project root directory 选择站点目录
在 Startup file name 填写 pm2.yaml
在 project name 填写 v2board

填写后点击Add添加即可运行。当然你也可以使用supervisor进行守护。


{{% callout note %}}
aaPanel在安装PM2的时候可能会造成问题无法安装，你可以手动进行PM2安装。如何安装可以参考Google
{{% /callout %}}


### <mark>常见问题<mark>

Q：500错误
A：检查站点根目录权限，递归755，保证目录有可写文件的权限，也有可能是Redis扩展没有安装或者Redis没有按照造成的。你可以通过查看storage/logs下的日志来排查错误或者开启debug模式。
