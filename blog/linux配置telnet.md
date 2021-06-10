## 用telnet连接linux ##
telnet传输没有经过加密，是明文的，安全性不如SSH不建议使用  
提前关闭selinux和防火墙，配置好yum仓库
### 1.安装telnet-server xinetd  

```bash
[root@localhost ~]# yum install telnet-server xinetd        //telnet进程由xinetd服务守护
```
### 2.编辑telnet的配置文件

可能没有这个文件,但依旧起效
```bash
[root@localhost xinetd.d]# vi /etc/xinetd.d/telnet
```
添加以下内容
``` 
# default: on
# description: The telnet server serves telnet sessions; it uses \
#       unencrypted username/password pairs for authentication.
service telnet
{
        flags           = REUSE
        socket_type     = stream
        wait            = no
        user            = root
        server          = /usr/sbin/in.telnetd
        log_on_failure  += USERID
        disable         = no
}
```
### 3.启动xinetd服务  
```bash
[root@localhost xinetd.d]# systemctl start xinetd
```
### 4.编辑/etc/securetty  添加以下内容  

` pts/1 `  
pts/*为伪(虚拟)终端,保存，退出，可以用root用户登录  
