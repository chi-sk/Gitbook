查看/etc/inittab如下：
```cpp
# systemd uses 'targets' instead of runlevels. 
# by default, there are two main targets:
#
# multi-user.target: analogous to runlevel 3
# graphical.target: analogous to runlevel 5
#
# To view current default target, run:
# systemctl get-default
#
# To set a default target, run:
# systemctl set-default TARGET.target

```
新版本的CentOS 系统里使用’targets’ 取代了运行级别的概念。系统有两种默认的’targets’: 多用户.target 对应之前版本的3 运行级别； 而图形.target 对应之前的5运行级别。

查看默认的target，执行：
```
systemctl get-default
```
开机以命令模式启动，执行：
```
systemctl set-default multi-user.target
```
开机以图形界面启动，执行：
```
systemctl set-default graphical.target
```