# 用户配置文件

用户配置文件主要包括两个文件，分别是：/etc/passwd和/etc/shadow。其中/etc/passwd存放的是用户的信息，/etc/shadow存放的是用户的密码信息。这两个文件的文件内容都是按照一定的格式编写的。

## /etc/passwd文件

/etc/passwd文件格式如下：

`用户名：密码位：UID：GID：描述信息：宿主目录：使用的shell命令`

例如：

`zhangsan:x:0:0:marketing dept:/home/zhangsan:shell`

## /etc/shadow文件

其中/etc/shadow文件的格式如下：

`用户名：加密密码：最后一次修改时间：最小时间间隔：最大时间间隔：警告时间：帐号闲置时间：失效时间：标志`

- 最后一次修改时间：是指最后一次修改密码的天数与1970年1月1日相隔的天数

- 最小时间间隔：指两次修改密码之间的最小天数（当为0时表示不限制）。

- 最大时间间隔：是指密码多少天之后失效，但是可以在重新密码使账户可以重新启用。而失效时间是指多久之后账户就直接无效（当不限制无效时间时，直接设置一个很大的值即可。）

- 警告时间：当密码失效前n天就进行提示警告（当为0时表示不警告）

- 帐号闲置时间：指用户没有登录活动但账号仍能保持有效的最大天数（不设置则留空）

- 失效时间：指多久之后账户就直接无效。一般应用于短期外来人员的帐号。

- 标志：一般不使用

如下面这个例子的最后一位和倒数第二位是空的：

`chanshuyi:$1$L79I629.$xBlLNY7I6Y7ok7no2JT6S.:16277:0:99999:7:0::`

## 常用命令

### useradd 添加用户命令

当我们要添加一个用户的时候，我们可以使用useradd命令设置用户的信息。

格式：useradd [参数] [用户名]

参数：

- -u  指定用户的UID（超级用户UID=0，普通用户UID 500-60000，伪用户UID 1-499） 

- -g  指定用户缺省所属的用户组的GID 

- -G  指定用户组所属多个组（用英文逗号隔开）

- -d  指定宿主目录

- -s  指定命令解释器Shell

- -c  指定描述信息

- -e  指定用户失效时间

范例：

```
#useradd -u 1888 -g webadmin -G sys,root -d /backup -s /bin/hash -e "Market WangWu" -e 2011-01-15 wangwu;
//属于sys/root/weadmin组，默认属于webadmin组。到2011年1月15日过期
```

添加一个用户hellen的例子：

```
useradd hellen //添加用户hellen
passwd hellen  //为hellen设置密码（之后输入密码即可）
```

注：你可以通过“useradd -d” 查看useradd命令时的缺省参数。

## usermod 用户信息修改命令

格式：usermod [参数] [用户名]

参数：

- -l 修改登录名 （所有useradd的参数都可以作为usermod的参数）

范例：

```
usermod -l samlee -d /home/samlee liming    //将用户liming的登录名改为samlee，用户目录改为/home/samlee
usermod -G softgroup samlee       //将用户samlee添加到softgroup用户组中
```

## userdel  删除用户 

格式：userdel [参数] [用户名]

参数：

- -r  删除用户的同时删除用户目录

## chage  用户管理命令

NOTE：chage只能在Linux中使用，在Unix无法使用

格式：chage [参数] [用户名]

参数：

- -l  查看用户密码设置（如：密码失效时间、最后一次修改密码时间等）

- -m 密码修改最小天数

- -M  密码修改最大天数

- -d  密码最后修改的日期

- -I  密码过期后，锁定账户的天数

- -E 设置密码的过期日期，如果为0，代码密码立即过期；如果为-1，代表密码永不过期

- -W 设置密码过期前，开始警告的天数

例如：

```
#chage -m 1 test2  //修改test2密码修改最小天数为1
#chage -E 2014/12/20 test2  //设置test2用户2014年12月20日过期
```

## 禁用账户和恢复账户

禁用：usermod -L username 或 passwd -l username

回复：usermod -U username 或 passwd -u username

加上参数-f可以强制解锁。

## 停用或启用shadow功能

pwconv/pwunconv   停用用户的shadow功能

grpconv/grpunconv   停用用户组的shadow功能

pwck 检测/etc/passwd文件是否有错误

pwck命令会检测/etc/passwd以及/tec/shadow两个文件是否出错

## vipw 编辑/etc/passwd文件（锁定文件）

## finger [用户名]    查看用户的详细信息

## su - [用户名]     切换用户

加横杠表示切换环境变量。不加横杆则环境变量不会改变。

## who/w  查看当前登录用户信息

Who与w的区别就是w命令会显示比who更加详细的信息。
