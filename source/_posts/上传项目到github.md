---
title: 上传项目到github
date: 2019-08-16 00:19:27
tags: git
---

## 把个人的项目上传到github仓库

#### 一、注册github账户：

*GitHub官网网址：<https://github.com/>*

注册过程比较简单，这里不详细介绍了～

#### 二、设置SSHKey

##### 本地的Git仓库和GitHub网站仓库之间的传输是通过SSH加密的，所以要设置SSH KEY.

```bash
$ ssh-keygen -t rsa -C "youremail@email.com" 
# "youremail@email.com"  是你注册github的邮箱地址
# 后面基本是一直回车， 但是有一个地方会让你输入密码，这是你sshkey的密码
```

##### 这里是让你输入密码：【输入两次确保密码设置正确】

{% asset_img 上传项目到github1.png 这里输入密码 %}

##### SSHKey创建成功后，会在你的用户目录的.ssh文件夹下生成`id_rsa`**和**`id_rsa.pub`文件。

##### 这是SSH Key的秘钥对，其中`id_rsa`是私钥，不能泄露，`id_rsa.pub`是公钥，可以告诉其他人。

```bash
$ vim id_rsa.pub
#复制文件内的内容
```

##### 登录GitHub，点击右上角头像，Settings -> Personal settings -> SSH and GPG keys。在SSH Keys标签右方点击New SSH Key。 这里会弹出两个文本框，其中的Title，读者可以随意命名。另一个Key文本框，就是粘贴刚才复制的内容。

#### 三、上传内容

```bash
$ git --version #检查是否安装了git
# 如果没安装，就先安装 ： sudo apt-get install git
$ cd /你的项目文件根目录
$ git init #初始化命令，这个命令可以把当前目录变成git可以管理的仓库。
$ git add file #添加文件到暂存区,file为文件名
$ git add . #把文件夹所有文件都添加
$ git status #该指令可以查看当前的分支以及添加文件的情况。
$ git commit -m "first commit"   # -m后的内容是添加的描述，提交新版本
```

使用push命令上传文件：

```bash
$ git push git@github.com:wooyee-ldq/chat-IM.git master
#仓库是第一次进行push时使用该命令，如果不是第一次则使用下面命令：
$ git push origin 分支名
# git@github.com:wooyee-ldq/chat-IM.git 这个是你的仓库download那里的ssh地址
```

```bash
$ git remote add origin git@github.com:wooyee-ldq/chat-IM.git
# 更改远程仓库名称为：origin  ，默认远程仓库名就是 origin
$ git remote rm origin #删除远程仓库
```

##### 遇到错误：

```bash
To github.com:wooyee-ldq/chat-IM.git
 ! [rejected]        master -> master (non-fast-forward)
error: 无法推送一些引用到 'git@github.com:wooyee-ldq/chat-IM.git'
提示：更新被拒绝，因为您当前分支的最新提交落后于其对应的远程分支。
提示：再次推送前，先与远程变更合并（如 'git pull ...'）。详见
提示：'git push --help' 中的 'Note about fast-forwards' 小节。
```

##### 一个解决办法：

```bash
$ git pull --rebase chatim master
来自 github.com:wooyee-ldq/chat-IM
 * branch            master     -> FETCH_HEAD
首先，回退分支以便在上面重放您的工作...
应用：first commit for blog_ejs
应用：add readme file
使用索引来重建一个（三方合并的）基础目录树...
回落到基础版本上打补丁及进行三方合并...
没有变更 —— 补丁已经应用过。
```

##### 然后再次上传成功了：

```bash
$ git push origin  master
对象计数中: 2817, 完成.
Delta compression using up to 4 threads.
压缩对象中: 100% (2476/2476), 完成.
写入对象中: 100% (2817/2817), 3.57 MiB | 1.30 MiB/s, 完成.
Total 2817 (delta 482), reused 0 (delta 0)
remote: Resolving deltas: 100% (482/482), done.
To github.com:wooyee-ldq/chat-IM.git
   9b5ab20..0d9c6a5  master -> master
```

> push结束后，在GitHub端的对应仓库上刷新一下，会看到你的项目文件，说明项目内容已经上传成功~
>
> > 到此，上传项目到github完成...



