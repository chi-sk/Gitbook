
## CentOS7关闭SELinux
 **查看**
 ```cpp
[root@dev-server ~]# getenforce
Disabled
[root@dev-server ~]# /usr/sbin/sestatus -v
SELinux status:                 disabled
 ```
 **临时关闭**
 ```cpp
##设置SELinux 成为permissive模式
##setenforce 1 设置SELinux 成为enforcing模式
setenforce 0
 ```
 **永久关闭**
 ```cpp
 vi /etc/selinux/config
 ```
 
 将SELINUX=enforcing改为SELINUX=disabled 
设置后需要重启才能生效


## CentOS7关闭防火墙
**关闭防火墙**
```cpp
systemctl stop firewalld.service #停止firewall
systemctl status firewalld.service #查看firewall的状态
systemctl disable firewalld.service #禁止firewall开机启动
```
**开启80端口**
```cpp
firewall-cmd --zone=public --add-port=80/tcp --permanent
```
**查询端口号80 是否开启**
```cpp
firewall-cmd --query-port=80/tcp
```
**重启防火墙**
```cpp
firewall-cmd --reload
```
**查询有哪些端口是开启的**
```cpp
 firewall-cmd --list-port
```
--zone #作用域
--add-port=80/tcp #添加端口，格式为：端口/通讯协议
--permanent #永久生效，没有此参数重启后失效

iptables防火墙的相关状态 
关闭虚拟机防火墙： 
关闭命令： service iptables stop 
永久关闭防火墙：chkconfig iptables off 
两个命令同时运行，运行完成后查看防火墙关闭状态 
service iptables status 
1 关闭防火墙—–service iptables stop 
2 启动防火墙—–service iptables start 
3 重启防火墙—–service iptables restart 
4 查看防火墙状态–service iptables status 
5 永久关闭防火墙–chkconfig iptables off 
6 永久关闭后启用–chkconfig iptables on
s