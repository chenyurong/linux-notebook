# APT包管理

APT包管理方式是Debian系Linux系列的二进制包管理方式。

其命令与arp包管理方式差不多，只不过是rpm前缀换成了apt-cache而已。

APT包管理方式的命令如下：

- apt-cache search   搜索软件包

- apt-cache show     软件包信息

- apt-get install   安装（-f 参数可以强制安装）

- apt-get reinstall 覆盖安装（-f 参数可以强制重新安装）

- apt-get remove 删除

- apt-get autoremove 自动删除（MARK  --purge）

- apt-get update 更新软件源

- apt-get upgrade 更新已安装包