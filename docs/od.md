## 功能简介

od（Octal Dump）命令用于将指定文件内容以八进制、十进制、十六进制、浮点格式或ASCII编码字符方式显示，通常用于显示或查看文件中不能直接显示在终端的字符。od命令系统默认的显示方式是八进制。

常见的文件为文本文件和二进制文件。od命令主要用来查看保存在二进制文件中的值，按照指定格式解释文件中的数据并输出，不管是IEEE754格式的浮点数还是ASCII码，od命令都能按照需求输出它们的值。

大家也可以了解一下hexdump命令，以十六进制输出，但感觉hexdump命令没有od命令强大。

## 命令格式

```
od [OPTION]... [FILE]...
```

## 选项说明

```
-A RADIX
  --address-radix=RADIX
 #选择以何种基数表示地址偏移
-j BYTES
  --skip-bytes=BYTES
 #跳过指定数目的字节
-N BYTES
  --read-bytes=BYTES
 #输出指定字节数
-S [BYTES]
  --strings[=BYTES]
 #输出长度不小于指定字节数的字符串，BYTES 缺省为 3
-v
  --output-duplicates
 #输出时不省略重复的数据
-w [BYTES]
  --width[=BYTES]
 #设置每行显示的字节数，BYTES 缺省为 32 字节
-t TYPE
  --format=TYPE
 #指定输出格式，格式包括 a、c、d、f、o、u 和 x，各含义如下：
  a：具名字符；比如换行符显示为 nl
  c：可打印字符或反斜杠表示的转义字符；比如换行符显示为 \n
  d[SIZE]：SIZE 字节组成一个有符号十进制整数。SIZE 缺省为 sizeof(int)
  f[SIZE]：SIZE 字节组成一个浮点数。SIZE 缺省为 sizeof(double)
  o[SIZE]：SIZE 字节组成一个八进制整数。SIZE 缺省为 sizeof(int)
  u[SIZE]：SIZE 字节组成一个无符号十进制整数。SIZE 缺省为 sizeof(int)
  x[SIZE]：SIZE 字节组成一个十六进制整数。SIZE 缺省为 sizeof(int)
  SIZE可以为数字，也可以为大写字母。如果 TYPE 是 [doux] 中的一个，那么SIZE 可以为C = sizeof(char)，S = sizeof(short)，I = sizeof(int)，L = sizeof(long)。如果 TYPE 是 f，那么 SIZE 可以为 F = sizeof(float)，D = sizeof(double) ，L = sizeof(long double)
--help
 #在线帮助
--version
 #显示版本信息
```

## 常用示例

1、设置第一列偏移地址以十进制显示。

```
od -Ad testfile
#偏移地址显示基数有：d for decimal, o for octal, x for hexadecimal or n for none。
```

2、od 不显示第一列偏移地址。

```
od -An testfile
```

3、以十六进制输出，默认以四字节为一组（一列）显示。

```
od -tx testfile
```

4、以十六进制输出，每列输出一字节。

```
od -tx1 testfile
```

5、显示ASCII字符和ASCII字符名称，注意换行符显示方式的区别。

```
#显示ASCII字符
[b3335@localhost]$ echo lvlv|od -a
0000000   l   v   l   v  nl
0000005

#显示ASCII字符名称
[b3335@localhost]$ echo lvlv|od -tc
0000000   l   v   l   v  \n
0000005
```

6、以十六进制显示的同时显示原字符。

```
[b3335@localhost]$ echo lvlv|od -tcx1
0000000   l   v   l   v  \n
         6c  76  6c  76  0a
0000005
```

7、指定每行显示512字节。

```
od -w512 -tx1 testfile
```

8、od 命令输出时去除列与列之间的空格符。

当我们需要将文件内容显示为十六进制，需要输出连续的单个字节，每个字节以十六进制显示。这时我们可以通过od命令将文件以单个字节为一组，十六进制输出在同一行，并去除每个字节之间的空格。目前还不知道怎么通过指定od命令的相关选项去除列与列之间的空格，也许od命令本身并不支持。我的做法是：

- （a）使用-An不输出偏移地址；
- （b）使用-v输出时不省略重复的数据；
- （c）使用-tx1以单个字节为一组按照十六进制输出，-w1每列输出一个字节；
- （d）最后通过管道传递给 awk 的标准输入，通过awk不换行输出所有行，拼接为一行输出。

具体命令如下：

```
od -An -w1 -tx1 testfile|awk '{for(i=1;i<=NF;++i){printf "%s",$i}}'
```