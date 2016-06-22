# 用户缺省配置文件

用户缺省配置文件指的是/etc/login.defs和/etc/default/useradd文件。

它们指的是当我们使用useradd命令添加用户时，对用户的缺省设置（如密码强度、警告时间、最长有效时间等）。

其中/etc/login.defs文件可以定义警告时间、最长有效时间等信息。

而/etc/default/useradd文件可以设置home目录，使用的shell等。