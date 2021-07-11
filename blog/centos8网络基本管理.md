# centos8网络基本管理
**简介：** centos8没有传统的network.service，centos8采用NetworkManager.service服务管理网络。NM能管理各种网络：有线网卡、无线网卡 ， 动态ip、静态ip，以太网、非以太网，物理网卡、虚拟网卡。
**基本知识：** nmcli使用方法非常类似linux ip命令、cisco交换机命令，并且支持tab补全（详见本文最后的示例），也可在命令最后通过-h、--help、help查看帮助。
```bash
nmcli connection		译作连接，可理解为配置文件，相当于ifcfg-ensXX。可以简写为nmcli c。
nmcli device			译作设备，可理解为实际存在的网卡（包括物理网卡和虚拟网卡）。
```
## 场景一：修改已经存在的网络配置
```bash
1.编辑网卡配置文件
[root@localhost ~]# vim /etc/sysconfig/network-scripts/ifcfg-ens33
2.交互式修改
[root@localhost ~]# nmcli connection edit <网卡名称>
3.图形化界面修改
[root@localhost ~]# nmtui
```
## 场景二：添加新的网卡，并配置网络
`nmcli c add type ethernet con-name ens37 ifname ens37 ipv4.addr 192.168.1.200/24 ipv4.gateway 192.168.1.254 ipv4.method manual
`  

**重启网卡命令**

`nmcli device reapply <网卡名称>`