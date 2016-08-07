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

### 2.1购买云主机

进入[阿里云](https://ecs-buy.aliyun.com/#/prepay)自行按需求购买,注意在系统选择时,选择CentOS 7.0.xx。

### 2.2连接云主机

打开上述提到的命令行终端,键入远程连接命令

```
ssh root@120.25.xxx.xx \\ 这里的IP填写购买云主机时,服务提供商给出的对公网IP
```
接下来,输入密码。通过验证后,即可连接到远程主机。从而进行下一步操作。

### 2.3获取JDK8
直接获取:在终端中键入如下命令

```
wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u92-b14/jdk-8u92-linux-i586.rpm" \\下载JDK
rpm -ivh jdk-8u92-linux-i586.rpm//安装JDK
```

本地上传:进入[JAVA中国](http://www.java.com/zh_CN/),选择当前可用的JDK8的版本,下载完毕后,使用File Zilla来进行上传,然后在终端中执行如下命令

```
cd /root/ \\ 这里的root为你上传文件的目标路径,加入你将文件上传到了/usr/share目录,则应该 使用 cd /usr/share
rpm -ivh jdk-8u92-linux-i586.rpm //这里的文件名为你上传文件的文件名,如果嫌文件名太长,可以使用tab进行自动补齐,例如 rpm -ivh jdk- 然后按下tab,系统会自动将文件名补齐
```
验证JAVA的安装:

在命令行终端中键入如下命令

```
java -version
```
如果正确的现实了版本号,则表示java环境已经安装成功。

除此之外,我们还需要**配置JAVA环境变量**,使我们能更轻松的使用java命令。

这里,我们要做的就是修改系统环境变量文件。

在终端中键入如下命令,来查看和编辑配置文件:

```
vi + /etc/profile
```

向文件里面追加以下内容：

```
JAVA_HOME=/usr/java/jdk1.8.0_92 ## 这里的文件路径为主机上的文件路径,请自己参照当前主机的安装路径来填写,如果不清楚java安装在什么位置,可使用 whereis java来查找java的安装位置。
JRE_HOME=/usr/java/jdk1.8.0_92/jre ## 同上
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export JAVA_HOME JRE_HOME PATH CLASSPATH
```
验证环境变量的配置是否成功,在命令行中键入如下命令:

```
source /etc/profile   //刷新配置文件,使更改立即生效
echo $PATH   //查看当前的PATH值
```
如果在打印结果中看到了刚才配置的两个路径,则表示JDK环境安装成功!


### 2.4获取Nukkit核心

直接获取:在命令行中键入如下命令:

```
wget http://ci.mengcraft.com:8080/job/nukkit/lastSuccessfulBuild/artifact/target/nukkit-1.0-SNAPSHOT.jar
```
本地上传:进入Nukkit官网,下载Nukkit核心文件之后,使用File Zilla来进行上传。

### 2.5启动Minecraft Serve服务

进入nukkit对应的jar文件目录,比如我将文件'nukkit-1.0-SNAPSHOT.jar'放在了 /home/ranger/nukkit目录下,在命令行中键入如下命令

```
cd /home/ranger/nukkit
java -jar nukkit-1.0-SNAPSHOT.jar
```
这样就将服务启动起来了。初次启动,服务会询问一些问题,例如使用哪种语言,服务将运行在哪个端口等等这些问题,统一使用默认配置就可以了。

## 3.发布服务器

### 3.1检查端口是否对外开放

默认的情况下,minecraft serve服务运行在19132端口。但是云主机的防火墙默认情况下,该端口是不对外开放的。这时候需要我们手动将该端口开放给公网,使得互联网上的所有用户都能访问这个端口。

CentOS7中,使用了新的防火墙firewall,这里我们使用原本可配置的iptables来作为防火墙。

* 3.1.1关闭firewall：在命令行当中键入如下命令:

```
systemctl stop firewalld.service #停止firewall
systemctl disable firewalld.service #禁止firewall开机启动
```

* 3.1.2安装iptables防火墙,在命令行当中键入如下命令:

```
yum install iptables-services #安装
```

* 3.1.3对外开放19132端口：在命令行当中查看和编辑'iptables':

```
vi /etc/sysconfig/iptables
```
在文件中添加如下记录:

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 19132 -j ACCEPT #允许19132端口tcp协议通过防火墙
-A INPUT -m state --state NEW -m tcp -p udp --dport 19132 -j ACCEPT #允许19132端口udp协议通过防火墙
```

* 3.1.4重启防火墙:在命令行当中键入如下命令

```
service iptables save #保存刚才的更改
service iptables restart #重启启动iptables服务
```

### 3.2发布服务器

使用'ifconfig'命令查看服务器的公网IP,在命令行当中键入命令

```
ifconfig
```
就可以查看服务器的公网IP了,比如我这里我的公网IP为120.25.96.xxx,我会向我的小伙伴们宣布,我的服务器的地址是 120.25.96.xxx:19132,大家可以通过连接这个地址来加入服务器,一起玩耍。

至此,我们已经可以对外提供Minecraft Serve服务了。

### *更优雅的发布自己的服务器:

有的时候,我们并不像暴露自己的服务器IP给大家,而是通过一个网址来让大家连接到服务器来。这时候,就需要我们自己拥有一个个性的域名。比如我这里使用的域名是 xianyu.io。那我就需要在我的DNS解析记录当中添加一条A类解析条目。比如让host:minecraft指向IP:120.25.96.xxx,这样我们就不用再记那么麻烦而又冗长的IP了,只需要告诉小伙伴们,通过连接minecraft.xianyu.io:19132就可以了。而且,使用域名的另外一个优点就是,当我们的服务器IP更换了之后,我们只需要更改自己的DNS解析记录就可以了,用户不需用做任何改动,一样能继续进行游戏。


### 一些问答:

**Q:为什么选择阿里云的ECS?**

A:考虑到以后的玩家多集中在中国大陆区域,所以选择国内的云主机。

**Q:为什么选择Linux系统?**

A:Linux对服务器资源利用的更加充分。至少不必浪费性能在无用的GUI上。

**Q:为什么选择Nukkit,而不是PocketMine-mp?**

A:Nukkit是一个新的尚处于开发中的MCPE服务端软件,相较于PocketMine-mp,Nukkit还很新,但是由于Nukkit采用java开发,其多线程模块带来的性能提升,是PocketMine-mp所无法比拟的。相同配置下的Nukkit能表现的比PocketMine-mp更为出色。