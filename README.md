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

< $ git config --global user.name "Your Name"
<
< $ git config --global user.email "email@email.com"

因为Git是分布式版本控制系统，所以每个机器都要有你的名字和email地址。

注意`git config`命令和`--global参数`，用了这个参数，表示你的机器上所以的Git库都会使用这个配置

## 创建版本库
## 时光机穿梭
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