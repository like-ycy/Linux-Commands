## 命令简介

ls(list)，ls命令显示指定目录下的内容，列出指定目录下所含的文件及子目录。此命令与Windows系统中dir命令功能相似。

ls命令的输出信息可以进行彩色加亮显示，以分区不同类型的文件。

## 语法格式

```
ls（选项）（参数）
```

## 选项说明

```
-a #显示指定目录下的所有文件以及子目录，包含隐藏文件
-A #显示指定目录下的（除“.”和“..”之外）所有文件及子目录
-d #显示指定目录的属性信息
-l #显示指定目录下的文件及子目录详细信息,输出的信息从左到右依次包括文件名，文件类型、权限模式、硬连接数、所有者、组、文件大小和文件的最后修改时间等
-r #倒序显示指定目录下的文件及子目录
-t #以时间顺序显示指定目录下的文件及子目录
-F  #在列出的文件名称后加一符号；例如可执行档则加 "*", 目录则加 "/"
-k：#以KB（千字节）为单位显示文件大小
-m：#用“,”号区隔每个文件和目录的名称
-n：#以用户识别码和群组识别码替代其名称
-s：#显示文件和目录的大小，以区块为单位
-L：#如果遇到性质为符号链接的文件或目录，直接列出该链接所指向的原始文件或目录
-R：#递归处理，将指定目录下的所有文件及子目录一并处理
```

## 应用实例

1、以下命令列出/root目录下文件及子目录。

```
[root@test ~]# ls -l /root/
total 4
-rw-------. 1 root root 1330 Mar 26 09:50 anaconda-ks.cfg
drwxr-xr-x  2 root root    6 Apr 24 01:59 test
drwxr-xr-x  2 root root    6 Apr 24 01:59 tools
```

2、以下命令以时间顺序倒序显示/root目录下的文件及子目录，并显示其详细信息。

```
[root@test ~]# ls -lrt /root/
total 4
-rw-------. 1 root root 1330 Mar 26 09:50 anaconda-ks.cfg
drwxr-xr-x  2 root root    6 Apr 24 01:59 test
drwxr-xr-x  2 root root    6 Apr 24 01:59 tools
```

3、显示文件索引节点号（inode）。一个索引节点代表一个文件；

```
[root@ ~]# ls -i *
134435243 1.sh  134318146 anaconda-ks.cfg
```

4、列出当前工作目录下所有档案及目录；目录于名称后加'/'，可执行档于名称后加'*'

```
ls -AF
```

5、计算当前目录下的文件数和目录数

```
ls -l * |grep "^-" |wc -l
ls -l * |grep  "^d" |wc -l
```

6、在ls中列出文件的绝对路径

```
#ls |sed "s:^:`pwd`/:"
/root/scripts/1.c
/root/scripts/2.c
/root/scripts/3.c
/root/scripts/a b.txt
/root/scripts/b.pdf
/root/scripts/cecho.sh
/root/scripts/echo.sh
```