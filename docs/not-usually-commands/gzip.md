## 命令简介

gzip 命令用来压缩文件，gzip，gunzip命令用于压缩或扩展 GNU GZIP 格式的文件。

如果压缩文件名对其文件系统而言太长，则gzip会将其截断。默认情况下，gzip 会将原始文件名和时间戳等信息保留在新产生的压缩文件中。

## 语法格式

```
gzip [ OPTIONS ]  [ name ]
gunzip [ OPTIONS ] [ name ]
```

## 选项说明

```
-a  #使用ASCII文字模式
-c  #将输出写入到标准输出，保持原始文件不变。
-d  #解压缩文件
-f  #强制压缩文件
-h  #显示在线帮助信息
-l  #列出压缩文件的相关信息
-L  #显示版本与版权信息
-n  #压缩文件时，不保留原来的文件名称及时间戳等属性信息
-N  #压缩文件时，保留原来的文件名称及时间戳属性信息
-q  #不显示警告信息
-r  #递归处理，将指定目录下的所有文件及子目录一并处理
-t  #测试压缩文件是否正确无误
-v  #显示命令执行过程信息
-V  #显示版本信息
-<压缩效率>  #压缩效率是一个介于1~9的数值，默认值为“6”，指定的值越高，压缩率就越高
```

## 应用举例

把当前目录所有的文件压缩成.gz包

```
[root@centos7 testdir]# gzip *
[root@centos7 testdir]# ll
total 24
-rw-r--r-- 1 root root 59 Jan 16 12:15 cest.txt.gz
-rw-r--r-- 1 root root 57 Jan 16 12:12 cuttest.txt.gz
-rw-r--r-- 1 root root 81 Jan 16 09:55 mingongge1.txt.gz
-rw-r--r-- 1 root root 51 Jan 16 03:36 mingongge2.txt.gz
-rw-r--r-- 1 root root 87 Jan 16 09:59 mingongge.txt.md5.gz
-rw-r--r-- 1 root root 65 Jan 16 10:19 sort.cut.txt.gz
```

把当前目录的每个压缩的文件解压，并列出详细的信息

```
[root@centos7 testdir]# gzip -dv *
cest.txt.gz:  77.8% -- replaced with cest.txt
cuttest.txt.gz:  73.5% -- replaced with cuttest.txt
mingongge1.txt.gz:  61.3% -- replaced with mingongge1.txt
mingongge2.txt.gz:  25.0% -- replaced with mingongge2.txt
mingongge.txt.md5.gz:  -4.1% -- replaced with mingongge.txt.md5
sort.cut.txt.gz:  19.0% -- replaced with sort.cut.txt
[root@centos7 testdir]# ll
total 24
-rw-r--r-- 1 root root 144 Jan 16 12:15 cest.txt
-rw-r--r-- 1 root root 102 Jan 16 12:12 cuttest.txt
-rw-r--r-- 1 root root 124 Jan 16 09:55 mingongge1.txt
-rw-r--r-- 1 root root  24 Jan 16 03:36 mingongge2.txt
-rw-r--r-- 1 root root  49 Jan 16 09:59 mingongge.txt.md5
-rw-r--r-- 1 root root  42 Jan 16 10:19 sort.cut.txt
```

详细显当前目录每个压缩的文件的信息，但不将文件解压出来

```
[root@centos7 testdir]# gzip -l *
         compressed        uncompressed  ratio uncompressed_name
                 59                 144  77.8% cest.txt
                 57                 102  73.5% cuttest.txt
                 81                 124  61.3% mingongge1.txt
                 51                  24  25.0% mingongge2.txt
                 87                  49  -4.1% mingongge.txt.md5
                 65                  42  19.0% sort.cut.txt
                400                 485  23.9% (totals)
```

和tar命令的常用用法基本一样，都属于文件压缩与解压命令。