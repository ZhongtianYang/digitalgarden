---
{"dg-publish":true,"permalink":"/class-notes/0919-virtual-box/","dgPassFrontmatter":true,"created":"2023-10-03T22:20:19.480+08:00"}
---

### windows的设置：

#### 1.共享网卡

打开控制面板>网络和 Internet>网络和共享中心>更改适配器设置，打开**以太网**属性（如果计算机使用的WLAN上网就打开WLAN）>共享，勾选**允许其他网络用户通过此计算机的Internet连接来连接（N）**，在家庭网络连接（H）里选择VirtualBox的网卡我这里叫**以太网2**，有的设备没有这一项也是正常的。

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE1-1-1024x581.png)

打开VirtualBox的网卡（以太网2）属性，双击Internet协议版本4（TCP/IPv），把IP地址`192.168.137.1`改为`192.168.1.1`，最后确定。

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE2-1-1024x546.png)

#### 2.启用回显请求（ping）

高级安全 Windows Defender 防火墙→入站规则→虚拟机监控（回显请求-ICMPv4-In）→启用

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE3-1024x654.png)

#### 3.打开ICS

Win+R”打开运行，键入：**server.msc**，打开服务，

定位到internet Connection Sharing(ICS)，启动类型（E）改为自动

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE5-1024x580.png)

由于Windows 10 网络连接共享功能重启后失效，进行以下设置

“Win+R”打开运行，键入：regedit，打开注册表编辑器，

定位到：HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\SharedAccess

在空白处右击鼠标，新建“DWORD（32位）值（D）”，

名称叫做“ EnableRebootPersistConnection ”，将数值数据改为1。

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE4-1024x705.png)

[Windows 10 网络连接共享功能重启后失效 - Microsoft Community](https://answers.microsoft.com/zh-hans/windows/forum/all/windows-10/b7b94ad6-890c-45df-8496-d552c1505098)

### VM VirtualBox的设置：

#### 1.工具→网卡→手动配置网卡 IPv4地址192.168.1.1

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE6-1024x600.png)

#### 2.关闭DHCP服务器

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE8-1024x600.png)

#### 3.虚拟机设置里网络连接方式改为 仅主机（Host-Only）网络

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE7-1024x640.png)

### kylinServer虚拟机里的设置：

启动虚拟机

删除VirBr0网卡，执行：

1.列出当前系统中的所有网络：

```
virsh net-list
```

2.取消定义（undefine）一个网络，在这里，“default”是网络的名称

```
virsh net-destroy default
```

3.停止（destroy）一个网络，在这里，“default”是网络的名称

```shell
virsh net-undefine default
```

配置虚拟机网卡：

```
nmtui
```

编辑连接

![](https://suniro.cn/wp-content/uploads/2023/10/%E7%BD%91%E7%BB%9C%E8%AE%BE%E7%BD%AE9-1024x771.png)