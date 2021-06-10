注：本次安装参照B站up主“bili逍遥bili”，采用glibc包安装。
所需工具：Redhat Linux（虚拟机），MobaXterm（终端工具），MySQL-5.6.44-1.el7.x86_64.rpm-bundle.tar（官网下载）。
[下载地址](https://cdn.mysql.com/archives/mysql-5.6/mysql-5.6.44-linux-glibc2.12-x86_64.tar.gz)
## 开始安装
 一.**配置本地yum仓库**，由于我的linux最小化安装，在安装过程中需要另外安装某些依赖包  
1.创建文件 `[root@linuxprobe ~]# mkdir -p /media/cdrom`  
2.挂载`[root@linuxprobe ~]# mount /dev/cdrom /media/cdrom`  
3.配置yum仓库`[root@linuxprobe ~]# vim /etc/yum.repos.d/rhel7.repo`  
4.编辑配置文件`[root@linuxprobe ~]# vim /etc/yum.repos.d/rhel7.repo`  

```bash
[rhel7]
name=rhel7
baseurl=file:///media/cdrom
enabled=1
gpgcheck=0
```
二、移动和解压
把安装好的安装包上传到Linux的root目录下，进行解压

```bash
[root@localhost~]#tar -zxf mysql-5.6.44-linux-glibc2.12-x86_64.tar.gz
[root@localhost ~]# mv mysql-5.6.44-linux-glibc2.12-x86_64 /usr/local/mysql
```
ls查看当前目录下的文件

```bash
[root@localhost ~]# ls
anaconda-ks.cfg  mysql-5.6.44-linux-glibc2.12-x86_64.tar.gz

```

三、创建用户和更改权限

```bash
[root@localhost ~]# useradd -r -s /sbin/nologin mysql
[root@localhost ~]# chown -R mysql.mysql /usr/local/mysql
```
四、安装依赖包

```bash
[root@localhost ~]# yum install  perl perl-devel
[root@localhost ~]# yum install libaio*
[root@localhost ~]# yum install autoconf
```
五、卸载自带的数据库

```bash
[root@localhost mysql]# yum remove mariadb-libs
```
六、运行脚本（在/use/local/mysql的目录下）

```bash
[root@localhostmysql]# /usr/local/mysql/scripts/mysql_install_db --user=mysql
```
七、复制mysql.service文件

```bash
[root@localhost mysql]# cp support-files/mysql.server /etc/init.d/mysql
```
八、启动mysql

```bash
[root@localhost ~]# service mysql start
```
九、设置密码

```bash
[root@localhost mysql]# ./bin/mysqladmin -u root password '123456'
```
十、创建软连接

```bash
[root@localhost bin]# ln -s /usr/local/mysql/bin/mysql /usr/bin
```
输入mysql -u root -p 即可打开MySQL
