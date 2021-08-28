# chown

## 命令简介

chown命令用来变更文件或目录的拥有者或所属群组，通过chown改变文件的拥有者和群组。用户可以是用户名或者用户ID；组可以是组名或者组ID；文件是以空格分开的文件列表，文件名也支持通配符。

系统管理员经常使用chown命令，去改变一个文件或目录的所属。普通用户是不能将自己所属文件或目录变成其它的拥有者。

## 语法格式

```
chown [选项] [用户或组] [文件或目录]
```

- 用户：组：指定所有者和所属工作组。当省略“：组”，仅改变文件所有者；
- 文件：指定要改变所有者和工作组的文件列表。支持多个文件和目标，支持shell通配符。

Linux/Unix 文件目录所属分为三级 : 拥有者、群组、其他。

- root：系统特权用户类，既 UID = 0 的用户
- owner：所有者
- group：所属组
- other：其它人，不属于上面3类的所有其他用户

## 选项说明

```
-c或--changes           #效果类似“-v”参数，但仅回报更改的部分；
-f或--quite或—-silent    #不显示错误信息；
-h或--no-dereference    #只对符号连接的文件作修改，而不更改其他任何相关文件；
-R或--recursive         #递归处理，将指定目录下的所有文件及子目录一并处理；
-v或--version           #显示指令执行过程；
--dereference          #效果和“-h”参数相同；
--help                 #在线帮助
--reference=<参考文件或目录>   #把指定文件或目录的拥有者与所属群组全部设成和参考文件或目录的拥有者与所属群组相同；
--version    #显示版本信息。
```

## 应用实例

将目录/usr/app及其下面的所有文件、子目录的文件主改成mingongge

```
chown -R mingongge /usr/app
```

使用mingongge用户可以有权限访问文件test.txt

```
chown mingongge test.txt
```



# chmod

## 命令简介

chmod 命令用来变更文件或目录的权限。

文件或目录权限有读取、写入、执行这3种，另外还有3种特殊权限。用户可以使用chmod去设置文件与目录的权限，设置方式采用文字或数字皆可。链接文件的权限无法直接变更，如果用户需要对链接文件修改权限，其真实作用是作用在原始文件上。

## 语法格式

```
chmod  [选项]   [权限] [文件或目录]
chmod [OPTION] [MODE]  FILE
chmod [OPTION] [MODE]  DIRECETORY
```

## 选项说明

```
u  #用户user，文件或目录的所有者。
g  #用户组group，文件或目录所属组
o  #其它用户others
a  #所有用户all，系统默认
+  #添加权限
-  #取消权限
=  #配置文件的权限为指定的权限
r  #可读权限
w  #可写权限
x  #可执行权限
-  #没有权限
x  #设置可执行权限
s  #设置suid和sgid，可以使用“u+s”，“g+s”的方式来设置
t  #只有目录或文件的所有者才可以删除目录下的文件
-c    #效果类似“-v”参数
-f    #操作过程中不显示任何错误信息；
-R    #递归处理，将指定目录下的所有文件及子目录一并处理；
-v或——verbose    #显示命令运行时的详细执行过程；
--reference=<参考文件或目录> #把指定文件或目录的所属组权限设成参考文件或目录的所属组一样；
<权限范围>+<权限设置> #开启权限范围的文件或目录的该选项权限设置；
<权限范围>-<权限设置> #关闭权限范围的文件或目录的该选项权限设置；
<权限范围>=<权限设置> #指定权限范围的文件或目录的该选项权限设置；
--help     #显示帮助信息
--version  #显示版本信息
```

## 权限说明

```
 -rw-r--r--   1 mingongge  mingongge   651 Oct 12 12:53 test.txt
# ↑╰┬╯╰┬╯╰┬╯
# ┆ ┆  ┆  ╰┈ 0 其他人
# ┆ ┆  ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈ g 属组
# ┆ ╰┈┈┈┈ u 属组
# ╰┈┈ 第一个字母是文件类型   

#d代表的是目录(directroy)
#-代表的是文件(regular file)
#s代表的是套字文件(socket)
#p代表的管道文件(pipe)或命名管道文件(named pipe)
#l代表的是符号链接文件(symbolic link)
#b代表的是该文件是面向块的设备文件(block-oriented device file)
#c代表的是该文件是面向字符的设备文件(charcter-oriented device file)

r=读取属性 ＝4
w=写入属性 ＝2
x=执行属性 ＝1
```

## 特殊权限说明

Linux系统除了正常的读写操作权限外，还有Linux特殊权限。包括SET位权限（suid，sgid）和粘滞位权限（sticky）。

```
chmod u+s filename  #设置suid位
chmod u-s filename  #去掉suid设置
chmod g+s filename  #设置sgid位
chmod g-s filename  #去掉sgid设置
chmod +t  filename  #设置粘滞位权限
chmod -t  filename  #去掉粘滞位权限
```

如果一个文件被设置了suid或sgid，在其所有者或所属组权限的可执行位上有明显的标记，如果文件设置了suid且也设置了x（执行）权限，则在其执行权限位上会显示一个字母s(小写)。但是，如果没有设置x权限，则显示为字母S(大写)。如下：

```
-rwsr-xr-x #设置了suid，且文件所有者也配置了可执行权限
-rwSr--r-- #设置了suid，但文件所有者没有配置可执行权限
-rwxr-sr-x #设置了guid，且所属组也配置了可执行权限
-rw-r-Sr-- #设置了guid，但所属组没有配置可执行权限
```

一个文件或目录如果被设置了粘滞位权限，会在其他人权限的可执行位上有标记。如果文件设置了sticky还设置了x（执行）位，其他人权限的可执行位显示一个字母t(小写)。但是，如果没有设置x位，则显示一个字母T(大写)。如下：

```
-rwsr-xr-t #表示设置了粘滞位且其他人用户也配置了可执行权限
-rwSr--r-T #表示设置了粘滞位但其他人用户没有配置可执行权限
```

## 应用实例

```
$ chmod u+x file      
#给file的属主增加执行权限

$ chmod 751 mingongge     
#给mingongge的属主分配读、写、执行权限

$ chmod u=rwx,g=rx,o=x mingongge      
#给mingongge属主分配读写执行权限，属组分配读执行权限，其它人分配执行权限

$ chmod =r mingongge    
$ chmod 444 mingongge   
#为mingongge的所有者、所属组、其他人分配读权限
                
$ chmod -R u+r mingongge           
#递归地给mingongge录下所有文件和子目录的属主分配读的权限

$ chmod 4755 mingongge                           
#设置用户ID，给属主分配读、写和执行权限，给所属组和其他用户分配读、执行的权限。
```