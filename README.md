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
现在，你已经学会了修改文件，然后把修改提交到Git版本库，现在，再练习一次，修改readme.txt文件如下：

> Git is a distributed version control system.
>
> Git is free software distributed under the GPL.

然后尝试提交：

> $ git add readme.txt
>
> $ git commit -m "append GPL"
>
> [master 1094adb] append GPL
> 1 file changed, 1 insertion(+), 1 deletion(-)

像这样，你不断对文件进行修改，然后不断提交修改到版本库里,每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为`commit`。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个`commit`恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

现在，我们回顾一下readme.txt文件一共有几个版本被提交到Git仓库里了：

版本1：wrote a readme file

> Git is a version control system.
>
> Git is free software.

版本2：add distributed

> Git is a distributed version control system.
>
> Git is free software.

版本3：append GPL

> Git is a distributed version control system.
>
> Git is free software distributed under the GPL.

当然了，在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容，不然要版本控制系统干什么。版本控制系统肯定有某个命令可以告诉我们历史记录，在Git中，我们用`git log`命令查看：
> $ git log
>
> commit 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master)
> Author: Michael Liao <askxuefeng@gmail.com>
> Date:   Fri May 18 21:06:15 2018 +0800
>    append GPL
> commit e475afc93c209a690c39c13a46716e8fa000c366
> Author: Michael Liao <askxuefeng@gmail.com>
> Date:   Fri May 18 21:03:36 2018 +0800
>    add distributed
> commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
> Author: Michael Liao <askxuefeng@gmail.com>
> Date:   Fri May 18 20:59:18 2018 +0800
>    wrote a readme file

`git log`命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是`append GPL`，上一次是`add distributed`，最早的一次是`wrote a readme file`。

如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：
> $ git log --pretty=oneline
>
> 1094adb7b9b3807259d8cb349e7df1d4d6477073 (HEAD -> master) append GPL
> e475afc93c209a690c39c13a46716e8fa000c366 add distributed
> eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file

每提交一个新版本，实际上Git就会把它们自动串成一条时间线

好了，现在我们启动时光穿梭机，准备把`readme.txt`回退到上一个版本，也就是`add distributed`的那个版本，怎么做呢？

首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

现在，我们要把当前版本`append GPL`回退到上一个版本`add distributed`，就可以使用`git reset`命令：

> $ git reset --hard HEAD^
>
> HEAD is now at e475afc add distributed

--hard参数有啥意义？这个后面再讲，现在你先放心使用。

看看`readme.txt`的内容是不是版本`add distributed`：

> $ cat readme.txt
>
> Git is a distributed version control system.
> Git is free software.

果然被还原了。

还可以继续回退到上一个版本`wrote a readme file`，不过且慢，然我们用`git log`再看看现在版本库的状态：

> $ git log
>
> commit e475afc93c209a690c39c13a46716e8fa000c366 (HEAD -> master)
> Author: Michael Liao <askxuefeng@gmail.com>
> Date:   Fri May 18 21:03:36 2018 +0800
>    add distributed
> commit eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0
> Author: Michael Liao <askxuefeng@gmail.com>
> Date:   Fri May 18 20:59:18 2018 +0800
>    wrote a readme file

最新的那个版本append GPL已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append GPL的commit id是1094adb...，于是就可以指定回到未来的某个版本：

> $ git reset --hard 1094a
>
> HEAD is now at 83b0afe append GPL

版本号没必要写全，前几位就可以了，Git会自动去找。

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的`HEAD`指针，当你回退版本的时候，Git仅仅是把`HEAD`从指向`append GPL`：
> ┌────┐
>
> │HEAD│
>
> └────┘
>   │
>
>   └──> ○ append GPL
>
>        │
>
>        ○ add distributed
>
>        │
>
>        ○ wrote a readme file

改为指向add distributed：

> ┌────┐
>
> │HEAD│
>
> └────┘
>
>   │
>
>   │    ○ append GPL
>
>   │    │
>
>   └──> ○ add distributed
>
>        │
>
>        ○ wrote a readme file

然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的`commit id`怎么办？

Git提供了一个命令`git reflog`用来记录你的每一次命令：
> $ git reflog
>
> e475afc HEAD@{1}: reset: moving to HEAD^
> 1094adb (HEAD -> master) HEAD@{2}: commit: append GPL
> e475afc HEAD@{3}: commit: add distributed
> eaadf4e HEAD@{4}: commit (initial): wrote a readme file
### 工作区和暂存区
Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。

- **工作区（Working Directory）**
就是你在电脑里能看到的目录
- **版本库（Repository）**

工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用`git add`把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个`master`分支，所以，现在，`git commit`就是往`master`分支上提交更改。

简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

现在，我们再练习一遍，先对readme.txt做个修改，比如加上一行内容：
> Git is a distributed version control system.
>
> Git is free software distributed under the GPL.
>
>Git has a mutable index called stage.

然后，在工作区新增一个`LICENSE`文本文件（内容随便写）。

先用`git status`查看一下状态：

> $ git status

`readme.txt`被修改了 而`LICENSE`还从来没有被添加过，所以它的状态应该是`Untracked`。

现在，使用两次命令`git add`，把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

> $ git status
>
> On branch master
> nothing to commit, working tree clean

### 管理修改
为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。

第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`

每次修改，如果不用`git add`到暂存区，那就不会加入到`commit`中。
### 撤销修改

`git checkout -- file`可以丢弃工作区的修改：
> $ git checkout -- readme.txt

命令`git checkout -- readme.txt`意思就是，把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

一种是`readme.txt`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是`readme.txt`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次`git commit`或`git add`时的状态。

`git checkout -- file`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到`git checkout`命令。

如果已经`add`到暂存区了，在`commit`发现了这个问题用`git status`查看一下，修改只是添加到了暂存区，还没有提交

用命令`git reset HEAD <file>`可以把暂存区的修改撤销掉（unstage），重新放回工作区：

> $ git reset HEAD readme.txt
>
> Unstaged changes after reset:
> M	readme.txt

git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。

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