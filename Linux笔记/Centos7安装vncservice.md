**安装vnc服务**
```cpp
yum -y install tigervnc tigervnc-server  
# tigervnc包替代了vnc包，有些文章建议同时安装vnc，其实是不需要的  
```
**vnc服务配置——宿主机远程控制**
vncserver的配置，创建一个新的配置文件，以开启1号窗口为例（也可以同时开启多个窗口，修改数字即可），方法如下(命名必须按下列格式)：
```cpp
cp /lib/systemd/system/vncserver@.service /lib/systemd/system/vncserver@:1.service
```
如果需要再增加一个窗口(序号依次增加)：
```cpp
cp /lib/systemd/system/vncserver@.service /lib/systemd/system/ncserver@:2.service
```
**编辑/lib/systemd/system/vncserver@:1.service,设置用户root相关参数,最终内容如下**
```cpp
[Unit]
Description=Remote desktop service (VNC)
After=syslog.target network.target
[Service]
Type=forking
# Clean any existing files in /tmp/.X11-unix environment
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/sbin/runuser -l root -c "/usr/bin/vncserver %i"
PIDFile=/root/.vnc/%H%i.pid
ExecStop=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
```
**防火墙设置**
- 查看防火墙状态：
```cpp
firewall-cmd --state
```
- 关闭防火墙
```cpp
systemctl stop firewalld
systemctl disable firewalld
```
- 或者开启防火墙添加5901端口（这里只开启一个端口，如有多个界面可以开启多个端口）：
```cpp
systemctl start firewalld
firewall-cmd --permanent --zone=public --add-port=5901/tcp
```
**开启VNC**
- 更新systemctl以使其生效；
```cpp
systemctl daemon-reload 
```
- 设置vncserver的密码；
```cpp
 vncpasswd root
 //按提示输入密码以及确认密码
```
- 启动该服务用来启用vnc的1号窗口；
```cpp
systemctl start vncserver@:1.service  或者 vncserver :1
```
- 关闭1号窗口：
```cpp
systemctl stop vncserver@:1.service   或者 vncserver -kill :1
```
- 设置为开机自动启动；
```cpp
systemctl enable vncserver@:1.service
```
**systemctl启动异常解决**
- 启动vncsercer出现下面异常：
```cpp
[root@anbot]# systemctl start vncserver@:1.service
Job for vncserver@:1.service failed because the control process exited with error code.
 See "systemctl status vncserver@:1.service" and "journalctl -xe" for details.
 
[root@anbot]# systemctl status vncserver@:1.service
● vncserver@:1.service - Remote desktop service (VNC)
   Loaded: loaded (/usr/lib/systemd/system/vncserver@:1.service; enabled; vendor preset:
 disabled)
   Active: failed (Result: exit-code) since Fri 2018-07-27 19:46:46 CST; 1min 55s ago
  Process: 5655 ExecStart=/sbin/runuser -l oracle -c /usr/bin/vncserver %i -geometry 
1280x720 (code=exited, status=1/FAILURE)
  Process: 5650 ExecStartPre=/bin/sh -c /usr/bin/vncserver -kill %i > /dev/null 2>&1 
|| : (code=exited, status=0/SUCCESS)
 
1月 07 22:58:08 wyx.pc.com systemd[1]: Starting Remote desktop service (VNC)...
1月 07 22:58:08 wyx.pc.com runuser[5655]: runuser: user oracle does not exist
1月 07 22:58:08 wyx.pc.com systemd[1]: vncserver@:1.service: control process...=1
1月 07 22:58:08 wyx.pc.com systemd[1]: Failed to start Remote desktop servic...).
1月 07 22:58:08 wyx.pc.com systemd[1]: Unit vncserver@:1.service entered fai...e.
1月 07 22:58:08 wyx.pc.com systemd[1]: vncserver@:1.service failed.
```
- 报错已经有进程存在，可以通过以下命令查看到:
```cpp
[root@anbot]# netstat -antulp | grep 5901
tcp        0      0 0.0.0.0:5901            0.0.0.0:*               LISTEN      5008/Xvnc           
tcp6       0      0 :::5901                 :::*                    LISTEN      5008/Xvnc           
[root@anbot]# ps -ef | grep vnc
root      5008     1  0 19:45 pts/0    00:00:00 /usr/bin/Xvnc :1 -auth /root/.Xauthority -
desktop wyx.pc.com:1 (root) -fp catalogue:/etc/X11/fontpath.d -geometry 1024x768 -pn 
-rfbauth /root/.vnc/passwd -rfbport 5901 -rfbwait 30000
root      5678  1640  0 19:48 pts/0    00:00:00 grep --color=auto vnc
```
可以看到，存在vnc进程监听5901端口，此时我们已经可以通过vnc viewer客户端来连接使用服务器，服务启动失败是因为其配    置默认启动第一个用户界面也就是5901(5900+1)端口

  设置我们可以在/usr/bin/vncserver看到$vncPort = 5900 + $displayNumber，这里也可以通过修改5900来更改默认的端口设置
  此时，$displayNumber=1
```cpp
关闭服务：
vncserver -kill :1
启动服务
vncserver ：n  （端口号=5900+n）
 
启动时可以同时启动过个进程来分配给不同用户，n不同即可
vncserver ：1
vncserver ：2
vncserver ：3
 
netstat -antulp | grep 59
tcp        0      0 0.0.0.0:5901            0.0.0.0:*               LISTEN      6510/Xvnc           
tcp        0      0 0.0.0.0:5902            0.0.0.0:*               LISTEN      11064/Xvnc          
tcp        0      0 0.0.0.0:5903            0.0.0.0:*               LISTEN      12457/Xvnc          
tcp        0      0 192.168.0.103:5901      125.71.203.215:65313    ESTABLISHED 6510/Xvnc           
tcp6       0      0 :::5901                 :::*                    LISTEN      6510/Xvnc           
tcp6       0      0 :::5902                 :::*                    LISTEN      11064/Xvnc          
tcp6       0      0 :::5903                 :::*                    LISTEN      12457/Xvnc

```
如果我们要使用刚才配置的服务来管理，需要杀死存在的进程
```cpp
杀掉已经启动的进程
pkill -9 vnc
 
清空配置缓存（删除X1即可，也可以根据需要全部删除）
[root@wyx .X11-unix]# ls /tmp/.X11-unix
X0  X1  X2  X3  X4  X5  X6
 
保留config passwd xstartup即可
[root@wyx .vnc]# ls /root/.vnc/
config  wyx.pc.com:1.log  wyx.pc.com:2.pid  wyx.pc.com:3.pid  wyx.pc.com:4.pid
passwd  wyx.pc.com:2.log  wyx.pc.com:3.log  wyx.pc.com:4.log  xstartup
 
现在可以通过systemd管理服务了
systemctl start vncserver@:1.service
 
netstat -antulp | grep 59
tcp        0      0 0.0.0.0:5901            0.0.0.0:*               LISTEN      5611/Xvnc           
tcp6       0      0 :::5901                 :::*                    LISTEN      5611/Xvnc 

```