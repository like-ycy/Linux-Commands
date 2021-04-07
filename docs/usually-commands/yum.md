## 命令简介

yum 命令是基于 RPM 的软件包管理器。

yum 可以自动执行系统更新，包括依赖关系分析和基于“存储库”元数据的过时处理。它还可以执行新软件包的安装，旧软件包的删除以及对已安装或可用软件包以及其他命令/服务的查询。yum 命令类似于 apt-get 和 smart 等其他高级软件包管理器。

## 语法格式

```
yum [options] [command] [package ...]
```

## 选项说明

```
-h  #显示帮助信息
-y  #对所有提示，都是“yes”确认
-c  #指定配置文件
-q  #安静模式
-v  #详细模式
-d  #设置调试等级（0-10）
-e  #设置错误等级（0-10）
-R  #设置yum处理一个命令的最大等待时间
-C  #完全从缓存中运行，而不去下载或者更新任何头文件

install  #安装rpm软件包
update   #更新rpm软件包
check-update  #检查是否有可用的更新rpm软件包
remove  #删除指定的rpm软件包
list    #显示软件包的信息
search  #检查软件包的信息
info    #显示指定的rpm软件包的描述信息和概要信息
clean   #清理yum过期的缓存
shell   #进入yum的shell提示符
resolvedep     #显示rpm软件包的依赖关系
localinstall   #安装本地的rpm软件包
localupdate    #显示本地rpm软件包进行更新
deplist        #显示rpm软件包的所有依赖关系
```

## 应用举例

安装

```
yum install              #全部安装
yum install package1     #安装指定的安装包package1
yum groupinsall group1   #安装程序组group1
```

更新和升级

```
yum update               #全部更新
yum update package1      #更新指定程序包package1
yum check-update         #检查可更新的程序
yum upgrade package1     #升级指定程序包package1
yum groupupdate group1   #升级程序组group1
```

查找和显示

```
# 检查 MySQL 是否已安装
yum list installed | grep mysql

#显示安装包httpd的所有信息
[root@centos7 ~]# yum info httpd
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * epel: mirrors.bfsu.edu.cn
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
Installed Packages
Name        : httpd
Arch        : x86_64
Version     : 2.4.6
Release     : 97.el7.centos
Size        : 9.4 M
Repo        : installed
From repo   : updates
Summary     : Apache HTTP Server
URL         : http://httpd.apache.org/
License     : ASL 2.0
Description : The Apache HTTP Server is a powerful, efficient, and extensible
            : web server.

yum list    #显示所有已经安装和可以安装的程序包
#显示httpd程序的安装情况
[root@centos7 ~]# yum list httpd
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * epel: mirrors.bfsu.edu.cn
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
Installed Packages
httpd.x86_64                                2.4.6-97.el7.centos                                 @updates

yum search string      #根据关键字string查找安装包
```

删除程序

```
yum remove | erase package1   #删除程序包package1
yum groupremove group1        #删除程序组group1
```

查看程序httpd安装包的依赖情况

```
[root@centos7 ~]# yum deplist httpd
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * epel: mirrors.bfsu.edu.cn
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
package: httpd.x86_64 2.4.6-97.el7.centos
  dependency: /bin/sh
   provider: bash.x86_64 4.2.46-34.el7
  dependency: /etc/mime.types
   provider: mailcap.noarch 2.1.41-2.el7
  dependency: /usr/sbin/groupadd
   provider: shadow-utils.x86_64 2:4.6-5.el7
 .......................
  dependency: rtld(GNU_HASH)
   provider: glibc.x86_64 2.17-323.el7_9
   provider: glibc.i686 2.17-323.el7_9
  dependency: system-logos >= 7.92.1-1
   provider: centos-logos.noarch 70.0.6-3.el7.centos
  dependency: systemd-units
   provider: systemd.x86_64 219-78.el7_9.3
```

清除缓存

```
yum clean packages       #清除缓存目录下的软件包
yum clean headers        #清除缓存目录下的 headers
yum clean oldheaders     #清除缓存目录下旧的 headers
```

查看可批量安装的组列表

```
[root@centos7 ~]# yum grouplist
Loaded plugins: fastestmirror
There is no installed groups file.
Maybe run: yum groups mark convert (see man yum)
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * epel: mirrors.bfsu.edu.cn
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
Available Environment Groups:
   Minimal Install
   Compute Node
   Infrastructure Server
   File and Print Server
   Cinnamon Desktop
   MATE Desktop
   Basic Web Server
   Virtualization Host
   Server with GUI
   GNOME Desktop
   KDE Plasma Workspaces
   Development and Creative Workstation
Available Groups:
   Cinnamon
   Compatibility Libraries
   Console Internet Tools
   Development Tools
   Educational Software
   Electronic Lab
   Fedora Packager
   General Purpose Desktop
   Graphical Administration Tools
   Haskell
   LXQt Desktop
   Legacy UNIX Compatibility
   MATE
   Milkymist
   Scientific Support
   Security Tools
   Smart Card Support
   System Administration Tools
   System Management
   TurboGears application framework
   Xfce
Done
```

查看组Xfce的所有信息

```
[root@centos7 ~]# yum groupinfo Xfce
Loaded plugins: fastestmirror
There is no installed groups file.
Maybe run: yum groups mark convert (see man yum)
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * epel: mirrors.bfsu.edu.cn
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com

Group: Xfce
 Group-Id: xfce-desktop
 Description: A lightweight desktop environment that works well on low end machines.
 Mandatory Packages:
   +Thunar
   +xfce4-panel
   +xfce4-session
   +xfce4-settings
   +xfconf
   +xfdesktop
   +xfwm4
 Default Packages:
   +NetworkManager-gnome
   +gdm
   +leafpad
   +openssh-askpass
   +orage
   +polkit-gnome
   +thunar-archive-plugin
   +thunar-volman
   +tumbler
   +xfce4-appfinder
   +xfce4-icon-theme
   +xfce4-power-manager
   +xfce4-pulseaudio-plugin
   +xfce4-session-engines
   +xfce4-terminal
   +xfwm4-theme-nodoka
 Optional Packages:
   xfwm4-themes
 Conditional Packages:
   +pinentry-gtk
```