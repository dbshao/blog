---
title: Linux安装BT客户端
date: 2019-05-12 14:51:17
categories:  Linux
tags: [vps,Linux,BT]
---
{% note warning %}子曰：路漫漫其修远兮，折腾之路永不停止。前面已经折腾完百度，aria2开始进入网上资源的收集模式，百度网盘当然能满足我们的很多需求，可是还是有一些需要我们想写办法的，比如著名的资源网站ourbits{% endnote %}

<!--more-->

## 资源站支持的BT客户端
这里拿著名的资源PT站：`https://ourbits.club/` 作为例子
>`Windows:`
Azureus: 2.5.0.4, 3.0.5.0, 3.0.5.2及后续版本
uTorrent: 1.6.1, 1.7.5, 1.7.6, 1.7.7, 1.8Beta(Build 10364), 2.0(Build 17624)及后续版本
BitTorrent: 6.0.1, 6.0.2, 6.0.3及后续版本
Deluge: 0.5.9.1, 1.1.6及后续版本
qBittorrent: 3.3.0 及后续版本
`Linux:`
Azureus: 2.5.0.4, 3.0.5.0, 3.0.5.2及后续版本
Deluge: 0.5.9.1, 1.1.6及后续版本
Transmission: 1.21及后续版本
rTorrent: 0.8.0（配合libtorrent 0.12.0或后续版本）及后续版本
Enhanced CTorrent: 3.3.2及后续版本
qBittorrent: 3.3.0 及后续版本
`MacOS X:`
Azureus: 2.5.0.4, 3.0.5.0, 3.0.5.2及后续版本
Transmission: 1.21及后续版本
qBittorrent: 3.3.0 及后续版本

## Linux端客户端的选择
网上撸了各种教程，比较下来，`Linux`上推荐`Deluge`，设置方便，有界面支持。

## 安装

```bash
#升级Ubuntu系统

apt-get update
apt-get install python-software-properties

#安装deluge
apt-get install -y software-properties-common
add-apt-repository ppa:deluge-team/ppa
apt-get update && sudo apt-get install  deluged deluge-web


#启动
deluge-web&  #后台运行

#开机启动

cd /etc
nano rc.local
将 `deluge-web`加入进去
```

##使用
访问你的机器http://YourIP:8112 
默认密码是：deluge
然后请立刻修改默认密码。

使用GCP的请修改防火墙设定，详情请参照下面的网站。
https://233blog.com/post/30/

## 注意事项
请大家保护账号，不要只是吸血哦！