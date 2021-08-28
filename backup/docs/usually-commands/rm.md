## 命令简介

rm 命令用来删除指定的文件或目录，此命令是一个危险的命令，操作前一定要再三确认是否正确，然后再执行操作步骤。

默认情况，它是不能直接删除目录的，需要配合选项来删除。当使用 -r 或 -R 选项来执行 rm 时，它会递归删除任何匹配到的目录，且它们的子目录以及子目录下包含的所有文件。

如需要针对文件扩展名字符匹配来删除多个文件时，rm 命令需要使用 -i 选项来配合完成。使用这个选项时，系统会逐一提示你是否要删除文件，当你输入y并按Enter键，文件就会被删除，反之，则文件不会被删除。

## 语法格式

```
rm [选项] 文件或目录
mv [options] FILE DIRECTORY
```

## 选项说明

```
-d：#把要删除的目录的硬连接数量变成0，删除该目录
-f：#强制删除文件或目录
-i：#删除之前提示用户是否删除
-r或-R：#递归处理
--preserve-root：#不对根目录进行递归操作；
-v：#显示指令的详细执行过程。
```

## 应用举例

删除文件test.txt和文件test1.txt前进行确认是否删除，删除命令如下

```
[root@test ~]# rm -i test.txt test1.txt 
rm: remove regular file ‘test.txt’? y
rm: remove regular file ‘test1.txt’? y
#输入y确认删除
```

删除/test目录下所有目录，并删除前不进行确认。删除命令如下。

```
[root@test ~]# rm -rf /test/
[root@test ~]# ls /test
ls: cannot access /test: No such file or directory
```