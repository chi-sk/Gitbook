## ubuntu18.04.1 设置开机默认进入命令行模式/用户图形界面
- **开机默认进入命令行模式**
1、输入命令：`sudo systemctl set-default multi-user.target `2、重启：`reboot`
要进入图形界面，只需要输入命令`startx`
从图形界面切换回命令行：`ctrl+alt+F7`

- **开机默认进入图形用户界面**
1、输入命令：`sudo systemctl set-default graphical.target` 2、重启：`reboot`
要进入命令行模式：`ctrl+alt+F2`
从命令行切换到图形界面：`ctrl+alt+F7`

[Ubuntu16.04 64位 + GTX1070显卡驱动 + CUDA 8.0](https://blog.csdn.net/lansetiankong2104/article/details/53858868)
[NVIDIA 驱动安装(超详细) ](https://www.cnblogs.com/pprp/p/9430836.html)
