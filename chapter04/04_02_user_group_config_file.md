# 组配置文件

组配置文件也是包括一个组信息文件和一个组密码文件，分别是：/etc/group、/etc/gpasswd。它们也是有一定的编写格式的。

## /etc/group

其中/etc/group文件的格式如下：

`组名：组密码位：GID：组成员列表`

其中组成员如果有多个，则用英文逗号隔开

如：

`sys::3:root,bin,adm`

上面表示有一个组名为sys，GID为3的组，这个组有root,bin,adm三个用户。

## /etc/gshadow

/etc/gshadow文件的格式如下：

`组名：组密码：用户组管理员的账号：组成员列表`

```
test1:test1:chanshuyi:chanshuyi,chenyr
test1的组，组密码是test1，组成员有chanshuyi & chenyr，组的管理者是chanshuyi。
```

## 常用命令

### groupadd  添加用户组

```
groupadd {-g 888} webadmin //创建用户组webadmin，其GID为888
```

### groupdel  删除用户组

```
groupdel webadmin  //删除用户组webadmin
```

### groupmod  修改用户组信息

```
groupmod -n apache webadmin //修改webadmin组名为apache
设置组密码用“gpasswd [组名]”，然后根据提示输入密码。不要用“gapsswd -p [组名]”的方式。
```

### gpasswd 用户组管理命令

格式：gpasswd [参数] {用户名} [组名]

参数：

- -a 添加用户到用户组

- -d 从用户组中删除用户

- -A 设置用户组管理员

- -r 删除用户组密码

- -R 禁止用户切换为该组

范例：

```
gpasswd group1 //为group1设置密码
gpasswd –a tomgao group1  //将tomgao加到group1里
gpasswd –d tomgao group1  //将tomgao从group1里删除
gpasswd –A tomgao group1 //设置tomgao为管理员
gpasswd –r group1 //删除group1的组密码
gpasswd –R group1  //禁止用户切换为该组
```

### groups [用户名]  查看用户所隶属的组

```
groups samlee  查看samlee所属的用户组
```

### newgrp  切换用户组

格式：newgrp [组名]

```
newgrp sugroup //（当前用户）加入sugroup用户组，之后根据提示输入组密码
```

### grpck  用户组配置文件检测

### chgrp  修改文件所属组

### vigr  编辑/etc/group文件（锁定文件）