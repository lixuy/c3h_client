c3h-client
===========
该项目代码源于以下项目：

njit8021xclient:https://github.com/liuqun/njit8021xclient

以及bitdust的fork:https://github.com/bitdust/njit8021xclient

由于对njit8021xclient版本的结构和内容作出不少修改，因此决定从该项目分离并建立一个新项目

License
---------
本项目继承并遵循GPLv3协议，不欢迎任何用于商业却不公开源代码的行为(除非自行重写程序代码)

概述
-----
* 本项目基于njit8021xclient代码进行修改
* 基于iNode V7.00-0102版本的EAP报文分析进行修改
* 可运作于Linux/openWRT/Windows
* 集成MD5算法，不需要再依赖openssl
* 增加断线重连机制
* 测试环境为佛大
* 暂时未集成makefile，如有需要可修改使用njit8021xclient项目相关文件

依赖的开发包
--------
* Linux/openWRT: libpcap
* Windows: WinPcap(WpdPack)

测试日志
-----
2015.4.19：佛大校园网测试：目前可成功认证，但校园网在心跳报文加入了某种检测导致心跳报文阶段检测不通过。
在auth.c中SendResponseSecurity()函数中
```
response[i++] = 0x00;	// 上报是否使用代理
```
此行代码取消注释后，不会立即强制下线，但7分钟后仍会断开（服务器收不到正确报文而强制下线），重新连接不会被拉黑。
非佛大环境可尝试直接使用该客户端。

用法
-----
```
c3h-client  [username] [password] [adapter]
```
Linux/openWRT环境下可以不输入[adapter]参数，则默认设备为eth0
```
Usage:
c3h-client	[Username]	Your Username.
			[password]	Your Password.
			[adapter]	Specify ethernet adapter to use.
						Adapter in Linux is eth0,eth1...etc
						Adapter in Windows starts with '\Device\NPF_'
```

参考文献
---------
iNode协议逆向研究初步入门by tsy http://www.cnblogs.com/bitpeach/p/4092806.html