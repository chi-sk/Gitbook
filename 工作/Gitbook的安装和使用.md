# Ubuntu命令行安装gitbook
Gitbook依赖于Node.j 4.0或其以上版本
### 安装`Node.js  v12.x`
[参考官方首次](https://github.com/nodesource/distributions/blob/master/README.md)
```
# Using Ubuntu
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs

# Using Debian, as root
curl -sL https://deb.nodesource.com/setup_12.x | bash -
apt-get install -y nodejs
```
同时还需要下载一个依赖工具：
```
sudo apt-get install -y build-essential
```
查看nodejs与npm版本: 
```
nodejs -v 
v4.4.2 
npm -v 
2.15.0
```
### 安装gitbook
```
sudo npm install -g gitbook-cli
```
查看gitbook是否安装成功
```
gitbook -V
```
gitbook导出pdf功能需要安装
```
sudo apt-get install calibre 
```
### 命令行gitbook 使用
在书目录下，初始化
```
gitbook init
```
编译生成静态网页
```
gitbook build
```
在本地通过静态网址访问
```
gitbook serve
```
生成pdf
```
gitbook pdf .
```
---

