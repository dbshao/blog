---
title: git多账号公钥添加
date: 2019-04-14 22:43:11
categories: Linux
tags:
 -git
 - 多账号
---
<p id="div-border-left-blue">虽说git平时不怎么常用，用的最多的也就是 git clone，但是最为大家都在夸奖的版本控制软件还是要学习一下的，你看这不最近笔者就遇到一个多账号私钥的问题，在这里把问题描述下，也很大将分享下解决办法。主要是在自己的电脑上大部分都是对github进行操作，笔者在入了gcp的坑之后也需要添加秘钥，这样两个公钥就会冲突。</p>
<!--more-->

## 事前准备
无论你是windows，Linux，还是Mac，git软件自己先搞定，一些环境配置也先配置好。下面直接从钥匙的生成说起。

## 配置
```bash
$ ssh-keygen -t rsa -C "邮箱地址"
Generating public/private rsa key pair.
Enter file in which to save the key (~/.ssh/id_rsa):
```
这里会提示输入rsa文件的名字和路径，加入你有很多个，建议在后面加上后缀，如id_rsa_github等，文件的路径也请自己记住（建议C:/Users/你的用户名/.ssh路径）。

Window进入`C:/Users/你的用户名/.ssh`文件夹，右键新建一个文本文件，改名为`config`即可。这里要注意，没有`.ssh`文件夹的要新建一个`.ssh`名的文件夹。

下面编写`config`文件，我以`Github`、`Gitlib`、`OSChina`，局域网为例

```XML
Host github.com
    HostName github.com
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile /home/Workspace/ssh/id_rsa_github
Host gitlib.com
    HostName gitlib.com
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile id_rsa_gitlib
Host oschina.com
    HostName oschina.com
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile /D/Workspace/ssh/id_rsa_oschina
Host 192.168.1.222
    HostName 192.168.1.222
    User smallajax@foxmail.com
    PreferredAuthentications publickey
    IdentityFile /D/Workspace/ssh/id_rsa_oschina
```
解释一下，`HostName`是服务器的地址，`User`是用户名，`PreferredAuthentications`照抄即可，`IdentityFile`是文件的绝对路径，注意盘符前面的`/`
本地配置结束，到各自网站添加相关公钥就可以了。

## 关于多邮箱账户的问题
有人或许会有疑问，我github，gitlab的邮箱用户名不一样怎么办，其实这个是根据项目设置的，命令行进入仓库文件夹再设置。第一种情况是先从Git上pull仓库下来，第二种情况是本地初始化Git仓库，总之进入改仓库文件夹后：

```bash
git config --local user.name "你的名字"
git config --local user.email "你的邮箱"
```
注意配置单个Git帐号时，是不进入项目文件夹就可以，不过不是使用`--local`，而是使用`--globa`l就可以全局配置。

配置项目用户和邮箱完成后，我们可以进入项目文件夹下的`.git`文件夹查看`config`文件内容，大概内容如下：
```
...
[user]
    name = YanZhenjie
    email = smallajax@foxmail.com
```

### 测试
配置全部结束，我们来测试一下配置是否成功：
```bash
ssh -T git@github.com
ssh -T git@gitlib.com
ssh -T git@192.168.1.222
```
### 常见git命令学习
- push代码到某个分值
>git push origin 分支名字

- 关联本地代码到远程分支
>git init
git commit -m "message"
git add .
git remote add origin 远程仓库地址