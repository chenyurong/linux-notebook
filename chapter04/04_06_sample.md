# 案例

## 典型案例之一：手动创建一个用户

我们除了可以通过useradd添加一个用户之外，我们也可以通过修改配置文件的方式手动添加一个用户。只要按下面的顺序我们就可以手动添加一个用户zhangsan：

- 1、修改/etc/passwd、/etc/shadow文件

```
//在/etc/passwd配置
zhangsan:x:556:556:zhangsan:/home/zhangsan:/bin/bash
//在/etc/shadow配置
zhangsan::16406:0:99999:7:::
MARK 这里少了关键的一步
```

- 2、创建宿主目录

```
//创建宿主目录/home/zhangsan
mkdir /home/zhangsan
```

- 3、拷贝/etc/skel下的配置文件到宿主目录/home/samlee（用户名）下

## 典型案例之二：批量添加用户

下面以批量添加10个用户为例。（MARK 补充一个完整的实例）

- 1、用newusers命令 - 导入用户信息文件

创建user.txt文件，内容如下：

```
cs1:x:0:0:marketing dept:/home/cs1:/bin/bash
cs2:x:0:0:marketing dept:/home/cs2:/bin/bash
```

执行以下命令，导入用户信息文件：

```
[root@localhost ~]# newusers /home/chanshuyi/Desktop/user.txt
```

- 2、pwunconv命令 - 取消shadow password功能

```
[root@localhost ~]# pwunconv
```

- 3、chpasswd命令 - 导入密码文件（格式->用户名：密码）

创建passwd文件，并输入以下内容：

```
cs1:cs1
cs2:cs2
```

执行密码文件导入的命令：

```
[root@localhost ~]# chpasswd /home/chanshuyi/Desktop/passwd.txt
```

- 4、pwconv命令 - 将密码写入shadow文件

```
[root@localhost ~]# pwconv
```

## 典型案例之三：限制用户使用su

限制用户使用su的本质是改变su命令的可执行位，对所有具有使用su命令的用户授予x权限。

- 1、创建sugroup组并改变su命令的权限

```
#groupadd sugroup
#chmod 4550 /bin/su  //限制只有创建者和所属组具有x权限（可执行权限，4表示SetUID权限）
SetUID权限可以让执行者执行此文件时以文件所有者的身份执行。
```

- 2、改变/bin/su所属组为sugroup

```
#chgrp sugroup /bin/su
设定之后，只有sugroup中的用户可以使用su切换为root。
```

## 典型案例之四：root权限的开放——sudo

Sudo是一个软件，它可以让普通用户以root身份执行命令，并且可以精细化到命令的参数。

Sudo的配置文件是：/etc/sudoers，要编译Sudo的配置文件用命令：visudo，用一般的vi命令是不能编译的。

而我们编辑sodoers文件也要按照一定的格式，/etc/sudoers文件的格式为：用户名（组名） 主机地址=命令（绝对路径）

比如我要让hellen具有添加用户的权限，那我用visudo编辑配置文件并加入下面的配置：

```
chenyr localhost=/usr/sbin/useradd  //有多个命令要赋予时，用英文逗号隔开
```

这样当我用chenyr登录的时候，我可以用“sudo [命令]”的格式去添加用户，如：

```
sudo useradd testuser
sudo passwd testuser
```

这样就可以成功添加testuser用户了。

此外，你可以用“sudo -l 命令”查看看当前用户被授予了哪些命令的root执行权限。如上面的chenyr账号，你可以看到它被授予执行的命令有useradd：

```
[chenyr@localhost ~]$ sudo -l
//.....
User chenyr may run the following commands on this host:
    (root) /usr/sbin/useradd
```

另外，sudo可以精细化地进行命令的授权，如：

```
hellen localhost=/sbin/shutdown -h now       
//只允许用户执行sudo shutdown -h now命令，少一个参数都不行。
```

## John the Ripper 密码强度检测软件