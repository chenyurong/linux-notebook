# 二进制包管理（基于rpm包管理工具）

rpm、yum是RedHat系列Linux下最常用的二进制包管理工具。yum与rpm的不同之处在于，yum可以解决安装二进制包时的依赖问题以及软件的升级问题。

## 卸载

格式：rpm -e [参数] [软件名]

范例：#rpm -e sudo  卸载名为sudo的软件

注：“--nodeps” 参数可以强行卸载该软件，而不检查其他软件与它的依赖关系。

## 安装

格式：rpm [参数] [软件文件名]

参数：

- -i 表示安装（必须）  
- -v 表示显示安装的详细信息（可选）  
- -h 显示安装进度（可选）

范例：

`#rpm -ivh sudo-1.7.2p1-5.e15.i386.rpm`

此外，还有其他参数可选：

**--excludedocs 不安装软件包中的文档文件**

范例：#rpm -ivh --excludedocs sudo-1.7.2p1-5.e15.i386.rpm 

**--prefix path 将软件包安装到path指定的路径下**

范例：#rpm -ivh --prefix=/usr/local/sudo sudo-1.7.2p1-5.e15.i386.rpm 将sudo软件安装到/usr/local/sudo目录下

**--test 只对安装进行测试，并不实际安装**

范例：#rpm -ivh --test sudo-1.7.2p1-5.e15.i386.rpm 测试安装sudo软件

**--replacepkgs 当软件包已被安装时，覆盖安装该软件包**

范例：#rpm -ivh --replacepkgs sudo-1.7.2p1-5.e15.i386.rpm 覆盖安装sudo软件

**--replacefiles**

要安装的软件包中有一个文件已在安装其它软件包时安装，会出现文件冲突错误，使用这个参数可以让rpm忽略该错误

范例：#rpm -ivh --replacefiles sudo-1.7.2p1-5.e15.i386.rpm 忽略文件冲突错误

**--nodeps 忽略未解决的依赖关系**

范例：#rpm -ivh --nodeps sudo-1.7.2p1-5.e15.i386.rpm

## 查询是否安装了某个软件

格式：rpm -q [软件名称]

范例：rpm -q sudo 查询是否安装了sudo这个软件

## 查询素有已安装的软件包

格式：rpm -qa  （a 表示 all）

范例：rpm -qa 

可以与grep连用，查询所有已安装软件中有某个关键字的软件，如：

rpm -qa | grep samba 查询已安装的所有软件包中有关键字samba的。

## 升级软件包

范例：#rpm -Uvh sudo-1.7.2p1-5.e15.i386.rpm

其中-U表示升级软件包（必须的参数）  -v 表示显示安装的详细信息（可选）  -h 显示安装进度（可选）

## rpm包查询

选项：-a 查询所有已安装的软件包

　　   -f 查询文件所属软件包

　　　-p 查询软件包

　　   -i 显示软件包信息

 　　  -l 显示软件包中的文件列表

　　   -d 显示被批注为文档的文件列表

　　   -c 显示被批注为配置文件的文件列表

**常用组合**

```
rpm -qf  查询文件隶书的软件包(father)

rpm -qi 或 rpm -qip  查询软件包信息（该软件包未安装。查询未安装软件的信息要加上p参数，下同）(info)

rpm -ql 或 rpm -qlp  查询软件包安装文件(list)

rpm -qd 或 rpm -qdp 查询软件包帮助文档(document)

rpm -qc 或 rpm -qcp 查询软件包配置文件(config)
```

范例：

```
#rpm -qf /etc/services 查询services文件隶书的软件包

#rpm -qi samba 查询samba软件包的信息

#rpm -ql sudo 查询sudo软件包安装了多少文件

#rpm -qd vsftpd 查询vsftpd软件帮助文档的位置

#rpm -qc sudo 查询sudo软件配置文件的位置
```

## 软件包校验

格式：rpm -V [软件名称]

范例：#rpm -V sudo 查询sudo软件的安装文件是否被更改过

输出：S.5......T c /etc/sudoers

输出字符串的含义如下：

5  文件的md5校验值（内容改变）

S  文件大小     L  链接文件     T 文件的创建或修改时间

D 设备文件     U 文件的用户   G 文件的用户组     M 文件的权限

上面范例的输出字符串表示：文件大小被改变，文件内容也被改变，并且文件的创建或修改时间被改变。

## 软件包文件提取

范例：解压所有文件到当前目录

`#rpm2cpio initscripts-8.45.30-2.e15.centos.i386.rpm | cpio -idv`

解压指定文件到当前目录下的etc/inittab目录下

`#rpm2cpio initscripts-8.45.30-2.e15.centos.i386.rpm | cpio -idv ./etc/inittab`

其中 v 表示显示详细信息，d 表示解压缩时保留目录结构，i 表示解压缩