---
layout: layout
title: '安装aria2和图形界面的配置'
date: 2019-03-31 17:11:37
categories: Linux
tags: [linux,aria2,caddy]
---

<p id="div-border-top-purple">前面已经有教程，可以一键安装Aria2+Caddy+Rclone+GDlist+Aria2Ng+Google Drive到服务器的一个工具，但很多
网友可能会觉得晕晕乎乎的，然后又写服务也不是必须的，现在就把aria2和他的图形界面单独拿拉出来说说</p>

<!--more-->

### 安装aria2
虽然aria2现在已经支持install安装了，这里还是给出逗比大佬的安装脚本，本人觉得特别好用。

```bash
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubiBackup/doubi/master/aria2.sh && chmod +x aria2.sh && bash aria2.sh
#备用地址
wget -N --no-check-certificate https://www.moerats.com/usr/shell/Aria2/aria2.sh && chmod +x aria2.sh && bash aria2.sh
```
##### aria2常见命令
```bash
启动：service aria2 start
停止：service aria2 stop
重启：service aria2 restart
查看状态：service aria2 status
配置文件：/root/.aria2/aria2.conf（配置文件包含中文注释，但是一些系统可能不支持显示中文）
下载目录：/usr/local/caddy/www/aria2/Download（该目录为Github下载安装的，而备用地址下载的默认为/usr/local/caddy/www/file）
```
### 安装 caddy
```
wget https://git.io/vra5C -O - -o /dev/null|bash
caddy install
会要求你输入域名和邮箱，自动帮你签发ssl。然后使用caddy start命令运行caddy。
```
##### 常用命令
```bash
caddy start  #开启Caddy Web Server
caddy stop  #停止Caddy Web Server
caddy reload  #重载Caddy Web Server
caddy restart  #重启Caddy Web Server
caddy status  #查看Caddy Web Server状态
caddy install  #安装Caddy Web Server
caddy edit  #编辑配置文件Caddyfile
caddy service  #使Caddy Web Server成为一项服务(upstart/systemd)
caddy update  #升级Caddy Web Server
caddy delete  #卸载Caddy and data
caddy about  #关于Caddy Web Server
caddy version  #检测脚本/Caddy/PHP5-fpm版本信息
```

### 安装AriaNg
`AriaNg`下载地址：<https://github.com/mayswind/AriaNg/releases>

```bash
yum install unzip  #CentOS系统
apt-get install unzip  #Debian和Ubuntu系统
cd /var/caddywww && rm -rf index.html
wget https://github.com/mayswind/AriaNg/releases/download/0.3.0/aria-ng-0.3.0.zip
unzip aria-ng-0.3.0.zip
```

### 安装webui-aria2
` webui-aria2`下载地址：<https://github.com/ziahamza/webui-aria2>

```bash
yum install git  #CentOS系统
apt-get install git  #Debian和Ubuntu系统
cd /var/caddywww && rm -rf index.html
git clone https://github.com/ziahamza/webui-aria2.git
mv webui-aria2/* /var/caddywww
```