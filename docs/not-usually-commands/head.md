## 命令简介

head 显示文件内容的头部。在系统默认情况下，head 命令只显示文件的头10 行内容。

## 命令格式

```
head [选项] [文件名]
head [OPTION] [FILE]
```

## 选项说明

```
-n<数字>  #按指定行数显示（从文件开头位置计算）
-c<字符数>  #按指定的字符数显示（从文件的第一个字符开始计算）
-v  #显示文件名信息
-q  #不显示文件名信息
--help     #打印帮助信息后退出
--version  #打印版本信息后退出
```

## 应用举例

```
#显示文件mingongge.txt前150行内容(如果没有其它参数，可以不需要-n)
head -150 mingongge.txt 

#显示文件mingongge1.txt 和mingongge2.txt的前100行内容
head -100 mingongge1.txt mingongge2.txt
 
[root@centos7 testdir]# head -100 mingongge1.txt mingongge2.txt
==> mingongge1.txt <==
11111111111111111111
22222222222222222222222
33333333333333333333333333
444444444444444444444444
....

==> mingongge2.txt <==
head1
head2
head3
head4
....
#注意：默认情况，一次显示多个文件的话，默认是显示文件名信息的，可以不加-v参数。
[root@centos7 testdir]# head -q -n 3 mingongge1.txt mingongge2.txt
11111111111111111111
22222222222222222222222
33333333333333333333333333
head1
head2
head3
```

常用的用法基本就这些，与more\less命令一样，都属于比较常用且简单的命令。