---
title: Linux主要目录
date: 2019-09-01 16:42:50
tags: linux
---

## Linux目录结构和window不一样，这里记录一下linux的主要目录和目录的存放文件类型

### linux系统的文件管理是没有盘符这个概念的，所有文件都在`/`目录下

#### 再根目录下的都是文件夹，每个文件存放的文件类型不一样：

- / ：系统根目录，所有文件都从这里开始
- /bin、/usr/bin ：存放可执行的二进制文件，例如常用的linux命令：ls、cat、tar、mv等
- /boot ：存放linux启动文件，例如grub系统引导文件
- /dev ：存放系统的设备文件，linux下设备是以文件形式挂载
- /etc ：系统配置文件的存放目录，一般不在该目录存放二进制文件，重要的配置文件：
  - /etc/inittab
  - /etc/fstab
  - /etc/init.d
  - /etc/X11
  - /etc/sysconfig
  - /etc/xinetd.d

- /home ：系统默认的用户家目录，新建用户时，用户的文件夹会建立在/home下面
  - 使用 ~ 表示家目录
  - cd 或者cd ~可以切换到家目录

- /lib、/usr/lib、/usr/local/lib ：系统使用的函数库的目录，程序在执行过程中，需要调用一些额外的参数时需要函数库的协助
- /lost+fount ：系统异常产生错误时，会将一些遗失的片段放置于此目录下
- /mnt /media ：光盘默认挂载点，通常光盘挂载于 /mnt/cdrom 下，但是挂载点一般可以自己选择
- /opt ：给主机额外安装软件所摆放的目录
- /root ：系统管理员的root的家目录
- /proc ：此目录的数据都在内存中，如系统核心，外部设备，网络状态，由于数据都存放于内存中，所以不占用磁盘空间，比较重要的文件：
  - /proc/cpuinfo
  - /proc/interrupts
  - /proc/dma
  - /proc/ioports
  - /proc

- /sbin、/usr/sbin、/usr/local/sbin ：放置系统管理员使用的可执行命令
- /tmp ：一般用户或正在执行的程序临时存放文件的目录
- /usr ：应用程序存放目录：
  - /usr/bin：存放应用程序
  - /usr/share：存放共享数据
  - /usr/lib：存放不能直接运行的，却是许多程序运行所必需的一些函数库文件
  - /usr/local：存放软件升级包
  - /usr/share/doc：系统说明文件存放目录
  - /usr/share/man：程序说明文件存放目录

- /var ：放置系统执行过程中经常变化的文件：
  - /var/log：随时更改的日志文件
  - /var/spool/mail：邮件存放的目录
  - /var/run：程序或服务启动后，其 PID 存放在该目录下

---

