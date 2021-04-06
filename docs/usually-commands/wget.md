## 命令简介

wget 命令是 Linux 系统一个免费实用的文件下载工具，支持 HTTP、HTTPS，或者 FTP。

wget 下载它是非交互式的，可以在后台运行，这就表明你可以事先登录到系统，启动一个下载的动作，然后退出系统让wget自动在后台将这个动作执行完成（下载完成）。wget 非常稳定，它在带宽不足或网络不稳定的情况下，如果产生下载失败，那么 wget 会不断的尝试下载动作，直至整个下载过程完成。

## 语法格式

```
wget [option]... [URL]...
```

## 选项说明

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPp3mZuDEdHGKtovuHxXkX1dyr15bKAAwpefS0hQtPgnOdqnJSLUP3riaHKsabzSRbWHREviat5zdo3w/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)wget 命令的选项参数特别的多，本文不会全部介绍，只介绍常用的，感兴趣的读者可以自己在系统中查看帮助信息。

启动选项

```
-V, –-version  #打印wget的版本后退出
-h, –-help     #打印帮助
-b, –-background  #启动后转入后台执行
```

记录和输入文件选项

```
-o, –-output-file=FILE    #将记录信息写入指定的FILE文件中
-a, –-append-output=FILE  #将记录信息追加到指定的FILE文件中
-d, –-debug    #打印调试信息并输出
-i, –-input-file=FILE  #下载指定FILE文件中出现的URLs
-F, –-force-html  #将输入文件当作HTML格式文件来处理
```

下载选项

```
-t, –-tries=NUMBER         #配置最大尝试链接次数(0 表示无限制).
-O –-output-document=FILE  #把文档写到FILE文件中
-c, –-continue      #接着下载末下载完成的文件
-T, –-timeout=SECONDS   #配置响应超时的秒数
-w, –-wait=SECONDS   #指定两次尝试之间间隔SECONDS秒
–waitretry=SECONDS   #指定在重新链接之间等待1…SECONDS秒
–limit-rate=RATE    #配置限制下载输率
```

目录选项

```
-nd –-no-directories     #不创建目录
-x, –-force-directories  #强制创建目录
-nH, –-no-host-directories  #不创建主机目录
-P, –-directory-prefix=PREFIX  #将文件保存到目录 PREFIX/…
```

HTTP 选项

```
-–http-user=USER     #指定HTTP用户名为 USER.
-–http-passwd=PASS   #指定http密码为 PASS
-–proxy-user=USER    #指定代理的用户名为 USER
-–proxy-passwd=PASS  #指定代理的密码为 PASS
-C, –-cache=on/off   #允许/不允许服务器端的数据缓存
-s, –-save-headers   #保存HTTP头到文件
–-cookies=off        #不使用 cookies
```

HTTPS 选项

```
--no-check-certificate   #下载文件时，不验证服务器的证书
--certificate=FILE       #指定客户端证书文件
--certificate-type=TYPE  #指定客户端证书类型
--private-key=FILE       #指定私钥文件
--private-key-type=TYPE  #指定私钥文件类型
```

FTP选项

```
-–passive-ftp   #使用被动传输模式
-–active-ftp    #使用主动传输模式
-–retr-symlinks  #在递归的时候，将链接指向文件(而不是目录)
```

## 应用举例

从 www.mingongge.com下载默认的主页文件（index.htm），将该文件保存到当前工作目录

```
wget https://www.mingongge.com
```

从www.mingongge.com下载文件 mysql_backup.tar.gz，并将下载的带宽使用限制为 20k/s。

```
wget --limit-rate=20k https://www.mingongge.com/backup/mysql_backup.tar.gz
```

从www.mingongge.com下载文件 mysql_backup.tar.gz，如果之前下载过此文件（当前目录存在此文件）将从断开的地方继续下载，即断点续传功能。

```
wget -c https://www.mingongge.com/backup/mysql_backup.tar.gz
```

后台下载www.mingongge.com/backup/mysql_backup.tar.gz

```
wget -b https://www.mingongge.com/backup/mysql_backup.tar.gz
```

察看后台下载进度

```
[root@CentOS7-1 ~]# wget -b https://downloads.mysql.com/archives/get/p/23/file/mysql-5.7.32-el7-x86_64.tar.gz
Continuing in background, pid 1974.
Output will be written to ‘wget-log’.
[root@CentOS7-1 ~]# tail -f wget-log
 59100K .......... .......... .......... .......... ..........  8% 9.53M 64s
 59150K .......... .......... .......... .......... ..........  8% 10.5M 64s
 59200K .......... .......... .......... .......... ..........  8% 11.4M 64s
 59250K .......... .......... .......... .......... ..........  8% 9.05M 64s
 59300K .......... .......... .......... .......... ..........  8% 11.0M 64s
 59350K .......... .......... .......... .......... ..........  8% 9.75M 64s
 59400K .......... .......... .......... .......... ..........  8% 10.8M 64s
 59450K .......... .......... .......... .......... ..........  8% 9.00M 64s
 59500K .......... .......... .......... .......... ..........  8% 12.0M 64s
 59550K .......... .......... .......... .......... ..........  8% 4.80M 64s
 59600K .......... .......... .......... .......... ..........  8% 84.9M 64s
 59650K .......... .......... .......... .......... ..........  8% 14.8M 64s
 59700K .......... .......... .......... .......... ..........  8% 8.33M 64s
 59750K .......... .......... .......... .......... ..........  8% 12.0M 64s
 59800K .......... .......... .......... .......... ..........  8% 11.4M 64s
 59850K .......... .......... .......... .......... ..........  8% 8.77M 64s
 59900K .......... .......... .......... .......... ..........  8% 2.94M 64s
 59950K .......... .......... .......... .......... ..........  8% 15.9M 64s
```

检查远程文件是否存在

```
wget --spider https://www.mingongge.com/backup/mysql_backup.tar.gz
[root@centos7 ~]# wget --spider https://www.mingongge.com/backup/mysql_backup.tar.gz
Spider mode enabled. Check if remote file exists.
--2021-03-10 09:30:41--  https://www.mingongge.com/backup/mysql_backup.tar.gz
Resolving www.mingongge.com (www.mingongge.com)... 104.164.133.141
Connecting to www.mingongge.com (www.mingongge.com)|104.164.133.141|:443... failed: Connection timed out.
Retrying.
```