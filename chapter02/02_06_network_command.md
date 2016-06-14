# Linux网络命令

## write 命令

- 所在路径：/usr/bin/write
- 语法：write <用户名>
- 功能：向另外一个用户发信息，以Ctrl+D作为结束

```bash
$write samlee
```

## wall 命令

- 所在路径：/usr/bin/wall   （Write All -> WALL）
- 执行权限：All User
- 语法：wall [message] [文件名]
- 功能：向所有用户广播信息

```bash
wall Happy New Year!
```

## ping 命令

- 所在路径：/usr/bin/ping
- 执行权限：root
- 语法：ping [选项] IP地址
- 功能：测试网络连通性

```bash
ping 192.168.1.1
```

能ping通并不能说明网络就一定没问题，要注意观察延迟和丢包率，也就是上面命令中的：`time=0.045ms`和`0% packet loss`。如果网线不好或者网卡不好，那么很可能出现延迟和丢包率很高的情况，甚至可能出现无法ping通。

如果`ping 127.0.0.1`不能ping通，那么可能是本机的TCP协议没有安装。如果`ping 127.0.0.1`能通，但是ping自己的IP地址不能ping通，那么可能是本地的网络设置有问题。

**设置ping次数**

```bash
ping -t 4 192.168.1.1
```

**设置ping包大小**

```bash
ping -s 60000 192.168.1.1
```

NOTE：但是包最大为65507。

## ifconfig 命令

- 所在路径：/usr/sbin/ifconfig
- 执行权限：root
- 语法：ifconfig [选项] [网卡设备标识]
	- 选项 -a 显示所有网卡信息
- 功能：查看网络设置信息

```bash
ifconfig -a
```

eth0是实际网卡，lo是回环网卡。

**修改IP地址**

```bash
ifconfig eth0 192.168.9.6
```

通过命令行设置IP地址，在机器重启后会失效。

## shutdown 命令

- 路径：/usr/sbin/shutdown
- 执行权限：root
- 语法：shutdown
- 功能描述：关机

```bash
$shutdown //关机，但默认情况下会延迟一定时间再关机
$shutdown -h now //立即关机
```

## reboot 命令

- 路径：/usr/sbin/reboot
- 执行权限：root
- 语法：reboot
- 功能描述：重启

```bash
$reboot
```