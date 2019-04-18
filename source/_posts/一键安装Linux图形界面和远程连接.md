---
title: 一键安装桌面环境和RDP远程桌面连接
date: 2019-03-31 23:14:37
categories: Linux
tags: [桌面环境,RDP,远程桌面]
---

<p id="div-border-left-purple">这段时间可算是是折腾的够呛，为了把群晖nas的东西移动到google driver可谓是想了好多办法，虽然群晖nas自带备份到云盘服务，但是我们伟大的墙，让这个不能用，本来直接路由器翻墙就能解决的问题，可是人在国外实在是无奈，网上也有介绍用dock安装小飞机的方法，这边试了下，也没有搞定，网上有大神试过的给点意见，也许是我的shadowsocks服务不好。也在网上试过通过nfs服务挂载到linux的方法，可是我的服务器连不上我的群辉nas真的是没办法。只能想个本办法，把群晖的东西分享出来在下载了，所以这篇文章就有了</p>

<!--more-->

### 功能介绍
1，一键安装，你需要全新的Linux系统，最低硬件要求是：CPU核心≥1，内存≥1GB，磁盘空间≥15GB
2，创建3GB内存交换
3，安装了中文环境支持
4，默认安装chrome，firefox
5，安装远程桌面客户端

```bash
#下载脚本
wget --no-check-certificate -qO ~/Linux-Remote-Desktop-Environment.sh 'https://tech.cxthhhhh.com/tech-tools/Linux-Remote-Desktop-Environment/Linux-Remote-Desktop-Environment.sh' && chmod a+x ~/Linux-Remote-Desktop-Environment.sh

#CentOS 7+安装
bash ~/Linux-Remote-Desktop-Environment.sh -CentOS
#Debian 9+安装
bash ~/Linux-Remote-Desktop-Environment.sh -Debian
#Ubuntu 18.04+安装
bash ~/Linux-Remote-Desktop-Environment.sh -Ubuntu
```
网上的大佬还对这个脚本遇到的一些问题做了归纳大致如下

1、完成后。你就可以连接IP:3389（通过远程桌面连接）。RDP登陆账号密码就是您的系统账户和密码。
(root用户和RdpUser用户均可登陆，root密码是您自己设置的密码，RdpUser密码为默认密码)
2、创建新用户时，请授权新用户RDP远程连接。 你需要这样做。（我将演示创建新用户CXT）
```
#输入useradd -m CXT创建用户或者在[控制中心]-[用户和组群]创建新用户CXT。(为CXT设置密码passwd CXT)
#使用root用户切换进入到CXT的目录。
cd /home/CXT
#输入下面的命令(你需要注意，下面命令中引号是”英文状态单引号”。)
touch ./.Xclients
echo 'mate-session' > ./.Xclients
chmod a+x ./.Xclients
#(可选)如果您是Debian/Ubuntu用户，新建用户后需要运行Windows程序，出现中文乱码请参照第9条的方案处理。(CentOS/Redhat无此问题)
```    
3、Chrome浏览器不能通过root用户运行。如果您需要运行，请新建账户。(或者附加运行命令 –no-sandbox)
4、一些Windows应用程序不工作，也许需要您关闭SELinux。（不推荐，一般情况下不需要）
5、一些Windows软件看起来模糊，你需要调整软件后面的背景颜色为暗色调。（例如更换壁纸为深色壁纸）
6、现在，你已经有了浏览器，我相信你可以完成很多的事情了。
7、如果你是Debian/Ubuntu用户，你需要修改部分一键脚本进行手动安装。
8、当前的默认系统语言是中文。如果您是英语用户，请执行’ sudo localectl set-locale LANG = en_US.UTF-8 ‘
```
9、Debian/Ubuntu系统下，由您新建的用户，运行Wine可能会出现中文乱码，需要您执行以下命令(以新建CXT用户为例)。
#运行命令
su - CXT -c 'mkdir -p /home/CXT/.wine/drive_c/windows/Fonts/'
cp -rf ~/.wine/drive_c/windows/Fonts/* /home/CXT/.wine/drive_c/windows/Fonts/
chown -R CXT:CXT /home/CXT/.wine/drive_c/windows/Fonts/*
```
10、一般情况下不建议使用OVZ服务器运行本程序。当然如果您想使用OVZ虚拟化的服务器，请注意：
#Swap Memory不会生效，因此你的内存必须≥2GB+。
#你需要等待Swap Memory创建完成后，立即开启新SSH窗口，删除Swap挂载。
#挂载的设置文件在这里(/etc/fstab)，删掉(/var/swapd swap swap default 0 0)。
#删除文件(/var/swapd)。

文章来源：<https://tech.cxthhhhh.com/linux/2018/08/08/original-one-click-installation-of-desktop-environment-rdp-windows-support-for-linux-cn.html>