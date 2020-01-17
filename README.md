## 《史上最简单的 git - 简明指南 教程》
### 助你入门 git 的简明指南，木有高深内容

### [下载 git OSX 版](https://git-scm.com/download/mac)
### [下载 git Windows 版](https://gitforwindows.org/)
### [下载 git Linux 版](https://book.git-scm.com/2_installing_git.html)

#### 首先你得注册一个自己的GitHub账号，注册网址：https://github.com/join
1. 有了自己的账号以后，就可以进行登录，开始创建一个新的项目
2. 创建一个新的项目，填写项目名称，描述
3. 创建完成之后，跳转到下面的页面，记住网址，在后面上传代码的时候需要使用
4. 接下来，我们需要先下载Git，这里最好下载最新版本的Git，安装时如果没有特殊需求，一直下一步就可以了，安装完成之后，cmd双击打开Git Bash

**创建新仓库**
> 创建新文件夹，打开，然后执行
> 
> git int
> 
> 以创建新的 git 仓库。

**检出仓库**
> 执行如下命令以创建一个本地仓库的克隆版本：
>
> git clone /path/to/repository
> 
> 如果是远端服务器上的仓库，你的命令会是这个样子：
>
> git clone https://github.com/1145990396/JavaGuide.git

**工作流**
> 
```你的本地仓库由 git 维护的三棵“树”组成。第一个是你的 工作目录，它持有实际文件；第二个是 暂存区（Index），它像个缓存区域，临时保存你的改动；最后是 HEAD，它指向你最后一次提交的结果。```

**添加和提交**
> 你可以提出更改（把它们添加到暂存区），使用如下命令：
>
> git add filename
>
> git add *
>
> 这是 git 基本工作流程的第一步；使用如下命令以实际提交改动：
> 
> git commit -m "代码提交信息"
> 
> 现在，你的改动已经提交到了 HEAD，但是还没到你的远端仓库。
> 
**推送改动**
> 你的改动现在已经在本地仓库的 HEAD 中了。执行如下命令以将这些改动提交到远端仓库：
>
> git push origin master
> 
> 可以把 master 换成你想要推送的任何分支。
>
> 如果你还没有克隆现有仓库，并欲将你的仓库连接到某个远程服务器，你可以使用如下命令添加：
>
> git remote add origin server
>
> 如此你就能够将你的改动推送到所添加的服务器上去了。
>
**分支**
> 分支是用来将特性开发绝缘开来的。在你创建仓库的时候，master 是“默认的”分支。在其他分支上进行开发，完成后再将它们合并到主分支上。
>
> 创建一个叫做“feature_x”的分支，并切换过去：
>
> ```git checkout -b feature_x```
