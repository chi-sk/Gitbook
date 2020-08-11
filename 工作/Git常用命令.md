# GIt常用命令
## 本地使用Git
- **配置用户名字和Email地址**
```
git config --global user.name "Your Nmae"
git config --global user.email "chi_sk@163.com"
```
- **创建版本库**
```
//创建一个版本库的空目录
mkdir learngit
cd learngit
pwd

//设置Git仓库的默认工作目录
git init 
initialized empty git repository in /D/Git_WS/.git/
```
- **将文件放到Git仓库**
```
git add test_1.txt
git add test_2.txt
git commit -m "Those are test files !"
```
## 时光机穿梭
1. 查看仓库的当前状态
```
git status
```
2. 查看当前未提交的文件做过哪些修改 
```
git diff test_1.txt
```
3. 提交新的修改
```
//提交新的修改和提交新文件一样
git add
test_1.txt
git status
git commit -m "add distributed"
git status
```
- 查看最近的提交日志
```
git log

//加上--pretty=oneline参数可以简化输出信息
git log --pretty=oneline
```
- 回退到上一个版本
```
git reset --hard HEAD^
//版本号没必要写全，前几位就可以，Git会自动去找
例: git reset --hard 3628164
使用 给 git reflog 可以显示最近提交过的历史命令
```
- 丢弃当前所做的修改
```
git checkout --test_1.txt
//该命令的作用就是将文件回到最近一次git commit或者 git add时的状态
```
- 删除文件
使用rm test_1.txt或者文件管理器删除文件后，在Git中相当于一次修改操作，可以使用commit命令提交修改或者用 git checkout --file_name.txt进行撤销。
使用 git rm test_1.txt从Git缓存区将文件删除。

- Git常用操作
```
git commit   --amend        撤销上一次提交  并讲暂存区文件重新提交
git checkout -- <file>      拉取暂存区文件 并将其替换成工作区文件
git reset HEAD  -- <file>   拉取最近一次提交到版本库的文件到暂存区  改操作不影响工作区
```
- 远程仓库 Github

创建SSH Key:
```c++
ssh-keygen -t rsa -C "chi_sk@163.com"
//一路回车即可
```
然后登陆Github，打开Settings，将SSH公钥添加到自己的Github账户。

- 添加远程库
登陆Github，创建一个新的Github仓库，以便将自己的本地仓库与之关联。
在本地连接远程Github仓库：
```c++
git remote add origin git@github.com:chi-sk/Git_ws.git
//chi-s为自己的Github账户名。Git_ws为刚刚建立的Github仓库名。
```
如果添加错误，可以使用git remote rm origin删除并重新添加。
- 推送到远程仓库
在本地提交之后，就可以通过下面命令推送到Github。
```
git push -u origin master
```
由于远程仓库是空的，第一次推送master分支时，加上了-u参数。
将远程库克隆到本地：
```
git clone git@github.com:chi-sk/Git_ws.git
```
## 分支管理
- 创建分支
创建dev分支，然后切换到dev分支
```
git checkout -b dev
```
git checkout命令加上-b表示创建并切换，相当于下面两条命令
```
git branch dev
git checkout dev
```
然后用git branch命令查看当前分支
```
git branch
//git branch 命令会列出所有分支，当前分支前面会加一个*号
```
当dev分支的工作完成，就可以切换回当前分支。
```
git checkout master
```
现在，将dev分支的工作成果合并到master分支上：
```
git merge dev
```
合并之后就可以使用下面命令删除dev分支了
```
git branch -d dev
```
- 解决冲突
如果我们新建一个feature分支，对某个文件做出修改并提交，然后切换到master分支对同一个文件做出修改并体交，此时master和feature分支分别有了自己的提交，执行`git merge feature`快速合并就会有冲突。
可以使用`git status`命令查看哪些文件存在冲突。
git使用<<<<<<<<,==========,>>>>>>>>标记出不同分支的内容，我们手动修改后再提交即可。
也可以使用git log命令查看分支合并情况。

```
git log --graph --pretty=oneline --abbrev-commit
```
最后删除frature分支即可。
- 如果合并了两个不同的开始提交的仓库，在新的 git 会发现这两个仓库可能不是同一个，为了防止开发者上传错误，于是就给下面的提示
```
fatal: refusing to merge unrelated histories
```
- 如我在Github新建一个仓库，写了License，然后把本地一个写了很久仓库上传。这时会发现 github 的仓库和本地的没有一个共同的 commit 所以 git 不让提交，认为是写错了 origin ，如果开发者确定是这个 origin 就可以使用` --allow-unrelated-histories  `告诉 git 自己确定遇到无法提交的问题，一般先pull 也就是使用 git pull origin master 这里的 origin 就是仓库，而 master 就是需要上传的分支，因为两个仓库不同，发现 git 输出` refusing to merge unrelated histories `无法 pull 内容,因为他们是两个不同的项目，要把两个不同的项目合并，git需要添加一句代码，在 git pull 之后，这句代码是在git 2.9.2版本发生的，最新的版本需要添加 ` --allow-unrelated-histories  `告诉 git 允许不相关历史合并


- 分支管理策略
通常合并分支时，Git会优先使用“Fast forward”模式，再删除分支后，就会丢掉分支信息。如果强制禁用“Fast forward”模式，使用merge合并分支时就会生成一个commit，在分支历史上就保留了分支信息。
下面实战使用`--no-ff`方式的merge。
```
git checkout -b dev
//修改readme.txt并commit
git add readme.txt
git checkout master
git merge --no-ff -m "do something" dev
//最后使用git log查看分支历史
git log --graph --pretty=oneline --abbrev-commit
```
Git还提供一个stash功能，把当前的工作现场压栈，等以后恢复现场后继续工作。

## 附
#### 在连接github时，执行”ssh -T git@github.com” 命令时，出现
```
ssh: connect to host github.com port 22: Connection timed out
```
**方案一：**
在存放公钥私钥(id_rsa和id_rsa.pub)的文件里，新建config文本，内容如下：

```
Host github.com
User YourEmail@163.com
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443
```
**方案二：**
连接超时，首先找到git的安装目录，找到/etc/ssh/ssh_config文件，用notepad++打开ssh_config文件。
把如下内容复制到ssh_config文件的末尾处：并记得保存。
```
Host github.com
User git
Hostname ssh.github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
Port 443
```
再使用：ssh -T git@github.com来测试git是否成功连接github。

---
#### 输入`git remote add origin git@github.com:chi_sk/Git_ws.git`,提示出错信息：fatal: remote origin already exists.

    解决办法如下：

    1、先输入git remote rm origin

    2、再输入git remote add origin git@github.com:djqiang/gitdemo.git 就不会报错了！

    3、如果输入git remote rm origin 还是报错的话，error: Could not remove config section 'remote.origin'. 我们需要修改gitconfig文件的内容

    4、找到你的Github仓库路径，里面有一个隐藏文件夹.git

    5、打开里面的config文件，它把里面的[remote "origin"]那一行删掉就好了！
#### 输入` ssh -T git@github.com`出现错误提示：`Permission denied (publickey)`.因为新生成的key不能加入ssh就会导致连接不上github。

解决办法如下：
    1、先输入ssh-agent，再输入ssh-add  ~/.ssh/id_key，这样就可以了。
    2、如果还是不行的话，输入ssh-add ~/.ssh/id_key 命令后出现报错Could not open a connection to your authentication agent.解决方法是key用Git Gui的ssh工具生成，这样生成的时候key就直接保存在ssh中了，不需要再ssh-add命令加入了，其它的user，token等配置都用命令行来做。
    3、最好检查一下在复制id_rsa.pub文件的内容时有没有产生多余的空格或空行，有些编辑器会帮你添加这些的。

#### 输入`git push origin master`提示出错信息：`error:failed to push som refs to .......`

解决办法如下：
    1、先输入git pull origin master //先把远程服务器github上面的文件拉下来
    2、再输入git push origin master
    3、如果出现报错 fatal: Couldn't find remote ref master或者fatal: 'origin' does not appear to be a git repository以及fatal: Could not read from remote repository.
    4、则需要重新输入$ git remote add origin git@github.com:djqiang/gitdemo.git


