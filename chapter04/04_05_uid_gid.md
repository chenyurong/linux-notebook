# SetUID权限、SetGID权限、黏着位

## SetUID权限

SetUID权限，其实对应与二进制文件的S权限位，它表示其他凡是对此文件有执行权的用户执行时权限自动提升为所有者的权限。如：

-rwsr-xr-x  小写s表示具有SetUID权限，当为大写S时表示SetUID权限出现了错误。

SetUID权限 权限值=4 代号s

授予/撤消SetUID权限（用s表示）分别有两种方式：

chmod u+s  或 chmod 4755

chmod u-s  或  chmod 755

注：4所在的位表示特殊位，而4这个值是SetUID权限的权限值。

## SetGID权限

SetGID权限 权限值=2 代号g

授予/撤消SetGID权限（用s表示）分别有两种方式：

chmod g+s  或  chmod 2755 

chmod g-s  或   chmod 755

如果同时授予SetGID和SetUID则用：chmod 6755

## 黏着位

黏着位 权限值=1 代号t

黏着位（用t表示）只能针对权限为777的目录设置。（权限要为777，并且是目录！）。如果一个目录具有黏着位，那么表示每个用户都可以在这个目录下创建文件，但是只能删除自己创建的文件。

授予/撤消黏着位分别有两种方式：

chmod o+t 或 chmod 1777

chmod o-t  或 chmod 777