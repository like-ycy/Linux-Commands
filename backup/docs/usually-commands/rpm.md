## 命令简介

rpm（RPM Package Manager）是一个强大的命令行驱动的软件包管理工具，用来安装、卸载、校验、查询和更新 Linux 系统上的软件包。

## 语法格式

```
rpm [OPTION...]
```

## 选项说明

```
-a, - -all     #查询所有已经安装过的程序包
-i, --install  #安装
-U, --update   #更新升级
-F, --freshen  #刷新，仅更新已安装的软件
-e, --erase    #卸载
-q, --query    #查询
-V, --verify   #校验
-l, --list     #程序安装生成的所有文件列表
-f file   #查询指定的文件由哪个程序包安装生成
-p,- -package package_file  #对未安装的程序包进行查询操作
-v   #显示详细信息
-h   #显示输出进度条，每个#表示2%的进度
-vv  #显示更详细的信息
- -replacepkgs #重新安装
- -nodeps      #安装时，忽略依赖关系
- -test        #测试安装，检查并报告依赖关系及冲突消息等，但并不是真的安装
```

校验结果

```
S file Size differs：文件大小是否发生改变
M Mode differs (includes permissions and file type)：文件类型或文件属性是否发生改变
5 digest (formerly MD5 sum) differs：数据指纹信息的内容已经改变
D Device major/minor number mismatch：设备的主，次代码发生改变
L readLink(2) path mismatch：Link路径已经发生改变
U User ownership differs：文件所属人发生改变
G Group ownership differs：文件所属组发生改变
T mTime differs：文件的创建时间发生改变
P caPabilities differ：功能发生改变
```

## 应用举例

安装

```
[root@centos7 ~]# rpm -ivh httpd-2.4.6-95.el7.centos.x86_64.rpm
```

查询

```
[root@centos7 ~]# rpm -qa|grep httpd
httpd-tools-2.4.6-97.el7.centos.x86_64
httpd-2.4.6-97.el7.centos.x86_64
```

列出程序包相关的信息，版本号、大小、所属的包组等等

```
[root@centos7 ~]# rpm -qi httpd
Name        : httpd
Version     : 2.4.6
Release     : 97.el7.centos
Architecture: x86_64
Install Date: Wed 10 Mar 2021 12:02:10 PM EST
Group       : System Environment/Daemons
Size        : 9821064
License     : ASL 2.0
Signature   : RSA/SHA256, Wed 18 Nov 2020 09:17:43 AM EST, Key ID 24c6a8a7f4a80eb5
Source RPM  : httpd-2.4.6-97.el7.centos.src.rpm
Build Date  : Mon 16 Nov 2020 11:21:17 AM EST
Build Host  : x86-02.bsys.centos.org
Relocations : (not relocatable)
Packager    : CentOS BuildSystem <http://bugs.centos.org>
Vendor      : CentOS
URL         : http://httpd.apache.org/
Summary     : Apache HTTP Server
Description :
The Apache HTTP Server is a powerful, efficient, and extensible
web server.
```

安装后所产生的所有文件列表

```
[root@centos7 ~]# rpm -ql httpd
/etc/httpd
/etc/httpd/conf
/etc/httpd/conf.d
/etc/httpd/conf.d/README
/etc/httpd/conf.d/autoindex.conf
/etc/httpd/conf.d/userdir.conf
/etc/httpd/conf.d/welcome.conf
/etc/httpd/conf.modules.d
/etc/httpd/conf.modules.d/00-base.conf
/etc/httpd/conf.modules.d/00-dav.conf
/etc/httpd/conf.modules.d/00-lua.conf
/etc/httpd/conf.modules.d/00-mpm.conf
/etc/httpd/conf.modules.d/00-proxy.conf
/etc/httpd/conf.modules.d/00-systemd.conf
/etc/httpd/conf.modules.d/01-cgi.conf
/etc/httpd/conf/httpd.conf
/etc/httpd/conf/magic
/etc/httpd/logs
/etc/httpd/modules
/etc/httpd/run
/etc/logrotate.d/httpd
/etc/sysconfig/htcacheclean
.........................省略
```