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



### 一些问答:

**Q:为什么选择阿里云的ECS?**

A:考虑到以后的玩家多集中在中国大陆区域,所以选择国内的云主机。

**Q:为什么选择Linux系统?**

A:Linux对服务器资源利用的更加充分。至少不必浪费性能在无用的GUI上。

**Q:为什么选择Nukkit,而不是PocketMine-mp?**

A:Nukkit是一个新的尚处于开发中的MCPE服务端软件,相较于PocketMine-mp,Nukkit还很新,但是由于Nukkit采用java开发,其多线程模块带来的性能提升,是PocketMine-mp所无法比拟的。相同配置下的Nukkit能表现的比PocketMine-mp更为出色。