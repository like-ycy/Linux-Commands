## 命令简介

less 命令分页上下翻页浏览文件内容。

less 命令与 more 命令相似，都可以用来查看文件内容，不同的是 less 命令可以向前或向后查看文件，而 more 命令只能向前查看。

用 less 命令显示文件时，按 PageUp 键向上翻页，按PageDown 键向下翻页，按 Q 键退出查看。

## 命令格式

```
less [选项] [文件名]
less [option] [file ...]
```

## 选项说明

```
-e  #文件内容显示完成后，自动退出
-f  #强制显示文件
-g  #不加亮显示
-l  #忽略大小写
-N  #行首显示行号
-s  #合并多个空行只显示一行
-S  #不换行显示内容
-x<数字>   #将TAB字符显示为指定个数的空格字符
```

## 应用举例

```
#分页显示mingongge.log文件内容
less /var/log/mingongge.log

#显示文件mingongge的内容，并在每行行首加上行号
less -N mingongge.txt

#下/上一页：
<Space> (down), b (up)

#less 命令转到文件的末尾/开始：
G (end), g (start)

#向前查找字符串（按 n N 跳转到下一个/上一个）
/mingongge
#向后查找字符串（按 n N 跳转到下一个/上一个）
?mingongge

#退出 less 命令
q
```

常用的用法基本就这些，与more命令一样，都属于比较常用且简单的命令。