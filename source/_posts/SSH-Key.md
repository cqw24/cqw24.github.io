---
title: SSH
date: 2015-01-01 15:08:35
tags: 
	- SSH Key
	- git
---

## 简介
 <p style="text-indent:2em">SSH(Secure Shell)，是一种网络协议，用于计算机之间的加密登录，利用SSH协议可以有效的放置远程管理过程中的信息泄露问题。在远程登录的时候，使用密码登录每次都必须输入密码，非常麻烦。SSH提供了公钥（SHH Key）登录，可以省去密码输入的步骤，具体流程如下：</p>

<!-- more -->

> 1. 用户将自己的公钥储存在远程主机上
> 2. 登录的时候远程会给用户发送一串随机字符串，用户用自己的**私钥**加密后再发送给远程主机
> 3. 远程主机用已储存的公钥进行解密，解密成功则代表用户是可信的，就可以直接登录不需密码

## SSH在git上的使用
<p style="text-indent:2em">git是分布式的代码管理工具，远程的代码管理是基于ssh的，所以要使用远程的git则需要ssh的配置。</p>
> &emsp;首先，使用代码管理工具把本地的代码上传到服务器时需要加密处理，而git使用的是RSA。RSA要解决的一个核心问题是，如何使用一对特定的数字，使其中一个数字可以用来加密，而另外一个数字可以用来解密。这两个数字就是在使用git和github，gitlab的时候所遇到的公钥以及私钥。
> &emsp;其中，公钥就是那个用来加密的数字，这也就是为什么你在本机生成了公钥之后，要上传到github的原因。从github发回来的，用那公钥加密过的数据，可以用你本地的私钥来还原。

> <font color=red>注：</font>如果你的key丢失了，不管是公钥还是私钥，丢失一个都不能用了。解决方法：删除原有的密钥，重新再生成一次，然后再设置一次就行。在个人电脑生成密钥后，会同时生成一个公钥和一个私钥，默认情况下在用户主目录下的`.ssh`目录中，密钥为`id_rsa`，公开密钥为`id_rsa.pub`。

## 生成SSH Key

* 检查电脑是否已存在SSH Key，若已有SSH Key则拷贝到粘贴板上，若无SSH Key则生成SSH Key
```
ls -al ~/.ssh 
```

* 生成SSH Key，后面为自己常用的邮箱
```
ssh-keygen -t rsa -C "your_email@example.com"

//下面是选择生成密钥存放的文件位置，直接回车密钥将按照默认问价进行存储 
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/you/.ssh/id_rsa): [Press enter] 

//下面是给密钥设置密码的，可以直接按回车，即不设置密码 
Enter passphrase (empty for no passphrase): [Type a passphrase]
Enter same passphrase again: [Type passphrase again]   
```

* 拷贝已生成的SSH Key
```
pbcopy < ~/.ssh/id_rsa.pub
```