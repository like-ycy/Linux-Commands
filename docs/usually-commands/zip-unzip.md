# zip

## 命令简介

zip 命令可以用来压缩、打包文件。

```
#Debian/Ubuntu安装
apt-get install zip

#CentOS安装
[root@centos7 testdir]# zip
-bash: zip: command not found
[root@centos7 testdir]# yum install zip -y
```

zip 命令也可以用来解压缩文件，zip也是一个常用的压缩、解压应用程序，文件经它压缩后会产生一个新以.zip为扩展名的压缩包文件。

## 语法格式

```
zip [ OPTIONS ] [ NAME ..]
```

## 选项说明

```
-A  #调整可执行的自动解压缩文件
-b<工作目录>  #指定压缩文件的存放目录
-c  #给每个被压缩的文件加上注释信息
-d  #从压缩文件内删除指定的文件，也可以使用--delete参数
-D  #压缩文件内不建立目录名称
-f  #更新既有文件，将其它文件一并加入到压缩文件中
-F  #修复已损坏的压缩文件
-g  #将指定文件压缩至已存在的压缩文件中，不建立新文件
-h  #打印帮助信息
-i<范本样式>  #只压缩匹配指定条件的文件
-m  #将指定文件压缩打包后直接删除原始文件
-o  #将压缩文件的属性信息更改成与压缩文件中的最新文件的属性一致
-q  #安静模式
-r  #递归处理
-t<日期时间>  #把压缩文件的日期设成指定的日期
-T  #检查备份文件内的每个文件是否正确无误
-u  #更新较新的文件到压缩文件内
-v  #打印命令执行过程信息或版本信息
-x<范本样式>  #压缩时排除符合条件的文件
-z  #给压缩文件加上注释信息
-<压缩效率>  #指定压缩效率（1~9数字）
```

## 应用举例

在当前目录下创建压缩文件（自动创建以.zip的文件）

```
[root@centos7 testdir]# zip mingongge *
  adding: cest.txt.gz (stored 0%)
  adding: cuttest.txt.gz (stored 0%)
  adding: dir/ (stored 0%)
  adding: file (stored 0%)
  adding: mingongge1.txt.gz (stored 0%)
  adding: mingongge2.txt.gz (stored 0%)
  adding: mingongge.txt.md5.gz (stored 0%)
  adding: sort.cut.txt.gz (stored 0%)
```

分割一个大文件

```
[root@centos7 ~]# ls -lh
total 22M
-rw-------.  1 root root 1.3K Aug 20 10:39 anaconda-ks.cfg
-rw-r--r--   1 root root  140 Jan 16 11:36 dos_test.txt
drwxr-xr-x   3 root root   39 Aug 30 03:48 goinception
-rw-r--r--   1 root root  13M Aug 30 03:42 goInception-linux-amd64-v1.2.3.tar.gz
drwxr-sr-x  11 root   40 4.0K Dec 24 22:35 httpd-2.4.46
-rw-r--r--   1 root root 9.0M Aug  5 07:32 httpd-2.4.46.tar.gz
-rw-r--r--   1 root root    0 Jan 16 11:32 mingongge.file
drwxr-xr-x   3 root root  192 Jan 16 16:19 testdir
-rw-r--r--   1 root root  140 Jan 16 11:32 test.txt
[root@centos7 ~]# zip -s 4M -r mingongge.zip httpd-2.4.46.tar.gz
  adding: httpd-2.4.46.tar.gz (deflated 0%)
[root@centos7 ~]# ls -lh
total 31M
-rw-------.  1 root root 1.3K Aug 20 10:39 anaconda-ks.cfg
-rw-r--r--   1 root root  140 Jan 16 11:36 dos_test.txt
drwxr-xr-x   3 root root   39 Aug 30 03:48 goinception
-rw-r--r--   1 root root  13M Aug 30 03:42 goInception-linux-amd64-v1.2.3.tar.gz
drwxr-sr-x  11 root   40 4.0K Dec 24 22:35 httpd-2.4.46
-rw-r--r--   1 root root 9.0M Aug  5 07:32 httpd-2.4.46.tar.gz
-rw-r--r--   1 root root    0 Jan 16 11:32 mingongge.file
-rw-r--r--   1 root root 4.0M Jan 16 16:24 mingongge.z01
-rw-r--r--   1 root root 4.0M Jan 16 16:24 mingongge.z02
-rw-r--r--   1 root root 943K Jan 16 16:24 mingongge.zip
drwxr-xr-x   3 root root  192 Jan 16 16:19 testdir
#从结果可以看出会拆分成三个文件即：4M大小的mingongge.z01、4M大小的mingongge.z02和一个943k的mingongge.zip文件。
```



# unzip

## 命令简介

unzip 命令用于解压由zip命令压缩的压缩包文件。

```
#Debian/Ubuntu安装
apt-get install unzip

#CentOS安装
[root@centos7 ~]# unzip 
-bash: unzip: command not found
[root@centos7 ~]# yum install unzip -y
```

## 语法格式

```
unzip [ OPTIONS ] file[.zip] [file(s) ...]
```

## 选项说明

```
-c  #将解压缩的结果输出，并对字符做适当的转换
-f  #更新现有的文件
-l  #列出压缩文件内所包含的文件
-p  #将解压缩的结果显示到屏幕上，但不执行任何的转换
-t  #检查压缩文件是否正确；
-u  #除了更新现有的文件外，也会将压缩文件中的其他文件解压缩到目录中
-v  #显示详细的信息
-z  #仅显示压缩文件的备注信息
-a  #对文本文件进行必要的字符转换
-b  #不对文本文件进行字符转换
-C  #压缩文件名称区分大小写
-j  #不处理压缩文件中原有的目录路径
-L  #将压缩文件中的全部文件名改为小写
-M  #将输出结果再交给more程序处理
-n  #解压缩时不覆盖原有的文件
-o  #unzip执行后覆盖原有的文件，不提示
-P<密码>  #使用zip的密码选项
-q  #不显示任何命令执行过程信息
-s  #将文件名中的空白字符转换为底线字符
-d<目录>  #将解压缩后存至指定的目录下
-x<文件>  #指定不要处理.zip压缩文件中的哪些文件
-Z  #unzip-Z相当于执行zipinfo命令
```

## 应用举例

解压一个文件

```
[root@centos7 testdir]# unzip mingongge.zip
```

查看一个压缩文件但不解压

```
[root@centos7 testdir]# unzip -v mingongge.zip 
Archive:  mingongge.zip
 Length   Method    Size  Cmpr    Date    Time   CRC-32   Name
--------  ------  ------- ---- ---------- ----- --------  ----
      59  Stored       59   0% 01-16-2021 12:15 b32621da  cest.txt.gz
      57  Stored       57   0% 01-16-2021 12:12 cbda1ce8  cuttest.txt.gz
       0  Stored        0   0% 01-16-2021 16:18 00000000  dir/
       0  Stored        0   0% 01-16-2021 16:18 00000000  file
      81  Stored       81   0% 01-16-2021 09:55 da9f2476  mingongge1.txt.gz
      51  Stored       51   0% 01-16-2021 03:36 8fdf382e  mingongge2.txt.gz
      87  Stored       87   0% 01-16-2021 09:59 982ab7bb  mingongge.txt.md5.gz
      65  Stored       65   0% 01-16-2021 10:19 17350869  sort.cut.txt.gz
--------          -------  ---                            -------
     400              400   0%                            8 files
```

指定解压后的文件存放目录

```
[root@centos7 testdir]# unzip -n mingongge.zip -d /tmp/
Archive:  mingongge.zip
 extracting: /tmp/cest.txt.gz        
 extracting: /tmp/cuttest.txt.gz     
   creating: /tmp/dir/
 extracting: /tmp/file               
 extracting: /tmp/mingongge1.txt.gz  
 extracting: /tmp/mingongge2.txt.gz  
 extracting: /tmp/mingongge.txt.md5.gz  
 extracting: /tmp/sort.cut.txt.gz    
[root@centos7 testdir]# ll /tmp/
total 24
-rw-r--r-- 1 root root 59 Jan 16 12:15 cest.txt.gz
-rw-r--r-- 1 root root 57 Jan 16 12:12 cuttest.txt.gz
drwxr-xr-x 2 root root  6 Jan 16 16:18 dir
-rw-r--r-- 1 root root  0 Jan 16 16:18 file
-rw-r--r-- 1 root root 81 Jan 16 09:55 mingongge1.txt.gz
-rw-r--r-- 1 root root 51 Jan 16 03:36 mingongge2.txt.gz
-rw-r--r-- 1 root root 87 Jan 16 09:59 mingongge.txt.md5.gz
-rw-r--r-- 1 root root 65 Jan 16 10:19 sort.cut.txt.gz
```