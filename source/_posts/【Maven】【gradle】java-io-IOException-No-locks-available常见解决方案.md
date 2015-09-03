title: '【Maven】【gradle】java.io.IOException: No locks available常见解决方案' 
date: 2015-05-03 09:55:02  
tags: [Maven, gradle]  
categories: [研发管理, maven/gradle]   
---

thumbnail: /images/maven_tb.png
banner: /images/maven_bner.png

    Java.io.IOException: No locks available
        at sun.nio.ch.FileChannelImpl.lock0(Native Method)
        at sun.nio.ch.FileChannelImpl.lock(FileChannelImpl.java:784)
        at java.nio.channels.FileChannel.lock(FileChannel.java:865)

能够下载依赖的jar包，但是每下载一次都会跑出**No locks available**异常，而且每个jar下载都需要等待很久。

最后通过 df   -T   -h 命令才发现当前目录挂载的是NFS。  
<!-- more -->
传送门：NFS介绍  
http://book.51cto.com/art/200808/85167.htm  
http://fedora.linuxsir.org/main/?q=node/41

这一般是因为 /home/* , /global,以及常用的/diskN是独立的，为了方便在任何一台机器上都可以访问/home和/global,所以这两个目录做的非本地的（也就是NFS）

Maven 和 gradle的默认本地仓库是home下的 如/home/userName/.gradle（或者.m2）

网上搜到的解决方案  
1、启用NFS filesystem lock服务  
2、换个本地的filesystem  
**实际上 **   
1. 公司的开发机，一般用户是没有roo权限的，所以方法1不能实现    
2. 关于2,  以下是具体操作：   
&#8195;&#8195; **Maven：**   
&#8195;&#8195;**settings.xml**文件中的： `<localRepository>/disk1/username/.m2/</localRepository>`  设置到一个非NFS的Disk(本地, 如disk1，disk2，之类的)上。基本的maven 安装和配置网上有很多。  

&#8195;&#8195;**Gradle：**    
&#8195;&#8195;1. 本地安装的Gradle 则修改   gradle目录下的 bin/gradle（Windows是bin/gradle.bat文件） 
`GRADLE_OPTS=-Dgradle.user.home=/disk1/userName/gradle#`添加这一行~  
&#8195;&#8195;2. 项目自带的gradlew（如某些采用gradle构建的开源项目 LinkedIn Gobblin）则修改gradlew文件也是添加那一行
 

参考：  
http://blog.csdn.net/liu251/article/details/7431696  
http://www.vicviz.com/gradle-in-action-bi-ji/  