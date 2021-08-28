## 命令简介

useradd/userdel 创建新用户/删除用户，需要管理员权限操作。

在创建用户时，如果不配置密码，用户的默认密码是不可用的，所以，useradd命令一般与passwd命令配合使用，下节我们将介绍这个命令。

## 语法格式

```
useradd 选项 用户名
userdel 选项 用户名
```

**用户的分类**

- 超级用户：root，拥有对系统的最高管理权限，UID默认为0。
- 虚拟用户：又叫系统用户或伪用户，具有一定特权，与系统或程序服务相关，但没有真正的使用者。一般不会用来登录系统，它主要用于维持某个访问的正常运行，如ftp，apache等。
- 普通用户：是一种受限制的用户，一般新建的用户都是普通用户。默认只能执行/bin、/usr/bin、/usr/local/bin以及自身主目录里的命令。

注意：UID即每个用户的身份标识，虽然可以修改/etc/passwd（命令设置的UID不允许重复），但尽量保持唯一性，类似于每个人的身份证号码。

## 选项说明

useradd 选项

```
-c #加上备注文字，备注文字保存在passwd的备注栏中。
-d #指定用户登入时的主目录，替换系统默认值/home/<用户名>
-D #变更预设值。
-e #指定账号的失效日期，日期格式为MM/DD/YY，例如06/30/12。缺省表示永久有效。
-f #指定在密码过期后多少天即关闭该账号。如果为0账号立即被停用；如果为-1则账号一直可用。默认值为-1.
-g #指定用户所属的群组。值可以使组名也可以是GID。用户组必须已经存在的，期默认值为100，即users。
-G #指定用户所属的附加群组。
-m #自动建立用户的登入目录。
-M #不要自动建立用户的登入目录。
-n #取消建立以用户名称为名的群组。
-r #建立系统账号。
-s #指定用户登入后所使用的shell。默认值为/bin/bash。
-u #指定用户ID号。该值在系统中必须是唯一的。0~499默认是保留给系统用户账号使用的，所以该值必须大于499。
```

userdel 选项

```
-f #强制删除用户账号
-r #删除用户主目录及其中的任何文件
-h #显示命令的帮助信息
```

## 应用实例

```
useradd -s mingongge   
#新建系统用户mingongge

useradd mingongge -u 888    
#设定ID值时尽量要大于500，以免冲突;一般0到499之间的值留给bin、mail这样的系统账号

useradd -m -d /home/mingongge mingongge   
#指定创建用户家目录的路径，/home/mingongge目录会被创建

useradd -s /sbin/nologin mingongge     
#创建一个没有家目录且不能登录的用户

useradd -m -G test,sudo mingongge      
#创建时把用户加入不同的用户组test,sudo

useradd -u 2020 -m -g root mingongge       
#添加用户mingongge其id为2020，并且将其添加到组群root中
```

使用useradd -D可以查看创建新用户时的默认信息，或直接cat /etc/default/useradd

```
useradd -D
GROUP=888
HOME=/home
INACTIVE=888
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
CREATE_MAIL_SPOOL=yes
```

修改创建新用户时的默认信息。

```
useradd -D -f 999

#查看是否修改成功
useradd -D | grep INACTIVE
INACTIVE=999
```

删除用户，但不删除其家目录及文件

```
[root@mingongge ~]# userdel mingongge
```

删除用户，并将其家目录及文件一并删除

```
[root@mingongge ~]# userdel -r mingongge
```

强制删除用户

```
[root@mingongge ~]# userdel -f mingongge
```