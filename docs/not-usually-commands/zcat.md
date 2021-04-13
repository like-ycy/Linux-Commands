## 命令简介

zcat 命令用于显示压缩包中文件的内容，可以使用 gzip -d 或 gunzip 或 zcat 将压缩文件恢复为原始格式。zcat 与 gunzip -c 相同。

zcat 命令用于不真正解压缩文件，就能显示压缩包中文件的内容的场合。

## 语法格式

```
zcat [ -fhLV ] [ name ...  ]
```

## 选项说明

```
-S  #指定gzip格式的压缩包的后缀
-c  #将文件内容写到标注输出
-d  #执行解压缩操作
-l  #显示压缩包中文件的列表
-L  #显示软件许可信息
-q  #禁用警告信息
-r  #在目录上执行递归操作
-t  #测试压缩文件的完整性
-V  #显示指令的版本信息
-l  #更快的压缩速度
-9  #更高的压缩比
```

## 应用举例

打印压缩的内容，将内容传给more命令进行分页显示

```
[root@centos7 ~]# zcat httpd-2.4.46.tar.gz | more
```

![图片](https://mmbiz.qpic.cn/mmbiz_png/tuSaKc6SfPpfMiaEuTENjpKAwJicFV73zAE66Urow2RbGQzXMMtGodmjkSJx2WbMsuwkBA4Wc88GfIBH5ftUDHpQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

查看压缩属性信息

```
[root@centos7 ~]# zcat -l httpd-2.4.46.tar.gz
         compressed        uncompressed  ratio uncompressed_name
            9363314            42301440  77.9% httpd-2.4.46.tar
compressed          #压缩大小    
uncompressed        #未压缩大小
ratio               #压缩比率
uncompressed_name    #未压缩文件的名称
```

查看普通文件(类似于cat功能)

```
[root@centos7 ~]# zcat -f test.txt
This is a test line
This is a test line
This is a test line
This is also a test line
This is also a test line
This is also also a test line
```

其它实例

```
#测试压缩包的完整性
[root@centos7 ~]# zcat -t httpd-2.4.46.tar.gz

#显示软件许可信息
[root@centos7 ~]# zcat -L httpd-2.4.46.tar.gz
gzip 1.5
Copyright (C) 2007, 2010, 2011 Free Software Foundation, Inc.
Copyright (C) 1993 Jean-loup Gailly.
This is free software.  You may redistribute copies of it under the terms of
the GNU General Public License <http://www.gnu.org/licenses/gpl.html>.
There is NO WARRANTY, to the extent permitted by law.
```