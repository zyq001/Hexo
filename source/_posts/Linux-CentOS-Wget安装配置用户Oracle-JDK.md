title: Linux(CentOS) Wget安装配置 [用户] Oracle JDK  
date: 2014-08-15 09:55:56  
tags: [Linux]
categories: [Linux] 
---
背景： 
开发机上的系统JDK是1.6的，由于项目需要1.7，故决定下载一个jdk7，并配置到用户环境变量中；
尝试直接用wget从官网上下，结果下来都是一个几k的文件，应该是oracle上的防盗链，也就是用图形界面要先点accept；
用本地Windows下载好之后通过rz传上去，结果最近网络有点问题，很慢，还经常一半停下来，，

网上搜了一下
  基于wget重定向，可以带一些cookie欺骗orcle，  
  一般都说的加上  

  `--no-cookie --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F"`  
<!-- more -->
如果出现Unable to establish SSL connection的话，在wget后面加上–no-check-certificate即可，即：  

  `wget --no-cookie --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F"`  

而经过测试，起码在我们这边是行不通的，跟不加一样，
  后来看到这篇文章：https://ivan-site.com/2012/05/download-oracle-java-jre-jdk-using-a-script/解决问题。
   完整命令为：  

    wget --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/7u4-b20/jdk-7u4-linux-x64.tar.gz"  


下载完之后

    tar -zxvf *.tar.gz
然后  

    vi ~/.profile  

添加如下  

    export JAVA_HOME=/你的路径/jdk1.7.0_79export CLASSPATH=$JAVE_HOME/lib/export PATH=$JAVA_HOME/bin/:$PATH  

**注意吧$JAVA_HOME/bin/写在前面，不然java -version还是先找到系统的java  **  
然后  
    `source ~/.profile`    



可以换成想要的版本，贴一些：
JDK 8u25

- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-i586.rpm
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-x64.rpm
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-linux-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-macosx-x64.dmg
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-solaris-sparcv9.tar.Z
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-solaris-sparcv9.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-solaris-x64.tar.Z
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jdk-8u25-solaris-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/jdk-8u25-windows-i586.exe
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/jdk-8u25-windows-x64.exe  

JDK 7u72

- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-linux-i586.rpm
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-linux-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-linux-x64.rpm
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-linux-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-macosx-x64.dmg
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-i586.tar.Z
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-x64.tar.Z
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-sparc.tar.Z
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-sparc.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-sparcv9.tar.Z
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-solaris-sparcv9.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-windows-i586.exe
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jdk-7u72-windows-x64.exe  

JRE 8u25

- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-linux-i586.rpm
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-linux-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-linux-x64.rpm
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-linux-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-macosx-x64.dmg
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-macosx-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-solaris-sparcv9.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/jre-8u25-solaris-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/jre-8u25-windows-i586-iftw.exe
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/jre-8u25-windows-i586.exe
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/jre-8u25-windows-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/jre-8u25-windows-x64.exe
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/jre-8u25-windows-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/server-jre-8u25-linux-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/server-jre-8u25-solaris-sparcv9.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b17/server-jre-8u25-solaris-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/8u25-b18/server-jre-8u25-windows-x64.tar.gz  

JRE 7u72

- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-linux-i586.rpm
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-linux-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-linux-x64.rpm
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-linux-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-macosx-x64.dmg
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-macosx-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-solaris-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-solaris-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-solaris-sparc.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-solaris-sparcv9.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-windows-i586-iftw.exe
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-windows-i586.exe
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-windows-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-windows-x64.exe
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/jre-7u72-windows-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/server-jre-7u72-linux-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/server-jre-7u72-solaris-i586.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/server-jre-7u72-solaris-sparc.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/server-jre-7u72-solaris-sparcv9.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/server-jre-7u72-solaris-x64.tar.gz
- http://download.oracle.com/otn-pub/java/jdk/7u72-b14/server-jre-7u72-windows-x64.tar.gz