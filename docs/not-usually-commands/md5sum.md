## 命令简介

md5sum 用于计算和校验文件的MD5值。

md5sum 常常被用来验证网络文件传输的完整性，防止文件被人篡改。在日常工作当中，我们可以用来监控系统中的重要文件是否被篡改。

还可以使用使用 md5sum 生成文件或用户的密码。

## 语法格式

```
md5sum [选项] [文件]
```

## 选项说明

```
-b #使用二进制模式对文件进行读取
-t #把输入的文件看作是文本文件
-c #从指定文件中读取MD5校验值，并进行校验
--status  #校验成功时不输出任何信息
-w  #当校验不正确时输出警告信息
```

## 应用举例

生成密码或随机数值

```
[root@centos7 ~]# date | md5sum
1b1f0ba711e7d4931c23fbbd2b328e40  -
```

检查一个文件的 md5 值

```
[root@centos7 testdir]# md5sum mingongge1.txt
c5cab5a45a72380ce456a4370bf40348  mingongge1.txt
```

检查一个文件是否被更改

```
#提取文件原md5值
[root@centos7 testdir]# md5sum mingongge1.txt >./mingongge.txt.md5
[root@centos7 testdir]# cat mingongge.txt.md5
c5cab5a45a72380ce456a4370bf40348  mingongge1.txt

#写入内容
[root@centos7 testdir]# cat >> mingongge1.txt << EOF
> 1
> 2
> 3
> 4
> EOF
[root@centos7 testdir]# md5sum mingongge1.txt -c mingongge.txt.md5
mingongge1.txt: FAILED
md5sum: WARNING: 1 computed checksum did NOT match
```