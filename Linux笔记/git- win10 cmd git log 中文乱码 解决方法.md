在win10中，用cmd或者bash中使用git时候，经常遇到乱码问题，网上类似的教程很多，一般可以直接在cmd/bash中输入如下设置命令：

```
git config --global core.quotepath false 
git config --global gui.encoding utf-8
git config --global i18n.commit.encoding utf-8 
git config --global i18n.logoutputencoding utf-8 
# bash 环境下
export LESSCHARSET=utf-8
# cmd环境下：
set LESSCHARSET=utf-8

```