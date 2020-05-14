## 目录

- [安装Git](#安装Git)
- [创建版本库](#创建版本库)
- [时光机穿梭](#时光机穿梭)
	- [版本回退](#版本回退)
	- [工作区和暂存区](#工作区和暂存区)
	- [管理修改](#管理修改)
	- [撤销修改](#撤销修改)
	- [删除文件](#删除文件)
- [远程仓库](#远程仓库)
	- [添加远程库](#添加远程库)
	- [从远程库克隆](#从远程库克隆)
- [分支管理](#分支管理)
	- [创建与合并分支](#创建与合并分支)
	- [解决冲突](#解决冲突)
	- [分支管理策略](#分支管理策略)
	- [Bug分支](#Bug分支)
	- [Feature分支](#Feature分支)
	- [多人协作](#多人协作)
	- [Rebase](#Rebase)
- [标签管理](#标签管理)
	- [创建标签](#创建标签)
	- [操作标签](#操作标签)
- [使用GitHub](#使用GitHub)
- [使用Gitee](#使用Gitee)
- [自定义Git](#自定义Git)
	- [忽略特殊文件](#忽略特殊文件)
	- [配置别名](#配置别名)
	- [搭建Git服务器](#搭建Git服务器)
- [使用SourceTree](#使用SourceTree)

## 安装Git
- **在Linux上安装Git**

首先，你可以试着输入git，看看系统有没有安装Git：
> $ git
>
> The program 'git' is currently not installed. You can install it by typing:sudo apt-get install git

像上面的命令，有很多Linux会友好地告诉你Git没有安装，还会告诉你如何安装Git。

如果你碰巧用Debian或Ubuntu Linux，通过一条`sudo apt-get install` git就可以直接完成Git的安装，非常简单。

老一点的Debian或Ubuntu Linux，要把命令改为`sudo apt-get install git-core`，因为以前有个软件也叫GIT（GNU Interactive Tools），结果Git就只能叫`git-core`了。由于Git名气实在太大，后来就把GNU Interactive Tools改成gnuit，git-core正式改为git。

如果是其他Linux版本，可以直接通过源码安装。先从Git官网下载源码，然后解压，依次输入：`./config`，`make`，`sudo make install`这几个命令安装就好了。

- **在Mac OS X上安装Git**

如果你正在使用Mac做开发，有两种安装Git的方法。

一是安装homebrew，然后通过homebrew安装Git，具体方法请参考homebrew的文档：http://brew.sh/ 

第二种方法更简单，也是推荐的方法，就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。

![在Mac OS X上安装Git](https://www.liaoxuefeng.com/files/attachments/919018691743136/0)

Xcode是Apple官方IDE，功能非常强大，是开发Mac和iOS App的必选装备，而且是免费的！

- **在Windows上安装Git**

在Windows上使用Git，可以从[Git官网](https://git-scm.com/downloads)直接下载安装程序，然后按默认选项安装即可。

国内官网下载较慢，建议从[国内镜像下载](https://github.com/waylau/git-for-win)

安装完成后，在开始菜单里找到`Git`->`Git Bash`，蹦出一个类似命令行窗口的东西，就说明Git安装成功！
![在Windows上安装Git](https://github.com/1145990396/git/blob/master/Photo/1.png?raw=true)

安装完成后，还需要最后一步设置，在命令行输入：

> $ git config --global user.name "Your Name"
>
> $ git config --global user.email "email@email.com"

因为Git是分布式版本控制系统，所以每个机器都要有你的名字和email地址。

注意`git config`命令和`--global`参数，用了这个参数，表示你的机器上所以的Git库都会使用这个配置

## 创建版本库
什么是版本库呢，版本库又叫仓库，英文名repository，可以简单理解为一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改，删除，Git都能跟踪，任何时刻都可以追踪历史，或者在将来某个时刻可以还原

所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：

> $ mkdir learngit
>
> $ cd learngit
>
> pwd
>
> /Users/wuxianxin/learngit 

`pwd`命令用于显示当前目录 

第二步，通过`git init`命令把这个目录变成Git的仓库

> $ git init
>
> Initialized empty Git repository in /Users/wuxianxin/learngit/.git/ 

仓库建好了，并且是一个空的仓库，文件夹下面会有一个`.git`的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

如果你没有看到`.git`目录，那么它是一个隐藏的目录，用`ls -ah`命令就可以看见。也可以更改电脑属性看到

现在我们编写一个`readme.txt`文件，内容如下：
> Git is a version control system.
>
> Git is free software.

一定要放到learngit目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害也找不到这个文件。

第一步，用命令`git add`告诉Git，把文件添加到仓库：
> $ git add readme.txt

执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

第二步，用命令`git commit`告诉Git，把文件提交到仓库：
> $ git commit -m "wrote a readme" 
>
> [master (root-commit) eaadf4e] wrote a readme file
>
> 1 file changed, 2 insertions(+)
>
> create mode 100644 readme.txt

简单解释下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容

`git commit`命令执行成功后会告诉你`1 file changed`1个文件被改动（我们新添加的readme.txt文件）,`2 insertions`：插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要`add`，`commit`一共两步呢？因为`commit`可以一次提交很多文件，所以你可以多次`add`不同的文件，比如：
> $ git add file1.txt
>
> $ git add file2.txt file3.txt
>
> $ git commit -m "add 3 files."
## 时光机穿梭
我们已经成功地添加并提交了一个readme.txt文件，现在，是时候继续工作了，于是，我们继续修改readme.txt文件，改成如下内容：
> Git is a distributed version control system.
>
> Git is free software.

现在，运行`git status`命令看看结果：
> $ git status
>
> On branch master
> Changes not staged for commit:
>  (use "git add <file>..." to update what will be committed)
>  (use "git checkout -- <file>..." to discard changes in working directory)
>	modified:   readme.txt
> no changes added to commit (use "git add" and/or "git commit -a")

`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。

虽然Git告诉我们`readme.txt`被修改了，但如果能看看具体修改了什么内容,需要用`git diff`这个命令看看：

> $ git diff readme.txt 
>
> diff --git a/readme.txt b/readme.txt
>index 46d49bf..9247db6 100644
> --- a/readme.txt
> +++ b/readme.txt
> @@ -1,2 +1,2 @@
> -Git is a version control system.
> +Git is a distributed version control system.
> Git is free software.

`git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，我们在第一行添加了一个`distributed`单词。

知道了对`readme.txt`作了什么修改后，再把它提交到仓库，提交修改和提交新文件是一样的两步，第一步是git add：

> $ git add readme.txt

同样没有任何输出。在执行第二步`git commit`之前，我们再运行`git status`看看当前仓库的状态：

> $ git status
>
> On branch master
> Changes to be committed:
>  (use "git reset HEAD <file>..." to unstage)
>
>	modified:   readme.txt

`git status`告诉我们，将要被提交的修改包括`readme.txt`，下一步，就可以放心地提交了：

> $ git commit -m "add distributed"
>
> [master e475afc] add distributed
> 1 file changed, 1 insertion(+), 1 deletion(-)

提交后，我们再用`git status`命令看看仓库的当前状态：

> $ git status
>
> On branch master
> nothing to commit, working tree clean
### 版本回退
### 工作区和暂存区
### 管理修改
### 撤销修改
### 删除文件
## 远程仓库
### 添加远程库
### 从远程库克隆
## 分支管理
### 创建与合并分支
### 解决冲突
### 分支管理策略
### Bug分支
### Feature分支
### 多人协作
### Rebase
## 标签管理
### 创建标签
### 操作标签
## 使用GitHub
## 使用Gitee
## 自定义Git
### 忽略特殊文件
### 配置别名
### 搭建Git服务器
## 使用SourceTree