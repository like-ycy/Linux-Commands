## 命令简介

mv 命令用于移动并重命名文件和目录。或者将文件从一个目录移动到另一个目录中，如果将一个文件移动到一个已经存在的目标文件中，这时目标文件的内容会被此文件内容覆盖。

如果源为文件，而目标为目录，mv 将进行文件的位置移动。如果源为目录，则目标只能是目录（不能为文件），mv 将进行目录的重命令名。

mv 命令移动文件时，在目标不同的情况下，会有下面4种不同的结果：

- 如果目标是指定的某一个具体路径，则源文件会被移动到此目录下，且文件名不变。
- 如果目标不是目录，则源文件名（只能有一个）会变为此目标文件名，如果存在同名文件，则会覆盖己存在的同名文件。
- 如果源文件和目标文件在同一个目录下，mv 的作用就是修改文件名。
- 当目标是目录时，源文件或目录可以是多个，这时所有的源文件都会被移至目标目录下。且所有的文件都将保留以前的文件名。

## 语法格式

```
mv [选项] 源文件或目录 目标文件或目录
mv [options] source destination
```

## 选项说明

```
-b   #当文件存在时，覆盖前，为其创建一个备份
-f   #如果移到的文件或目录与目标重复，则直接覆盖
-i   #交互式操作，覆盖前会提示用户进行确认操作，用户通过输入Y/N来确认是否覆盖
-u   #若目标文件已存在，且与需移动的文件同名，只有在源文件比目标文件较新时，才会更新目标文件
-t   #指定mv的目标目录，此选项使用于移动多个文件到一个目录的情况，此时目标文件在前，源文件在后。
-S<后缀>：#为备份文件指定后缀，而不使用默认的后缀（删除源文件中的斜杠“/”）
-n  #不覆盖任何现有文件
-T  #将目标当作普通文件，而不是目录
-v  #详细输出命令的执行过程
```

## 应用举例

```
#移动文件到目标目录
[root@centos7 testdir]# ll
total 0
-rw-r--r-- 1 root root 0 Feb 25  2021 filetest
-rw-r--r-- 1 root root 0 Feb 25  2021 testfile
[root@centos7 ~]# mv mingongge.txt testdir/
[root@centos7 ~]# ll testdir/
total 0
-rw-r--r-- 1 root root 0 Feb 25  2021 filetest
-rw-r--r-- 1 root root 0 Jan  2 08:43 mingongge.txt
-rw-r--r-- 1 root root 0 Feb 25  2021 testfile

#移动并重命令文件
[root@centos7 testdir]# mv mingongge.txt test/mingongge
[root@centos7 testdir]# ll test/
total 0
-rw-r--r-- 1 root root 0 Jan  2 08:50 mingongge
```

如果目标位置有同名文件，我们不希望它被覆盖，可以加上-n选项。

```
[root@centos7 testdir]# ll *.txt dir/*.txt
-rw-r--r-- 1 root root 0 Jan  2 08:58 dir/test1.txt
-rw-r--r-- 1 root root 0 Jan  2 08:58 dir/test2.txt
-rw-r--r-- 1 root root 0 Jan  2 09:03 test1.txt
-rw-r--r-- 1 root root 0 Jan  2 08:57 test2.txt
-rw-r--r-- 1 root root 0 Jan  2 09:03 test3.txt
[root@centos7 testdir]# mv -nv *.txt dir/
‘test3.txt’ -> ‘dir/test3.txt’    
#目标目录中没有test3.txt文件，所以移动成功
[root@centos7 testdir]# ll
total 0
drwxr-xr-x 2 root root 57 Jan  2 09:04 dir
-rw-r--r-- 1 root root  0 Jan  2 09:03 test1.txt
-rw-r--r-- 1 root root  0 Jan  2 08:57 test2.txt
```

备份功能

```
#如果test2.txt存在，它将会被重命令为test2.txt,原来的文件会被备份
[root@centos7 dir]# cat test1.txt 
1
[root@centos7 dir]# cat test2.txt 
2
[root@centos7 dir]# mv -b test1.txt test2.txt
mv: overwrite ‘test2.txt’? y
[root@centos7 dir]# ll
total 12
-rw-r--r-- 1 root root 2 Jan  2 09:12 test2.txt
-rw-r--r-- 1 root root 2 Jan  2 09:12 test2.txt~
-rw-r--r-- 1 root root 2 Jan  2 09:12 test3.txt
[root@centos7 dir]# cat test2.txt
1
[root@centos7 dir]# cat test2.txt~
2
#如果test3.txt存在，它将会被重命令为test3.txt.bak
[root@centos7 dir]# mv -b --suffix=.bak test2.txt test3.txt
mv: overwrite ‘test3.txt’? y
[root@centos7 dir]# ll
total 12
-rw-r--r-- 1 root root 2 Jan  2 09:12 test2.txt~
-rw-r--r-- 1 root root 2 Jan  2 09:12 test3.txt
-rw-r--r-- 1 root root 2 Jan  2 09:12 test3.txt.bak
[root@centos7 dir]# cat test3.txt
1
[root@centos7 dir]# cat test3.txt.bak 
3
```