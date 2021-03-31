## 命令简介

文本查找或搜索工具。用于查找内容包含指定的范本样式的文件，如果发现某文件的内容符合所指定的范本样式，预设grep会把含有范本样式的那一列显示出来。若不指定任何文件名称，或是所给予的文件名为 -，则grep会从标准输入设备读取数据。

同样可以配合正则表达式来搜索文本，并将匹配的行打印输出,也可用于过滤与搜索特定字符串，使用十分灵活

## 常用参数

```
-a  #不要忽略二进制数据
-A  #除了显示符合范本样式的那一行之外，并显示该行之后的内容
-b  #在显示符合范本样式的那一行之外，并显示该行之前的内容
-B  #除了显示符合样式的那一行之外，并显示该行之前的内容
-c  #计算符合范本样式的列数
-C  #除了显示符合范本样式的那一列之外，并显示该列之前后的内容
-d  #当指定要查找的是目录而非文件时，必须使用这项参数，否则grep命令将回报信息并停止动作
-e  #指定字符串作为查找文件内容的范本样式
-E  #将范本样式为延伸的普通表示法来使用，意味着使用能使用扩展正则表达式
-f  #指定范本文件，其内容有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每一列的范本样式
-F  #将范本样式视为固定字符串的列表
-G  #将范本样式视为普通的表示法来使用
-h  #在显示符合范本样式的那一列之前，不标示该列所属的文件名称
-H  #在显示符合范本样式的那一列之前，标示该列的文件名称
-i  #忽略字符大小写的差别
-l  #列出文件内容符合指定的范本样式的文件名称
-L  #列出文件内容不符合指定的范本样式的文件名称
-n  #在显示符合范本样式的那一列之前，标示出该列的编号
-q  #不显示任何信息
-R/-r #此参数的效果和指定“-d recurse”参数相同
-s  #不显示错误信息
-v  #反转查找
-V  #显示版本信息 
-w  #只显示全字符合的列
-x  #只显示全列符合的列
-y  #此参数效果跟“-i”相同
-o  #只输出文件中匹配到的部分
```

## 正则表达式

```
^  #匹配以XX开头的行
$  #匹配以XX结尾的行
```

## 常用实例

1、在多个文件中查找：

```
grep "file" file_1 file_2 file_3
```

2、输出除之外的所有行 -v 选项：

```
grep -v "file" file_name
```

3、标记匹配颜色 --color=auto 选项：

```
grep "file" file_name --color=auto
```

4、使用正则表达式 -E 选项：

```
grep -E "[1-9]+"

egrep "[1-9]+"
```

5、只输出文件中匹配到的部分 -o 选项：

```
echo this is a test line. | grep -o -E "[a-z]+."
line.

echo this is a test line. | egrep -o "[a-z]+."
line.
```

6、统计文件或者文本中包含匹配字符串的行数-c 选项：

```
grep -c "text" file_name
2
```

7、输出包含匹配字符串的行数 -n 选项：

```
grep "text" -n file_name
或
cat file_name | grep "text" -n
```

8、多个文件

```
grep "text" -n file_1 file_2
```

9、搜索多个文件并查找匹配文本在哪些文件中：

```
grep -l "text" file1 file2 file3...
```

10、grep递归搜索文件

在多级目录中对文本进行递归搜索：

```
grep "text" . -r -n
```

11、忽略匹配样式中的字符大小写：

```
echo "hello world" | grep -i "HELLO"
hello
```

12、选项 -e 指定多个匹配样式：

```
echo this is a text line | grep -e "is" -e "line" -o
is
line
```

13、也可以使用 -f 选项来匹配多个样式，在样式文件中逐行写出需要匹配的字符。

```
cat patfile
aaa
bbb

echo aaa bbb ccc ddd eee | grep -f patfile -o
```

14、在grep搜索结果中包括或者排除指定文件：

只在目录中所有的.php和.html文件中递归搜索字符"main()"

```
grep "main()" . -r --include *.{php,html}
```

15、在搜索结果中排除所有README文件

```
grep "main()" . -r --exclude "README"
```

16、在搜索结果中排除filelist文件列表里的文件

```
grep "main()" . -r --exclude-from filelist
```

更多Linux命令请参考>>>值得收藏！[Linux系统常用命令速查手册](http://mp.weixin.qq.com/s?__biz=MzI0MDQ4MTM5NQ==&mid=2247500085&idx=2&sn=5455a50a3ec0fc0a69a7cc910a316ebe&chksm=e918a429de6f2d3f4ba700653b387459cb16dd4bf34cd42b4b0ef53c2dd91a53ce40abf0f2a2&scene=21#wechat_redirect)

```
grep "San" testfile 
#过滤有San的行

grep '^J' testfile 
#显示以J开头的行

grep '70$' testfile 
#显示以70结尾的行

grep -v "834" testfile 
#显示所有不包括834的行

grep ':12/' testfile 
#显示:12/的行 

grep ':498-' testfile 
#显示:498-的行

grep '[A-Z][a-z]{4}:[[:space:]][A-Z]' testfile 
#显示这样的行，一个大写字母+四个小写字母+空格+一个大写字母

grep '[a-z]{1,}[[:space:]][Kk]' testfile 
#显示包括K k的行

grep -n '[0-9]{6,}$' testfile 
#显示6位数字的行，并打印行号

grep -i "lincoln" testfile 
#显示有lincoln的行，不区分大小写
```