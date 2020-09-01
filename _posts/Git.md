---
title: Git
date: 2020-08-30 22:22:38
tags:
---

# Git

## Git简介

* Git是一个开源的分布式版本控制系统;
* 所谓分布式，是指每个人的电脑上都有一个版本库（仓库），而每当要与别人合作的时候便把自己的版本库推送到模拟的“中央服务器”上，别人再从这个“中央服务器”中获得该版本库。


## Git安装及配置

* 在linux上可以通过`sudo apt-get git`来直接安装;在Windows上需要到[Git的官网下载](https://git-scm.com/downloads);而在Mac上的安装可以在命令行通过[homebrew](https://brew.sh/)安装，但实际上Mac的Xcode上集成了Git，安装Xcode的时候就已经安装好了Git。
* **配置用户名和用户邮箱**：
    ```shell
    git config --global user.name "yourname"
    git config --global user.email "youremail"
    ```
  * `--config`这个参数，代表你这台机器上的所有仓库都使用这个用户名和邮箱。

## 创建版本库(仓库)

* 版本库又名仓库，英文名repository，你可以简单理解成一个目录(文件夹），这个目录(目录的路径设置成英文避免出现问题）里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
* 仓库的初始化：进入当前目录下，打开“Git bash”,在终端输入`git init`,之后会在当前目录下生成一个`.git`文件目录，这是Git用来跟踪这个目录的文件，不能随意改动。
* 在当前目录下创建一个文件之后，需要将这个文件加入Git的暂存区中，此时使用`git add <filename> `（`git add .`可以将当前目录下的所有文件加入暂存区）
* 暂存区的文件需要加入Git的版本分支中，才算完成了整个文件的Git版本管理，此时使用`git commit -m "本次提交说明"`

## 时间轴上版本查看

### 分支状态查看

* 使用`git stastus`查看当前分支的状态，例如主分支下有多少分分支，以及暂存区多少文件待提交。

### 查看具体修改内容

* 使用`git diff  <filename>`可以查看具体的修改内容。

### 查看commit的历史记录

* 使用`git log`可以看到从最近到最远的所有commit记录，每个记录都会有commit的版本号id（一串乱七八糟的数字）,时间，作者以及commit时的描述。（此处就显得commit时一个合适的描述是多么的重要。）

### 版本回退（回退commit）

* Git中用HEAD来表示当前版本，HEAD^来表示上一个版本，HEAD^^来表示上上个版本，而至于像100次提交前的版本，则用HEAD~100来表示。
* 要回到某一个版本可以使用`git reset --hard HEAD^`或者`git reset --hard <版本号>`(版本号不用输完，指数前几位即可，Git会自动去寻找符号这部分版本号的commit)。

### 查看历史命令

* 使用`git reflog`可以查看历史命令。

###  撤销工作区的修改

* 使用`git checkout -- <filename>`可以将工作区的某文件恢复至上一次`git add`或者`git commit`时的状态。（注意，`--`和`<filename>之间有一个空格）。
* 总结： `git reset`是撤销版本库的修改（即.git文件中的版本信息）,`git checkout`是撤销对工作区文件的修改（即当前电脑上真实的文件，实际原理是从.git文件中的暂存区或者版本库中把以前的版本还原到工作区中。）
* 删除文件

* 工作区文件被删除后，会导致版本库和工作区中的文件不一致。为了使工作区与版本库一致，可以使用`gir rm <filename>`删除，在`git conmmit -m "删除描述"`将版本库中的文件也删除。当然，我们也可以用`git checkout --<filename>`恢复工作区中被误删的文件。

## 远程仓库

### 使用SSH与远程主机（GitHub）关联

* 前面说到使用Git与多人合作，需要使用一个类似“中央服务器”的东西，我们可以自己创建一个Git服务器来充当这个中央服务器，也可以直接使用GitHub来充当这个东西。
* 首先得使用SSH将本地机与GitHub关联起来，是两者之间能够安全的传输数据。

#### 创建本机的SSH秘钥

* 首先查看自己用户主目录中有没有一个`.ssh`的文件（我的电脑是在`C:\Users\12246\.ssh`）。如果没有则使用`ssh-keygen -t rsa -C "youremail@example.com"`创建。
* 在`.ssh`文件中会有`id_rsa`和`id_rsa.pub`两个文件，其中`id_rsa`是私钥，`id_rsa.pub`是公钥。

#### 将SSH公钥放入GitHub账号中

* 然后登录GitHub，在设置中找到设置SSH的地方，将本机上的公钥粘贴上去。这样就建立了本地机与GitHub的关联。只有将公钥放在GitHub上的电脑，才可以将文件上传到GitHub上。

### 创建远程仓库

* 首先在GitHub账号中创建一个仓库
* 之后将本地仓库与GitHub中的远程仓库关联起来。在本地仓库目录下打开Gitbash输入如下指令`$ git remote add origin git@github.com:<GitHub上的username》/<GitHub上的远程仓库名>.git`,便将当前目录下的本地仓库与远程的仓库关联起来了。在本地机上远程库的名字叫orgin，这是远程仓库的默认叫法，当然也可以叫其它名字，只需再关联远程仓库时将orgin改成其它名字即可。

### 推送到远程仓库

* 使用`git push -u orgin master`，将当前库中的当前分支推送到远程库的master中。（在这个命令中，参数 -u只有在第一次推送这个分支时才需要使用，若不是第一次，只需`git push orgin master`即可；其中，origin是远程仓库在本地的名字，而master是远程仓库的分支名。）

### 从远程库克隆

* 使用`git clone  git@github.com:<GitHub上的username》/<GitHub上的远程仓库名>.git`可以将远程的仓库克隆到本地（在哪个目录下打开gitbash使用的克隆，最后克隆下来的仓库就在哪个目录）。
* 除了使用`git@....`格式的地址外，还可以使用普通的http地址，只是传输速度相对较慢。

## 分支管理

