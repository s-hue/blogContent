# Git自学教程

本教程记录了自己学习Git的相关知识和命令，记录留存。

## Git简介

[Git](https://git-scm.com)就是一种分布式的版本控制系统。所谓版本控制系统，就是记录你在创建、编辑到完成文档的系统，它可以让你委很方便地查看文档整个编辑历史，可以方便地回溯到版本记录的各个时间结点。

Git最早由Linus用C语言写的版本控制系统，用来管理Linux系统的源码。随着GitHub网站的上线上线，无数开源项目迁移到GitHub，加速了Git的普及。

分布式的概念相对于集中式而言的，集中式需要有一个中央服务器在存储管理版本，用户在每次使用之前从中央服务器获取最新的版本，修改完成后提交到中央服务器。分布式则是在每个用户的本地存在一个完整的版本库，不用担心联网不畅造成无法进行工作。为了方便多人协作，在实际的分布式版本控制系统，还是存在一台中央电脑用来协调多人之间不同的修改。

### Git的基本概念

工作区：电脑中能直接操作的文件及目录。

版本库：`.git`隐藏目录，一般不算做工作区。

暂存区：也就是`.git`目录下有`index`文件夹下的index文件。

Git的简单工作流程：首先在工作区中编辑调试文件内容，再使用`git add`命令将修改保存到缓存区中，最后使用`git commit`命令将缓存区的内容提交到版本库中。

### 安装Git

可以从Git的[下载地址](https://git-scm.com/download)中按不同的操作系统下载安装包。

安装完成后，需要设置用户的名称和电子邮箱来表明每个不同的用户。

```sh
# git config --global user.name "Your Name"
# git config --global user.email "youremail@example.com"
```

### 创建版本库

版本库就是一个目录，用来跟踪每个文件的创建、修改、删除等操作。

首先，定位到需要版本控制的目录创建版本库：

```sh
# git init
```

Git会在当前目录生成一个名为`.git`的隐藏文件夹，这就是用来跟踪管理版本库，新手最好不要尝试手动修改里面的文件。与此同时，Git会自动创建master分支，分支的概念会在后续说明。

然后，为版本库添加`.gitignore`文件来指定不需要进行版本管理的文件（比如那些在程序调试过程中生成的文件），具体的可以到GitHu上的[gitignore](https://github.com/github/gitignore)中下载对应程序语言的.gitignore模板，再按自己的需求进行修改。

*（如果是在已经存在内容的文件夹下来创建版本库，最好先将`.gitignore`文件修改好后再初始化版本库）*

### 添加和提交修改

当我们为项目增加了一些修改（即修改保存相关文件）后，就可以将这些修改添加到暂存区：

```sh
# git add <filename>
# git add .
```

第一个是添加某个具体的文件，后一个是添加当前目录下所有的文件和子目录。然后为这部分修改添加说明文字，方便后续查看修改的历史流程。

```sh
# git commit -m "description about the change"
```

这样就完成了一次版本的记录，当然这只是保存在你本地的版本库中，别人还无法查看这些修改。

### 查看版本库状态

使用`git status`查看上次提交后工作区中是否有修改。`git diff`可以显示出具体的改动是什么。

经过上述的步骤后，完全可以在本地实现项目的版本控制操作。

## Git高级操作

### 克隆仓库

克隆本地仓库:

```sh
# git clone /path/to/repository
```

克隆远端服务器的仓库：

```sh
# git clone username@host:/path/to/repository
```

### 远端仓库的操作

添加远端仓库：

```sh
# git remote add [remote-alias] [url]
```
`[remote-alias]`是为了方便记忆的简称，比如origin、mygithub等，`[url]`是远端仓库的地址。

remote的其它命令：

```sh
# git remote        // 列出所有的远端仓库
# git remote -v     // 远端仓库的网址
# git remote show <remote-alias>    // 远端仓库的详细信息
# git remote rm <remote-alias>      // 删除远端仓库
# git remote rename <old-remote-alias> <new-remote-alias> // 重命名远端仓库
```

提取远端仓库的更新到本地：

```sh
# git pull <remote-alias> <remote-branchname>:<local-branchname>
或下列三条命令（提取、切换分支、合并）
# git fetch <remote-alias> <remote-branchname>
# git checkout [local-branchname]
# git merge [remote-alias]/[remote-branchname]
```

在大部分的情况下，合并过程肯定会出现冲突（conflicts），需要手动修改冲突点后需要使用添加命令将修改的文件添加到暂存区，再提交到版本库当中，完成整个合并操作。

将分支的内容提交到远端仓库（`-u`表示在多个远端仓库中指定一个默认的仓库，平时可以不写）

```sh
# git push <-u> [remote-alias] <local-branchname>:<remote-branchname>
```

建立本地分支与远端仓库分支的追踪关系（tracking），`git clone`会自动将所有的本地分支与远端仓库的同名分支建立追踪关系，也可手动建立关系：

```sh
# git branch --set-upstream [local-branchnam] [remote-alias]/[remote-branchname]
```

### 分支操作

分支是Git中非常重要的概念，它可以将项目的特性开发完全独立出来，在测试通过后再合并到主要分支进行发布。

创建一个名为“featureA”的分支，并切换到该分支：

```sh
# git checkout -b featureA
等价于
# git branch featureA
# git checkout featureA
```

切换到不同的分支（比如master分支）：

```sh
# git checkout master
```

合并分支“featureA”到当前分支：

```sh
# git merge featureA
```

删除分支：

```sh
# git branch -d featureA
```

不带参数的分支命令`git branch`用来查看当前所有的分支，当前的所在的分支名前面有`*`来标示。

### 查看版本库的历史记录

基本的命令：

```sh
# git log
```

其它特定的命令：

```sh
# git log --author=alpha        // 只看alpha的提交记录
# git log --pretty=oneline      // 压缩每条记录只显示一行
# git log --graph --oneline --decorate --all    // 树形结构展示所有分支
# git log --name-status         // 查看改变的文件
# git log --help                // 查看帮助文档
```

### 替换本地改动

万一操作失误，可用命令替换本地改动，它将使文件`filename`退回到最近一次`git commit`或者`git add`时的状态。**注意不要漏掉`--`。**

```sh
# git checkout -- <filename>
```


### 取消之前缓存的内容

```sh
# git reset HEAD <-- filename>
```

后面跟`filename`表示只取消某个文件的缓存。

### 版本库文件操作

将条目`filename`从缓存区中移除：

```sh
# git rm filename           // 从缓存区和工作目录中删除文件
# git rm --cached filename  // 只从缓存区删除文件
```

移动或重命名一个文件：

```sh
# git mv sourcefile destinationfile
```

### 在U盘或网络硬盘上自建Git仓库

1. 查看U盘或网络硬盘的挂载路径（以`//MYSHAREDISK`为例），再定位到仓库的存放的文件夹（以`//MYSHAREDISK/CodeGit/`为例）；

2. 新建仓库文件夹（以`firstGit.git`为例，记住文件夹的名称就是`firstGit.git`，有后缀），打开这个文件夹后，在该文件夹下使用命令来创建新的空仓库：

```sh
# git init --bare
```

3. 打开本地电脑上想要同步的项目（如果没有就创建一个新的文件夹），创建`.gitignore`文件来标明需要忽略的文件，再使用命令`git init`来初始化本地Git库；

4. 进行首次提交到本地仓库：

```sh
# git add .
# git commit -m "initialized"
```

5. 为U盘或网络硬盘上的自建Git仓库命名为`myusbgit`：

```sh
# git remote add myusbgit //MYSHAREDISK/CodeGit/firstGit.git
```

6. 将本地仓库push到`myusbgit`上：

```sh
# git push myusbgit master
```

## 参考链接

[git-简明指南](http://rogerdudler.github.io/git-guide/index.zh.html)

[Git reference](https://git-scm.com/docs)

[Pro Git](https://git-scm.com/book/en/v2)

[gitignore templates](https://github.com/github/gitignore)

[Git教程](http://www.runoob.com/git/git-tutorial.html)