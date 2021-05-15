---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "2021 05 15debian下安装pacs服务器记录及尝试"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2021-05-15T18:49:08+08:00
lastmod: 2021-05-15T18:49:08+08:00
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
## 安装所需应用及版本

- JDK1.8

安装教程地址(包含手动/自动)

- MARIADB

安装教程地址

-wildfly


```
sudo apt-get install -y libboost-all-dev libzmq3-dev libminiupnpc-dev curl git build-essential libtool autotools-dev automake pkg-config bsdmainutils python3 software-properties-common libssl-dev libevent-dev
```


## 在Debian 10 Buster上安装WildFly

步骤1.在安装任何软件之前，请务必apt在终端中运行以下命令，以确保系统是最新的，这一点很重要：

```
sudo apt update
sudo apt upgrade
```


步骤2.安装Java。

运行以下命令以安装OpenJDK：

```
sudo apt install default-jdk
```

在安装完上述OpenJDK之后，您可以运行以下命令来验证其是否已安装：

```
java -version
```

步骤3.创建一个WildFly用户。

我们将创建一个新的名为WildFly的系统用户和组，并带有一个主目录，该目录将运行WildFly服务：***/opt/wildfly***

```
sudo groupadd -r wildfly
sudo useradd -r -g wildfly -d /opt/wildfly -s /sbin/nologin wildfly
```

步骤4.在Debian 10上下载并安装WildFly Jboss。

首先， 在服务器上下载WildFly的最新版本，并使用以下命令将其解压缩：

```
WILDFLY_VERSION=21.0.0.Beta1
wget https://download.jboss.org/wildfly/$WILDFLY_VERSION/wildfly-$WILDFLY_VERSION.tar.gz -P /tmp
```

下载完成后，解压缩tar.gz文件并将其移至目录：/opt

```
sudo tar xf /tmp/wildfly-$WILDFLY_VERSION.tar.gz -C /opt/
```

接下来，创建一个符号链接WildFly，它将指向WildFly安装目录：

```
sudo ln -s /opt/wildfly-$WILDFLY_VERSION /opt/wildfly
sudo chown -RH wildfly: /opt/wildfly

```

步骤5.配置Systemd WildFly。

现在，让我们创建一个将运行WildFly服务的系统用户和组：

```
sudo mkdir -p /etc/wildfly
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.conf /etc/wildfly/
```

然后，通过以下命令在收藏夹编辑器中打开配置文件：


```
sudo nano /etc/wildfly/wildfly.conf
```

```
# The configuration you want to run
WILDFLY_CONFIG=standalone.xml

# The mode you want to run
WILDFLY_MODE=standalone

# The address to bind to
WILDFLY_BIND=0.0.0.0
```

接下来，将WildFly launch.sh脚本复制到目录：/opt/wildfly/bin/


```
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/launch.sh /opt/wildfly/bin/
sudo sh -c 'chmod +x /opt/wildfly/bin/*.sh'
sudo cp /opt/wildfly/docs/contrib/scripts/systemd/wildfly.service /etc/systemd/system/
```

之后，通过执行以下命令来启动WildFly服务：

```
sudo systemctl daemon-reload
sudo systemctl start wildfly
sudo systemctl enable wildfly
```

步骤6.配置防火墙。

您需要允许端口8080上的通信。如果您的Debian默认未安装UFW防火墙应用程序，请运行以下命令以将其安装在系统上：


```
sudo apt install ufw
sudo ufw allow 8080/tcp
```

步骤7.访问WildFly Web界面。

默认情况下，WildFly将在HTTP端口8080上可用。打开您喜欢的浏览器，然后浏览至或完成所需的步骤以完成安装。http://your-domain.com:8080http://server-ip-address:8080

恭喜你！您已经成功安装了WildFly。感谢您使用本教程在Debian 10上安装WildFly Jboss的最新版本。有关其他帮助或有用的信息，我们建议您检查[WildFly官方网站](https://www.wildfly.org/)
