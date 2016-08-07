---
layout: post
title:  "Build MinecraftPE Server"
date:   2016-08-07 02:49:37
author: Ranger
overview: 
categories: game minecraft
---
 
## 1.准备:
 * 一台拥有公网IP的VPS云主机(系统为Linux)。比如**[阿里云](https://ecs-buy.aliyun.com/#/prepay)**的ECS或者**[Linode](https://www.linode.com/linodes)**的VPS。本文选择的主机为阿里云ECS。
 * Minecraft服务器端软件[Nukkit](http://nukkit.io/)或[PocketMine-mp](https://www.pocketmine.net/)。本文选择的服务端软件为Nukkit。
 * 一个自主注册的域名(非必须)。本文选择的域名为 xianyu.io,host为minecraft。
 * 服务端必备的一些模块:screen,jdk8。远程访问端需要的模块:bash终端环境(比如Unix下的terminal)。window平台可以使用[cygwin](https://www.cygwin.com)或其他终端连接软件(如:[putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)、[SSH client](http://ultra.pr.erau.edu/~jaffem/tutorial/SSH_secure_shell_client.htm))。

## 2.搭建服务:

### 2.1

### 一些问答:

**Q:为什么选择阿里云的ECS?**

A:考虑到以后的玩家多集中在中国大陆区域,所以选择国内的云主机。

**Q:为什么选择Linux系统?**

A:Linux对服务器资源利用的更加充分。至少不必浪费性能在无用的GUI上。

**Q:为什么选择Nukkit,而不是PocketMine-mp?**

A:Nukkit是一个新的尚处于开发中的MCPE服务端软件,相较于PocketMine-mp,Nukkit还很新,但是由于Nukkit采用java开发,其多线程模块带来的性能提升,是PocketMine-mp所无法比拟的。相同配置下的Nukkit能表现的比PocketMine-mp更为出色。