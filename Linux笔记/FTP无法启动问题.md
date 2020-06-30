环境：    centos7

yum install vsftpd 之后显示安装成功
    然后systemctl start vsftpd报错
```cpp
[root@localhost ~]# systemctl start vsftpd
Job for vsftpd.service failed because the control process exited with error code. See "systemctl status vsftpd.service" and "journalctl -xe" for details.
```

按照提示查看 systemctl status vsftpd

```cpp
[root@localhost ~]# systemctl status vsftpd
● vsftpd.service - Vsftpd ftp daemon
   Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; disabled; vendor preset: disabled)
   Active: failed (Result: exit-code) since 一 2019-12-30 23:12:04 CST; 2min 25s ago
  Process: 2979 ExecStart=/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf (code=exited, status=1/FAILURE)

12月 30 23:12:01 localhost.localdomain systemd[1]: Starting Vsftpd ftp daemon...
12月 30 23:12:04 localhost.localdomain systemd[1]: vsftpd.service: control process exited, code=exited status=1
12月 30 23:12:04 localhost.localdomain systemd[1]: Failed to start Vsftpd ftp daemon.
12月 30 23:12:04 localhost.localdomain systemd[1]: Unit vsftpd.service entered failed state.
12月 30 23:12:04 localhost.localdomain systemd[1]: vsftpd.service failed.
```
解决： 首先查看端口是否被占用：

```cpp
[root@localhost ~]# lsof -i:21
COMMAND    PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
pure-ftpd 1867 root    4u  IPv4  23140      0t0  TCP *:ftp (LISTEN)
pure-ftpd 1867 root    5u  IPv6  23141      0t0  TCP *:ftp (LISTEN)
```

再接下来查看配置文件 IPv4 ipv6 不能同时listen. 再启动

```cpp
[root@localhost ~]# kill -9 1867
[root@localhost ~]# lsof -i:21
[root@localhost ~]# systemctl start vsftpd
[root@localhost ~]#         //无任何提示，表示启动成功
```
此时再启动ftp，没有任何信息返回，表示启动成功

```cpp
[root@localhost ~]# systemctl status vsftpd
● vsftpd.service - Vsftpd ftp daemon
   Loaded: loaded (/usr/lib/systemd/system/vsftpd.service; disabled; vendor preset: disabled)
   Active: active (running) since 一 2019-12-30 23:17:21 CST; 9h ago
  Process: 3250 ExecStart=/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf (code=exited, status=0/SUCCESS)
 Main PID: 3251 (vsftpd)
   CGroup: /system.slice/vsftpd.service
           └─3251 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf

12月 30 23:17:21 localhost.localdomain systemd[1]: Starting Vsftpd ftp daemon...
12月 30 23:17:21 localhost.localdomain systemd[1]: Started Vsftpd ftp daemon.
[root@localhost ~]#
```

## ftp Linux：530 Permission denied问题解决
使用filezilla连接,输入IP地址，root用户，密码，快速连接，报错：
530 Permission denied。
###故障排除：
**1. 检查系统是否开启了vsftp服务**
首先检查系统是否开启了vsftp服务，如果没有开启，先开启该服务。
  方法1.setup--系统服务--自启动服务
  方法2.界面设置，service vsftpd restart
**2. 查看配置**
vsftpd的配置，配置文件中限定了vsftpd用户连接控制配置。
vsftpd.ftpusers：位于/etc目录下。它指定了哪些用户账户不能访问FTP服务器，例如root等。
vsftpd.user_list：位于/etc目录下。该文件里的用户账户在默认情况下也不能访问FTP服务器，仅当vsftpd .conf配置文件里启用userlist_enable=NO选项时才允许访问。
vsftpd.conf：位于/etc/vsftpd目录下。来自定义用户登录控制、用户权限控制、超时设置、服务器功能选项、服务器性能选项、服务器响应消息等FTP服务器的配置。
**3. 重启服务**
配置修改完成后，执行service vsftpd restart重启vsftpd服务。


## Filezilla连接阿里云服务器遇到的问题
**第一个问题**：服务器发回了不可路由的地址。被动模式失败
- 解决方法：点击客户端左上角文件>站点管理器>新建站点，在右边 输入主机ip、账号密码，然后点击上面的选项卡“传输设置”,传输模式设置为主动。
点击链接。

**第二个问题**：错误: 20 秒后无活动，连接超时 错误: 读取目录列表失败
点击客户端左上角文件>站点管理器

- 解决方法：打开报错的连接站点，将加密方式选择为 “只是用普通FTP（不安全）”模式即可。

**第三个问题**：服务器发回了不可路由的地址。使用服务器地址代替。
- 解决方法：更改Filezilla设置，编辑-设置-连接-FTP-被动模式，将“使用服务器的外部ip地址来代替”改为“回到主动模式”即可。