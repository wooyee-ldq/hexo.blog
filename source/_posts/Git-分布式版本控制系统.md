---
title: Git--分布式版本控制系统
date: 2019-08-18 09:53:29
tags: git
---

### Git的两大特点：

* 版本控制：可以解决多人同时开发代码的问题，也可以解决找回历史代码的问题
* 分布式：Git是分布式版本控制系统，同一个Git仓库，可以分不到不同的电脑上。其中有一台作为服务器，24小时开机，其他人都是从这个台服务器仓库克隆一份完整的版本到自己的电脑上，并且把各自的提交推送到服务器仓库里，也可以从拉取别人的提交。自己可以搭建这个服务器，也可以直接使用github。

---

#### 一、Git的基本操作：

* 安装git

```bash
sudo apt-get install git
git --version  # 显示git的版本，可以测试是否安装成功
```

* 使用 git init 初始化仓库 

```bash
mkdir floder  # 创建一个文件夹，这个文件夹就是 工作区
cd floder  # 进入创建的文件夹
git init  # 初始化，为该文件夹创建git版本仓库
# 初始化仓库后，会生成一个 .git的隐藏文件夹，这个就是git的版本仓库，在版本仓库中有一个 暂存区【stage】
ls -lha
总用量 12K
drwxr-xr-x  3 wooyee wooyee 4.0K 8月  29 10:27 .
drwxrwxrwx 14 wooyee wooyee 4.0K 8月  27 21:18 ..
drwxr-xr-x  8 wooyee wooyee 4.0K 8月  29 10:27 .git
```

* 创建一个版本

```bash
git add file_name  # 添加修改到暂存区
git commit -m "版本描述信息"  # 创建版本记录，在创建版本记录前，可以多次添加修改到暂存区
# 注意：git commit -m "版本描述信息" 只是把暂存区的修改创建新版本，如果没有git add 的修改是无法创建新版本的
```

* 查看版本记录

```bash
git log

commit 4ab9d751962be7b9e6f658526ef92f7383926019 (HEAD -> master)
Author: wooyee-ldq <2632230944@qq.com>
Date:   Sun Sep 29 10:18:58 2019 +0800

    版本2

commit d6f250ffbc954465d9ac17ecdd70b913c6253b16  # 版本号
Author: wooyee-ldq <2632230944@qq.com>
Date:   Sun Sep 29 10:17:16 2019 +0800

    版本1
```

* 版本回退：在git中，HEAD指针指向最新的版本，使用HEAD^或者HEAD～1表示最新版本的前一个版本，同理，HEAD^^或者HEAD～2表示最新版本的前两个版本

```bash
git reset --hard HEAD^  # 回退到上一个版本
git reset --hard 版本号  # 回退到某个版本，回退版本时，原版本并不删除
```

* 查看操作记录

```bash
git reflog

d6f250f (HEAD -> master) HEAD@{0}: reset: moving to HEAD^
4ab9d75 HEAD@{1}: commit: 版本2  # 最前面的号码就是版本的序列号，
# 可以通过这个命令查看过去版本的序列号，在使用 git reset --hard 版本号 回到某个版本
d6f250f (HEAD -> master) HEAD@{2}: commit (initial): 版本1
```

* 查看工作状态

```bash
git status

位于分支 master
未跟踪的文件:
  （使用 "git add <文件>..." 以包含要提交的内容）

	code2.txt

提交为空，但是存在尚未跟踪的文件（使用 "git add" 建立跟踪）
```

* 撤销修改

```bash
# 如果修改了文件，在git add 之前，你想撤销之前的修改，使用下面命令：
git checkout -- 文件名  # 丢弃改动

# 如果修改了文件，并且已经使用 git add 添加到暂存区，但是还没git commit 创建新版本，要撤销文件的修改：
git reset HEAD 文件名 ...  # 取消暂存
git checkout -- 文件名  # 丢弃改动

# 如果修改的文件已经创建了新的版本，直接使用上面的版本回退就可以回到原来的版本了
```

* 文件对比：

```bash
# 比较工作区中的文件和某个版本有什么不同【比较的是同一个文件】：
git diff HEAD -- 文件名  # 这里的HEAD指的是版本，比如 HEAD^ 也可以

# 比较不同版本中同一个文件的不同：
git diff HEAD HEAD^ -- file_name  # 这里比较的是最新版本和前一个版本的 file_name这个文件的不同
```

* 删除文件

```bash
# 在工作区删除文件也是一种修改，如果在工作区删除了文件，可以使用 git checkout -- 文件名恢复文件
# 如果确实要删除文件，要使用 git rm 文件名来添加修改到暂存区，再使用git cmmit来保存新版本
# 在使用了 git rm 添加到暂存区后，还是可以使用git reset HEAD 文件名 来取消暂存，然后git checkout 恢复文件
# 注意：如果你在删除了文件后，保存了新的版本，如果要找回原来的文件只能回退到文件还没有被删除的版本
# 注意：如果新建的文件，还没有添加到过暂存区，如果删除了是不可以使用git 的管理来恢复文件的
```

---

#### 二、Git分支管理

* 查看当前有几个分支，并且在哪个分支下工作

```bash
git branch
```

* 创建新分支

```bash
# 创建新分支
git branch 分支名
# 切换分支
git checkout 分支名
# 创建一个分支，并切换到该分支
git checkout -b dev  # 这里dev是创建的新分支名
git branch
* dev  # *表示当前所在分支
  master
```

* 切换分支

```bash
git checkout 分支名
```

* 合并分支

```bash
# 一般在主分支合并其他分支
git checkout master  # 切换到主分支
git merge 分支名  # 合并分支到当前分支
```

* 删除分支

```bash
# 注意：一般在把分支合并之后再删除分支
git branch -d 分支名
```

* 解决分支合并冲突

```bash
# 合并分支的时候，可能会发生合并冲突
# 原因是：你在合并该分支前，修改了某个文件并创建了新的版本，但是在此之前，
# 你要合并的这个分支也修改了这个文件并且也创建了新的提交版本，
# 因此，需要手动打开发生冲突的文件，这时git会标示出发生冲突的内容，
# 你可以根据需要，手动修改和解决冲突，并创建新版本提交
# 这样实际上版本已经合并保存提交了，这时可以删除分支了
```

* 没有冲突的非快速合并

```bash
# 在合并分支时，没有发生冲突，但是此次合并不是快速合并，而是其他策略
# 原因是：你在其他分支新建了一个文件并提交，然后切换回主分支时，修改了某个文件并提交
# 在合并分支时，git会把分支新建的文件合并过来，然后进行一次提交，这时就不是快速提交了
# 因此，在此次合并时会自动提交一次，就需要我们输入提交的描述
# 输入描述后，ctrl+x退出 ，这样就合并好了
git log --pretty=oneline --graph  # 查看提交记录，会发现多了一次提交
```

* 禁用快速合并的合并操作【git merge 默认是快速合并】

```bash
git merge --no-ff -m "提交描述" 分支名  # 禁用快速合并，会在合并后进行一次提交
```

* 保存工作现场

```bash
git stash  # 保存当前分支的工作现场
git stash list  # 显示保存的工作现场
git stash pop  # 回到保存的工作现场
```

* 拉取最新的版本

```bash
git fetch origin master:temp  # orgin是项目的拉取地址，
# master表示从项目的master分支拉取更新，temp表示创建temp分支并把拉取的更新放在temp分支中
git checkout master  # 切换到主分支master
git merge temp  # 把temp分支合并到master
```

强制推送本地库版本到远程库（用本地库的版本覆盖远程库）

```bash
git push -f origin master
# -f 强制推送，origin是远程库的地址，master是指定的远程分支
```

---

#### 三、GitHub的使用

* 从github克隆项目

```bash
git clone ssh/https的克隆地址  # 把项目克隆到本地
# 如果克隆出错，执行命令:
eval "$(ssh-agent -s)"
ssh-add
```

* 推送分支到github

```bash
git push origin 分支名  # 把该分支推送到github仓库
```

* 设置本地分支跟踪远程服务器分支

```bash
git branch --set-upstream-to=origin/远程分支名 本地分支名  # 设置本地分支跟踪远程服务器分支
git push  # 设置本地分支跟踪远程服务器分支后，使用该本地分支推送时，直接使用 git push 就可以
```

* 从远程分支拉取代码

```bash
git pull origin 分支名  # 从远程分支拉取代码
```

* 如果是自己把项目上传的推送

```bash
git add . #把文件夹所有文件都添加
git commit -m "first commit"  
git push git@github.com:wooyee-ldq/chat-IM.git master  # 这里push后面的地址是仓库的ssh地址
git remote add origin git@github.com:wooyee-ldq/chat-IM.git  # 设置远程仓库名 为 origin
git remote rm origin #删除远程仓库  
```

