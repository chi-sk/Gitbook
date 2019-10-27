

# shell编程100例

## 1. 编写hello world脚本
编写hello world脚本
```shell
#!/bin/bash
# 编写hello world脚本
echo "Hello World!"
```
## 2. 通过位置变量创建 Linux 系统账户及密码

```shell
#!/bin/bash
# 通过位置变量创建 Linux 系统账户及密码
#$1 是执行脚本的第一个参数,$2 是执行脚本的第二个参数
useradd "$1" 
echo "$2"  |  passwd  ‐‐stdin  "$1"

```
## 3. 备份日志
```shell
#!/bin/bash
# 每周 5 使用 tar 命令备份/var/log 下的所有日志文件
# vim  /root/logbak.sh
# 编写备份脚本,备份后的文件名包含日期标签,防止后面的备份将前面的备份数据覆盖
# 注意 date 命令需要使用反引号括起来,反引号在键盘<tab>键上面
tar	-czf	log-`date +%Y%m%d`.tar.gz	/var/log 
 
# crontab ‐e	#编写计划任务,执行备份脚本
00	03	**	5	/root/logbak.sh

```
## 4. 一键部署 LNMP(RPM 包版本)
```shell
#!/bin/bash
# 一键部署 LNMP(RPM 包版本)
# 使用 yum 安装部署 LNMP,需要提前配置好 yum 源,否则该脚本会失败
# 本脚本使用于 centos7.2 或 RHEL7.2
yum ‐y install httpd
yum ‐y install mariadb mariadb‐devel mariadb‐server
yum ‐y install php  php‐mysql
 
systemctl start httpd mariadb
systemctl enable httpd mariadb
```
## 5. 监控内存和磁盘容量，小于给定值时报警
```shell
#!/bin/bash
# 实时监控本机内存和硬盘剩余空间,剩余内存小于500M. 根分区剩余空间小于1000M时,发送报警邮件给root管理员
 
# 提取根分区剩余空间
disk_size=$(df / | awk '/\//{print $4}')
 
# 提取内存剩余空间
mem_size=$(free | awk '/Mem/{print $4}')
while :
do
# 注意内存和磁盘提取的空间大小都是以 Kb 为单位
if  [  $disk_size -le 512000 -a $mem_size -le 1024000  ]
then
    mail  ‐s  "Warning"  root  <<EOF
	Insufficient resources,资源不足
EOF
fi
done
```

## 6. 猜数字游戏
```shell
 #!/bin/bash
 
# 脚本生成一个 100 以内的随机数,提示用户猜数字,根据用户的输入,提示用户猜对了,
# 猜小了或猜大了,直至用户猜对脚本结束。
 
# RANDOM 为系统自带的系统变量,值为 0‐32767的随机数
# 使用取余算法将随机数变为 1‐100 的随机数
num=$[RANDOM%100+1]
echo "$num"
 
# 使用 read 提示用户猜数字
# 使用 if 判断用户猜数字的大小关系:‐eq(等于),‐ne(不等于),‐gt(大于),‐ge(大于等于),
# ‐lt(小于),‐le(小于等于)
while  :
do
	read -p "计算机生成了一个 1‐100 的随机数,你猜: " cai
    if [ $cai -eq $num ]
    then
       	echo "恭喜,猜对了"
       	exit
    	elif [ $cai -gt $num ]
    	then
           	echo "Oops,猜大了"
      	else
           	echo "Oops,猜小了"
 	fi
done
```

## 7. 检测本机当前用户是否为超级管理员,如果是管理员,则使用 yum 安装 vsftpd,如果不是,则提示您非管理员(使用字串对比版本)
```shell
#!/bin/bash
# 检测本机当前用户是否为超级管理员,如果是管理员,则使用 yum 安装 vsftpd,如果不
# 是,则提示您非管理员(使用字串对比版本) 
if [ $USER == "root" ]
then
	yum ‐y install vsftpd
else
    echo "您不是管理员,没有权限安装软件"
fi
```
## 8. 检测本机当前用户是否为超级管理员,如果是管理员,则使用 yum 安装 vsftpd,如果不是,则提示您非管理员(使用 UID 数字对比版本)
```shell
#!/bin/bash
# 检测本机当前用户是否为超级管理员,如果是管理员,则使用 yum 安装 vsftpd,如果不
# 是,则提示您非管理员(使用 UID 数字对比版本)
if [ $UID -eq 0 ];then
    yum ‐y install vsftpd
else
    echo "您不是管理员,没有权限安装软件"
fi
```

## 9. 编写脚本:提示用户输入用户名和密码,脚本自动创建相应的账户及配置密码。如果用户不输入账户名,则提示必须输入账户名并退出脚本;如果用户不输入密码,则统一使用默认的 123456 作为默认密码。
```shell
#!/bin/bash
# 编写脚本:提示用户输入用户名和密码,脚本自动创建相应的账户及配置密码。如果用户
# 不输入账户名,则提示必须输入账户名并退出脚本;如果用户不输入密码,则统一使用默
# 认的 123456 作为默认密码。
 
read -p "请输入用户名: " user
#使用‐z 可以判断一个变量是否为空,如果为空,提示用户必须输入账户名,并退出脚本,退出码为 2
#没有输入用户名脚本退出后,使用$?查看的返回码为 2
if [ -z $user ];then
   	echo "您不需输入账户名"
 	exit 2
fi
#使用 stty ‐echo 关闭 shell 的回显功能
#使用 stty  echo 打开 shell 的回显功能
stty -echo
read -p "请输入密码: " pass
stty echo
pass=${pass:‐123456}
useradd "$user"
echo "$pass" | passwd ‐‐stdin "$user"

```

## 10. 输入三个数并进行升序排序
```shell
#!/bin/bash
# 依次提示用户输入 3 个整数,脚本根据数字大小依次排序输出 3 个数字
read -p "请输入一个整数:" num1
read -p "请输入一个整数:" num2
read -p "请输入一个整数:" num3
# 不管谁大谁小,最后都打印 echo "$num1,$num2,$num3"
# num1 中永远存最小的值,num2 中永远存中间值,num3 永远存最大值
# 如果输入的不是这样的顺序,则改变数的存储顺序,如:可以将 num1 和 num2 的值对调
tmp=0
# 如果 num1 大于 num2,就把 num1 和和 num2 的值对调,确保 num1 变量中存的是最小值
if [ $num1 -gt $num2 ];then   
	tmp=$num1
	num1=$num2
	num2=$tmp
fi
# 如果 num1 大于 num3,就把 num1 和 num3 对调,确保 num1 变量中存的是最小值
if [ $num1 -gt $num3 ];then   
  	tmp=$num1
  	num1=$num3
  	num3=$tmp
fi
# 如果 num2 大于 num3,就把 num2 和 num3 对标,确保 num2 变量中存的是小一点的值
if [ $num2 -gt $num3 ];then
  	tmp=$num2
  	num2=$num3
  	num3=$tmp
fi
echo "排序后数据(从小到大)为:$num1,$num2,$num3"

```
## 11. 石头. 剪刀. 布游戏
```shell

```
## 12. 编写脚本测试 192.168.4.0/24 整个网段中哪些主机处于开机状态,哪些主机处于关机状态(for 版本)
```shell

```
## 13. 编写脚本测试 192.168.4.0/24 整个网段中哪些主机处于开机状态,哪些主机处于关机状态(while 版本)
```shell

```
### 14. 编写脚本测试 192.168.4.0/24 整个网段中哪些主机处于开机状态,哪些主机处于关机状态(多进程版)
```shell

```
## 15. 编写脚本,显示进度条
```shell

```
## 16. 进度条,动态时针版本；定义一个显示进度的函数,屏幕快速显示| / ‐ \
```shell

```
## 17. 9*9 乘法表
```shell

```
## 18. 使用死循环实时显示 eth0 网卡发送的数据包流量
```shell

```
## 19. 使用 user.txt 文件中的人员名单,在计算机中自动创建对应的账户并配置初始密码本脚本执行,需要提前准备一个 user.txt 文件,该文件中包含有若干用户名信息
```shell

```
## 20. 编写批量修改扩展名脚本
```shell

```
## 21. 使用 expect 工具自动交互密码远程其他主机安装 httpd 软件
```shell

```
## 22. 一键部署 LNMP(源码安装版本)
```shell

```
## 23. 编写脚本快速克隆 KVM 虚拟机
```shell

```
## 24. 点名器脚本
```shell

```
## 25. 查看有多少远程的 IP 在连接本机
```shell

```
## 26. 对 100 以内的所有正整数相加求和(1+2+3+4...+100)
```shell

```
## 27. 统计 13:30 到 14:30 所有访问 apache 服务器的请求有多少个
```shell

```
## 28. 统计 13:30 到 14:30 所有访问本机 Aapche 服务器的远程 IP 地址是什么
```shell

```
## 29. 打印国际象棋棋盘
```shell

```
## 30. 统计每个远程 IP 访问了本机 apache 几次?
```shell

```
## 31. 统计当前 Linux 系统中可以登录计算机的账户有多少个
```shell

```
## 32. 统计/var/log 有多少个文件,并显示这些文件名
```shell

```
## 33. 自动为其他脚本添加解释器信息
```shell

```
## 34. 自动化部署 varnish 源码包软件
```shell

```
## 35. 编写 nginx 启动脚本
```shell

```
## 36. 自动对磁盘分区. 格式化. 挂载
```shell

```
## 37. 自动优化 Linux 内核参数
```shell

```
## 38. 切割 Nginx 日志文件(防止单个文件过大,后期处理很困难)
```shell

```
## 39. 检测 MySQL 数据库连接数量
```shell

```
## 40. 根据 md5 校验码,检测文件是否被修改
```shell

```
## 41. 检测 MySQL 服务是否存活
```shell

```
## 42. 备份 MySQL 的 shell 脚本(mysqldump版本)
```shell

```
## 43. 将文件中所有的小写字母转换为大写字母
```shell

```
## 44. 非交互自动生成 SSH 密钥文件
```shell

```
## 45. 检查特定的软件包是否已经安装
```shell

```
## 46. 监控 HTTP 服务器的状态(测试返回码)
```shell

```
## 47. 自动添加防火墙规则,开启某些服务或端口(适用于 RHEL7)
```shell

```
## 48. 使用脚本自动创建逻辑卷
```shell

```
## 49. 显示 CPU 厂商信息
```shell

```
## 50. 删除某个目录下大小为 0 的文件
```shell

```
## 51. 查找 Linux 系统中的僵尸进程
```shell

```
## 52. 提示用户输入年份后判断该年是否为闰年
```shell

```
## 53. 生成随机密码(urandom 版本)
```shell

```
## 54. 生成随机密码(字串截取版本)
```shell

```
## 55. 生成随机密码(UUID 版本,16 进制密码)
```shell

```
## 56. 生成随机密码(进程 ID 版本,数字密码)
```shell

```
## 57. 测试用户名与密码是否正确
```shell

```
## 58. 循环测试用户名与密码是否正确
```shell

```
## 59. Shell 脚本的 fork 炸弹
```shell

```
## 60. 批量下载有序文件(pdf. 图片. 视频等等)
```shell

```
## 61. 显示当前计算机中所有账户的用户名称
```shell

```
## 62. 制定目录路径,脚本自动将该目录使用 tar 命令打包备份到/data目录
```shell

```
## 63. 显示进度条(回旋镖版)
```shell

```
## 64. 安装 LAMP 环境(yum 版本)
```shell

```
## 65. 循环关闭局域网中所有主机
```shell

```
## 66. 获取本机 MAC 地址
```shell

```
## 67. 自动配置 rsynd 服务器的配置文件 rsyncd.conf
```shell

```
## 68. 修改 Linux 系统的最大打开文件数量
```shell

```
## 69. 设置 Python 支持自动命令补齐功能
```shell

```
## 70. 自动修改计划任务配置文件
```shell

```
## 71. 使用脚本循环创建三位数字的文本文件(111-999 的文件)
```shell

```
## 72. 找出/etc/passwd 中能登录的用户,并将对应在/etc/shadow 中第二列密码提出处理
```shell

```
## 73. 统计/etc/passwd 中 root 出现的次数
```shell

```
## 74. 统计 Linux 进程相关数量信息
```shell

```
## 75. 从键盘读取一个论坛积分,判断论坛用户等级
```shell

```
## 76. 判断用户输入的数据类型(字母. 数字或其他) 
```shell

```
## 77. 显示进度条(数字版) 
```shell

```
## 78. 打印斐波那契数列
```shell

```
## 79. 判断用户输入的是 Yes 或 NO
```shell

```
## 80. 显示本机 Linux 系统上所有开放的端口列表
```shell

```
## 81. 将 Linux 系统中 UID 大于等于 1000 的普通用户都删除
```shell

```
## 82. 使用脚本开启关闭虚拟机
```shell

```
## 83. 调整虚拟机内存参数的 shell 脚本 
```shell

```
## 84. 查看 KVM 虚拟机中的网卡信息(不需要进入启动或进入虚拟机) 
```shell

```
## 85. 不登陆虚拟机,修改虚拟机网卡 IP 地址
```shell

```
## 86. 破解虚拟机密码,无密码登陆虚拟机系统
```shell

```
## 87. Shell 脚本对信号的处理,执行脚本后,按键盘 Ctrl+C 无法终止的脚本
```shell

```
## 88. 一键部署 memcached
```shell

```
## 89. 一键配置 VNC 远程桌面服务器(无密码版本)
```shell

```
## 90. 关闭 SELinux
```shell
#!/bin/bash
# 关闭 SELinux 
 
sed -i  '/^SELINUX/s/=.*/=disabled/' /etc/selinux/config
setenforce 0

```
## 91. 查看所有虚拟机磁盘使用量以及CPU使用量信息
```shell
#!/bin/bash
# 查看所有虚拟机磁盘使用量以及CPU使用量信息 
 
virt‐df
read -n1 "按任意键继续" key
virt‐top

```
## 92. 使用 shell 脚本打印图形
```shell
#!/bin/bash
# 使用 shell 脚本打印如下图形: 
 
# 打印第一组图片
# for(())为类 C 语言的语法格式,也可以使用 for i  in;do  ;done 的格式替换
# for((i=1;i<=9;i++))循环会执行 9 次,i 从 1 开始到 9,每循环一次 i 自加 1
clear
for (( i=1; i<=9; i++ ))
do
  for (( j=1; j<=i; j++ ))
  do
    echo -n "$i"
  done
  echo ""
done
read  -n1  "按任意键继续"  key
#打印第二组图片
clear
for (( i=1; i<=5; i++ )) 
do
  for (( j=1; j<=i; j++ ))
  do
    echo -n " |"
  done
  echo "_ "
done
read  -n1  "按任意键继续"  key
#打印第三组图片
clear
for (( i=1; i<=5; i++ ))
do
  for (( j=1; j<=i; j++ ))
  do
    echo -n " *"
  done
  echo ""
done
for (( i=5; i>=1; i‐‐ ))
do
  for (( j=1; j<=i; j++ ))
  do
    echo -n " *"
  done
  echo ""
done

```
## 93. 根据计算机当前时间,返回问候语,可以将该脚本设置为开机启动
```shell
#!/bin/bash
# 根据计算机当前时间,返回问候语,可以将该脚本设置为开机启动 
 
# 00‐12 点为早晨,12‐18 点为下午,18‐24 点为晚上
# 使用 date 命令获取时间后,if 判断时间的区间,确定问候语内容
tm=$(date +%H)
if [ $tm -le 12 ];then
	msg="Good Morning $USER"
elif [ $tm -gt 12 -a $tm -le 18 ];then
  	msg="Good Afternoon $USER"
else
  	msg="Good Night $USER"
fi
echo "当前时间是:$(date +"%Y‐%m‐%d %H:%M:%S")"
echo -e "\033[34m$msg\033[0m"

```
## 94. 读取用户输入的账户名称,将账户名写入到数组保存
```shell
#!/bin/bash
# 读取用户输入的账户名称,将账户名写入到数组保存 
 
# 定义数组名称为 name,数组的下标为 i,小标从 0 开始,每输入一个账户名,下标加 1,继续存下一个账户
# 最后,输入 over,脚本输出总结性信息后脚本退出
i=0
while :
do
	read -p "请输入账户名,输入 over 结束:" key
	if [ $key == "over" ];then 
		break
  	else
		name[$i]=$key
		let i++
  	fi
done
echo "总账户名数量:${#name[*]}"
echo "${name[@]}"

```
## 95. 判断文件或目录是否存在
```shell
#!/bin/bash
# 判断文件或目录是否存在 
 
if [ $# -eq 0 ] ;then
echo "未输入任何参数,请输入参数"
echo "用法:$0 [文件名|目录名]"
fi
if [ -f $1 ];then
	echo "该文件,存在"
	ls -l $1
else
	echo "没有该文件"
fi
if [ -d  $1 ];then
   	echo "该目录,存在"
   	ls -ld  $2
else
   	echo "没有该目录"
fi

```
## 96. 打印各种格式的时间
```shell
#!/bin/bash
# 打印各种时间格式 
 
echo "显示星期简称(如:Sun)"
date +%a
echo "显示星期全称(如:Sunday)"
date +%A
echo "显示月份简称(如:Jan)"
date +%b
echo "显示月份全称(如:January)"
date +%B
echo "显示数字月份(如:12)"
date +%m
echo "显示数字日期(如:01 号)"
date +%d
echo "显示数字年(如:01 号)"
date +%Y echo "显示年‐月‐日"
date +%F
echo "显示小时(24 小时制)"
date +%H
echo "显示分钟(00..59)"
date +%M
echo "显示秒"
date +%S
echo "显示纳秒"
date +%N
echo "组合显示"
date +"%Y%m%d %H:%M:%S"

```
## 97. 使用 egrep 过滤 MAC 地址
```shell
#!/bin/bash
# 使用 egrep 过滤 MAC 地址 
 
# MAC 地址由 16 进制组成,如 AA:BB:CC:DD:EE:FF
# [0‐9a‐fA‐F]{2}表示一段十六进制数值,{5}表示连续出现5组前置:的十六进制
egrep "[0‐9a‐fA‐F]{2}(:[0‐9a‐fA‐F]{2}){5}" $1

```
## 98. 统计双色球各个数字的中奖概率
```shell
#!/bin/bash
# 统计双色球各个数字的中奖概率 
 
# 往期双色球中奖号码如下:
# 01 04 11 28 31 32  16
# 04 07 08 18 23 24  02
# 02 05 06 16 28 29  04
# 04 19 22 27 30 33  01
# 05 10 18 19 30 31  03
# 02 06 11 12 19 29  06
# 统计篮球和红球数据出现的概率次数(篮球不分顺序,统计所有篮球混合在一起的概率)
awk '{print $1"\n"$2"\n"$3"\n"$4"\n"$5"\n"$6}' 1.txt | sort | uniq -c | sort
awk '{print $7}' 1.txt | sort | uniq -c | sort

```
## 99. 生成签名私钥和证书
```shell
#!/bin/bash
# 生成签名私钥和证书 
 
read -p "请输入存放证书的目录:" dir
if [ ! -d $dir ];then
	echo "该目录不存在"
	exit
fi
read -p "请输入密钥名称:" name
# 使用 openssl 生成私钥
openssl genrsa -out ${dir}/${name}.key
# 使用 openssl 生成证书 #subj 选项可以在生成证书时,非交互自动填写 Common Name 信息
openssl req -new -x509 -key ${dir}/${name}.key -subj "/CN=common" -out ${dir}/${name}.crt

```
## 100. 使用awk编写的wc程序
```shell
#!/bin/bash
# 使用awk编写的wc程序 
 
# 自定义变量 chars 变量存储字符个数,自定义变量 words 变量存储单词个数
# awk 内置变量 NR 存储行数
# length()为 awk 内置函数,用来统计每行的字符数量,因为每行都会有一个隐藏的$,所以每次统计后都+1
# wc 程序会把文件结尾符$也统计在内,可以使用 cat ‐A 文件名,查看该隐藏字符
awk '{chars+=length($0)+1;words+=NF} END{print NR,words,chars}' $1

```