---
title: 使用hexo搭建个人博客并部署到github
date: 2019-07-30 23:06:48
tags: Hexo
---

## 使用[Hexo](<https://hexo.io/zh-cn/docs/>)博客框架搭建自己的个人博客并不需要学会nodejs，html，css等内容。其中nodejs只是作为hexo框架的运行环境。

## *下面是各个步骤：*

## 一.安装node.js

#### **Linux:**

#### 1. 官网下载[node.js](<https://nodejs.org/en/>).tar.xz安装包；这里有我之前下载的[安装包](https://pan.baidu.com/s/1zj9yjueD9IR9hTg6HttFJg)，密码: 7flj

#### 2.把安装包移动或复制到你想要安装的目录下

#### 3.Ctrl+Alt+t 或者 鼠标右键 '打开终端'，下面是在终端的代码：

```bash
cd 你的安装包所在目录
xz -d nodejs.tar.xz
tar -xvf nodejs.tar
```

#### 4.上面的代码是解压安装包，解压好之后需要配置环境变量：

```bash
vim /etc/profile   #打开配置文件，添加以下内容：

#set path for nodejs
export NODE_HOME=/nodejs的安装目录
export PATH=$NODE_HOME/bin:$PATH
```

#### 5.使环境变量生效

```bash
source /etc/profile    #使得环境变量生效
```

#### 6.检查nodejs是否安装成功

```bash
#检查nodejs是否安装成功：
$ node --version	#检查nodejs的版本
$ node --help	#显示nodejs的帮助信息
$ npm --version	#检查npm的版本
$ npm --help	#显示npm的帮助信息
```

#### **Window:**

#### 1.官网下载[node.js](<https://nodejs.org/en/>)的window安装包。

#### 2.双击nodejs安装包，选择安装位置等，勾选添加到path。

#### 3.window的安装比较简单，这里不在详细叙述。

#### 4.安装完成后，在运行窗口（win+R 打开）输入 cmd ，打开命令行窗口，输入命令检查nodejs的安装（直接在开始菜单右键打开power shell也可以）：

```bash
> node --version	#检查nodejs的版本
> npm --version		#检查npm的版本
```

## 二.注册Github和创建存储库

#### 1.[Github官网](https://github.com)注册账户，如果已注册自行忽略。

#### 2.登录账户，创建一个： ***你的用户名.github.io*** 的存储库。

{% asset_img github1.png%}

{% asset_img github2.png%}

## 三.安装Git和配置Github

#### **Linux:**（这里是官方Linux各种版本的[安装](https://git-scm.com/download/linux)，我这里是基于ubuntu）

#### 1.打开终端，输入：

```bash
$ sudo apt-get update
$ sudo apt-get install git
```

#### 2.配置git的个人信息和配置SSH

```bash
$ git config --global user.name "你的github用户名"
$ git config --global user.email "你注册的邮箱地址"
$ ssh-keygen -t rsa -C "你注册的邮箱地址"	#生成SSH
$ vim ~/.ssh/id_rsa.pub		#打开生成的文件，复制里面的所有内容
```

##### 打开github,点击右上⻆自己的头像,点击settings,再点击SSH,之后添加new ssh key,最后把复制的信息都粘贴进去,title可以写，然后测试是否成功配置：

```bash
$ ssh -T git@github.com
#显示下面内容就是成功了
Hi! You ve successfully authenticated, but GitHub does not provide shell access.
```

#### **window:**

#### 1.直接官网下载[安装包](https://git-scm.com/download/win)，双击运行安装。

#### 2.打开Git Bash命令窗口

#### 3.配置git的方法和上面linux的相似，建议读者可以参考<https://blog.csdn.net/robertzhouxh/article/details/9887063>

## 四.安装Hexo和使用Hexo创建博客项目

#### **Linux&Window:**

#### 1.安装hexo，打开终端【window打开cmd命令行窗口或power shell窗口】，输入：

```bash
$ npm install hexo -g
```

#### 2.使用hexo创建你的博客项目，终端输入：

```bash
$ hexo init blog	#这里blog是你要创建的项目根目录
```

#### 3.安装 hexo-deployer-git

```bash
$ cd /../blog	#进入你的博客项目根目录
$ npm install hexo-deployer-git -save
```

#### 4.创建文章(在你的博客项目根目录)

```bash
$ hexo new "newPost"
```

#### 5.生成静态文件

```bash
$ hexo generate
```

#### 6.此时，在部署之前，读者可以输入以下命令来在本地电脑运行服务：

```bash
$ hexo server
#然后浏览器打开localhost:3000就可以预览自己的博客
```

#### 7.部署前还要配置一下_config.yml文件：

```bash
#该文件是前面生成的项目根目录下的_config.yml文件：
$ cd blog #项目根目录
$ vim _config.yml
#打开文件后，添加以下内容：
	# Deployment
	## Docs: https://hexo.io/docs/deployment.html
	deploy:
 	 	type: git
 		repo: git@github.com:wooyee-ldq/wooyee-ldq.github.io.git	#这里要填你github项目download那里的ssh地址
 		branch: master
```

#### 8.配置好_config.yml后，部署博客到github

```bash
$ hexo deploy
```

#### 9.浏览器输入地址：***你的用户名.github.io*** 便可以浏览你的博客了，hexo会有个hello world 的默认文章，那里有一些hexo操作的教程和官网教程地址。 

---

> > 到此，你创建了一个博客并部署到了github，还不现在就写篇文章发表到博客！！！关于如何编写文章(你的项目根目录/source/_post文件夹下面的md文件)，读者可以参考[markdown语法编写博客文章](https://wooyee-ldq.github.io/2019/07/30/markdown语法编写博客文章/)！！！







