# 1、简介

Git 是目前世界上最先进的分布式版本控制系统，它是 Linux 之父花费 2 周时间用 C 语言开发的。

什么是版本控制系统？

它用来记录对一个文件的修改详情，Git 记录了的修改，而不是文件。

# 2、Git 的命令

## 管理仓库

### 创建版本库

`git init`

### 把文件添加到缓冲区

`git add <filename>`

### 把文件添加到版本库

`git commit -m "<discribe message>"`

### 查看版本库状态

`git status`

### 查看版本库的历史记录

`git log`

`git log --pretty=online`

### 回退到上一个版本

`git reset --hard HEAD^`

### 回退到上上个版本

`git reset --hard HEAD^^`

### 回退到之前的 100 个版本

`git reset --hard HEAD~100`

### 恢复到回退之前的版本

`git reset --hard <版本的 commit id>`

`git reflog` 

可以找到 commit id，然后用 `git reset --hard <版本 commit id>`

### 工作区和暂存区

工作区就是电脑里能看到的文件夹，在某个目录下通过 `git init ` 创建版本库，这个目录就是工作区。

工作区里的一个隐藏的目录 `.git` 是真正的版本库。

`.git` 中有 `stage/index` 叫做暂存区，有 Git 自动创建的第一个分支 `master`，有指向 `master` 的指针 `HEAD`

`git add <filename>`：将工作区文件的修改添加到暂存区

`git commit -m "<discribe message>"`：将暂存区文件的修改提交到版本库

### 工作区和版本库最新版的区别

`git diff HEAD -- <filename>`

### 撤销修改

`git checkout -- <filename>`

如果文件没有 add，则撤销到文件修改之前的样子，即回到最近一次 commit 的状态

如果文件已经 add，则撤销到文件添加到暂存区之后的样子，即回到最近一次 add 的状态

如果文件没有 add，修改之后做了 add，则可以通过 `git reset HEAD <filename>` 回退到工作区，然后通过 `git checkout --<filename>` 恢复到最近一次 commit 的状态

### 删除

`git rm <filename>`

确实要删除

`git commit -m "<discribe message>"`

想恢复

`git checkout -- <filename>`

`git checkout` 其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”

## 远程仓库

### 密钥和公钥

` ssh-keygen -t rsa -C "youremail@example.com"`

在` .ssh` 目录的 `id_rsa` 是密钥，`id_rsa.pub` 是公钥

将公钥添加到 `github` 账号上的 `SSH Keys` 中。这样本地版本库和远程仓库就连接了。

### 本地库和远程库同步（现有本地库后有远程库）

本地已经有一个本地仓库。

1. 在 `github` 上创建一个 `repository`

2. 将已有的本地库与之关联

   `git remote add origin git@github.com:newCoderGT/repositoryName.git`

3. 将本地库的所有内容推送到远程库

   `git push -u origin master`

   实际上是把当前分支 `master` 推送到远程库。

   远程库开始是空的，第一次推送使用 `-u`，Git会把本地的 `master` 分支内容推送的远程新的 `master` 分支，还会把本地的 `master` 分支和远程的 `master`分支关联起来，在以后的推送或者拉取时就可以简化命令

4. 只要本地作了提交，就可以通过命令推送到远程库

   `git push origin master`

### 先创建远程库，然后克隆到本地（开发中的模式）

本地还没有一个本地仓库。

1. 在 `github` 上创建一个 `repository` （勾选 Initialize this repository with a README）

2. 将远程库克隆到本地

   `git clone git@github.com:newCoderGT/repositoryName.git`

3. 只要本地做了提交，就可以通过命令推送到远程库

   `git push `