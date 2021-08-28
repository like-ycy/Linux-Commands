## 命令简介

DNF (Dandified Yum) 是新一代的RPM软件包管理器。

DNF 包管理器克服了 YUM 包管理器的一些瓶颈，提升了包括用户体验，内存占用，依赖分析，运行速度等多方面的内容。DNF 使用 RPM, libsolv 和 hawkey 库进行包管理操作，Fedora22 已经默认使用 DNF。

```
[root@centos7 ~]# dnf
-bash: dnf: command not found
#CentOS 安装
#安装 epel-release 依赖：
[root@centos7 ~]# yum install epel-release
 
#安装 DNF 包：
[root@centos7 ~]# yum install dnf
```

配置文件所在目录 ：/etc/dnf/dnf.conf

## 为什么要舍弃 Yum 而用 DNF?

有三个主要原因：

- Yum 没有 API 文档。这意味着开发者需要做更多的工作。Yum 开发者写一个调用函数都需要查看 Yum 的代码库，使开发变得缓慢。
- Fedora 将会过渡到 Python3，但 Yum 却没有这个能力，而 DNF 既可以使用 Python2，也可以在 Python3 环境下运行。
- 依赖解决能力长期是 Fedora 软件包管理的阿喀硫斯之踵。DNF 使用基于 SAT 的依赖问题解决方法，与 SUSE 和 OpenSUSE 的 Zypper 类似。

## 语法格式

```
dnf [options] [command] [package ...]
```

## 选项说明

```
#与YUM 基本保持一致，少数用法有区别
--version  #查看DNF包管理器版本
help       #查看所有的DNF命令及其用途
help <command>  #获取命令的使用帮助
history         #查看 DNF 命令的执行历史
repolist        #查看系统中可用的DNF软件库
search <package>     #搜索软件库中的RPM包
list installed       #列出所有安装的RPM包
list available       #列出所有可安装的RPM包
info <package>       #查看软件包详情
provides <file>      #查找某一文件的提供者
install <package>    #安装软件包及其所需的所有依赖
update <package>     #升级软件包
remove <package>     #删除软件包
reinstall <package>  #重新安装特定软件包
distro-sync   #更新软件包到最新的稳定发行版
check-update  #检查系统所有软件包的更新
update        #升级所有系统软件包
clean all     #删除缓存的无用软件包
```

## 应用举例

DNF 安装、卸载

```
[root@centos7 ~]# dnf install package
[root@centos7 ~]# dnf remove  package

#升级软件
[root@centos7 ~]# dnf update
 
#升级系统
[root@centos7 ~]# dnf upgrade
 
#清除 RPM 包缓存
[root@centos7 ~]# dnf clean packages
```

查看 dnf 版本：

```
[root@centos7 ~]# dnf --version
4.0.9
  Installed: dnf-0:4.0.9.2-2.el7_9.noarch at Mon 29 Mar 2021 09:58:48 AM EST
  Built    : CentOS BuildSystem <http://bugs.centos.org> at Wed 07 Apr 2021 03:52:38 PM EST

  Installed: rpm-0:4.11.3-43.el7.x86_64 at Thu 20 Aug 2020 02:49:31 PM EST
  Built    : CentOS BuildSystem <http://bugs.centos.org> at Wed 01 Apr 2020 04:21:52 AM EST
```