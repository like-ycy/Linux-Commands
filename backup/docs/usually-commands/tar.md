## 命令简介

tar 命令用于打包、压缩与解压压缩包文件。

tar 命令常常用于打包、压缩某些文件或目录，也可以添加新文件到归档文件中。Tar 代表的是磁带存档，是一种归档的文件格式，早期用于将文件归档到磁带备份存储。现可以用于收集、分发、归档文件，还可以保留文件原有的属性，如：用户和组权限，访问和修改日期以及目录结构。

## 语法格式

```
tar [OPTIONS] [FILE]
```

## 选项说明

```
-A  #新增文件到已经存在的归档文件
-B  #设置区块大小
-c  #建立新的归档文件
-C  #将压缩的文件解压到指定的目录下
-d  #记录文件的差异
-x  #解压或提取归档文件内容              
-t  #列出备份文件的内容
-z  #通过gzip命令来压缩/解压缩文件，文件名一般为 xx.tar.gz
-Z  #通过compress命令处理备份文件
-f  #指定备份文件
-v  #显示命令执行过程
-r  #添加新文件到已经压缩的文件中
-u  #添加改变了和现有的文件到已经存在的压缩文件
-j  #通过bzip2命令来压缩/解压缩文件，文件名一般为xx.tar.bz2
-v  #显示操作过程；
-k  #保留原有文件不覆盖
-m  #保留文件不被覆盖
-w  #确认压缩文件的正确性
-p  #保留原来的文件权限与属性
-P  #使用文件名的绝对路径，不删除文件名称前的“/”号
-N  #只将较指定日期更新的文件保存到备份文件中
--exclude=[范本样式]  #排除符合范本样式的文件
--remove-files       #归档/压缩之后删除源文件
```

## 应用举例

常见应用例子

```
tar -cf mingongge.tar *.jpg
#将所有.jpg的文件打包成一个名为mingongge.tar的文件
 
tar -rf mingongge.tar *.gif
#将所有.gif的文件增加到mingongge.tar的包里
 
tar -uf mingonggel.tar mingongge.gif
#更新mingongge.tar文件中的mingongge.gif文件
 
tar -tf mingongge.tar
#列出 all.tar 包中所有文件

tar -cfv mingongge.tar foo bar  
#将文件foo和bar打包成mingongge.tar文件包，也可以理解成：从这两个文件中去创建这个mingongge.tar文件

tar -tvf mingongge.tar         
#详细列出mingongge.tar中的所有文件

tar -xf mingongge.tar          
#从mingongge.tar提取所有文件
```

将文件全部打包成tar包

```
tar -cvf mingongg.tar mingongg.log       #仅打包，不压缩！
tar -zcvf mingongg.tar.gz mingongg.log   #打包后，以gzip方式压缩
tar -jcvf mingongg.tar.bz2 mingongg.log  #打包后，以bzip2方式压缩
```

解压目录

```
tar -xvf portal-web-v2.0.0.tar --strip-components 1  -C 指定目录
#排除目录--strip-components
```

将 tar包解压缩

```
tar -zxvf /opt/soft/test/log.tar.gz
```

打包或压缩文件时，排队指定的文件类型

```
tar -zcf mingongge.tar.gz /etc/ /var/ --exclude=*.txt
```

**注意**：如果在使用过程中遇到这类错误提示

```
tar: Removing leading `/’ from member names 
```

原因是tar默认为相对路径，使用绝对路径的话就回报这个错，可以使用-P（大写）参数解决这个问题。