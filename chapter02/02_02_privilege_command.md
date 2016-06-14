# Linux权限处理命令

在Linux系统中通过chmod命令来改变文件或目录权限。而chmod命令有两种方式改变文件或文件夹的权限，一种是ugo方式，一种是421方式。

## ugo方式

对应的chmod语法格式是：chmod [{ugo} {+-=} {rwx}] [文件或目录]

- u 是所有者，g 是指所属组，o 是指其他人。
- + 是指增加权限，- 是指减少权限，= 是指赋予权限
- r 是指读权限，w 是指写权限、x 只是执行权限

**为文件的所有者增加写和执行权限**

chmod u+wx hello.txt

**为其他人减少读和执行权限**

chmod o-rx hello.txt　　

## 421方式

对应的chmod语法格式是： chmod [mode] [文件或目录]

- r的值是4，w的值是2，x的值是1。
- 这里写的mode，是指一组数字。如：421。这里的421，是指所有者所拥有权限的数字总和是4，所属组所拥有权限的总和是2，其他人所拥有权限的数字总和是1。这里421，对应的rwx就是：r---w---x。

**为所有者设置可读权限，为所属组设置写权限，为其他人设置可执行权限**

chmod 421 hello.txt

## 常用命令

**改变文件或目录的所有者**

chown user_tom hello.txt

**添加用户**

useradd user_hellen

**为用户设置密码**

passwd user_hellen

**更改文件或目录所属组**

chgrp group_root hello.txt

**查看新建文件或目录时的缺省权限**

```bash
[chanshuyi@localhost Desktop]$ umask
0002
```

输出为：0002，这里第一个0是特殊权限位。之后的”002“表示权限掩码值。上面改变文件或目录时的MODE（421 = r---w---x）是权限码，权限掩码值= 666 - 权限码。

当我们需要改变创建文件时的缺省权限时，可以使用：”umak [权限掩码值]“来赋予权限。

```bash
[chanshuyi@localhost Desktop]$ umask 027  --修改缺省权限
[chanshuyi@localhost Desktop]$ umask  --查看缺省权限
0027
[chanshuyi@localhost Desktop]$ touch test.txt  --创建文件
[chanshuyi@localhost Desktop]$ ls -ld test.txt  --文件的权限码为：640
-rw-r-----. 1 chanshuyi chanshuyi 0 Nov 16 07:32 test.txt
```

上面的命令修改了创建文件或文件夹的默认权限为：750，即所有者rwx权限，所属组r-x权限，其他人无权限。但是我们之后新建了一个文件，发现其文件的默认权限吗却为640，而不是我们希望的750。这是因为Linux中有一个默认的权限规则：**缺省创建的文件不能授予可执行权限，即x权限**。所以在计算文件的执行权限的时候，要用 666 - 权限掩码值，而不是用 777 - 权限掩码值。

