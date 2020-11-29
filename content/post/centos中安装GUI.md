---
title: "Centos中安装GUI"
date: 2020-11-29T21:51:13+08:00
draft: false
toc: true
---

[toc]
# CentOS中安装GUI界面

## 关于vnc模式登陆报错
> 这个报错是密码错误，需要先输入账户名（默认是root），在输入密码（密码默认不显示），才能进入系统

## (1)安装GNOME 
```
yum groupinstall "GNOME Desktop" "Graphical Administration Tools" -y
```
卸载GNOME

```
yum groupremove "GNOME Desktop"
```

- Centos7 yum groupinstall 报错的解决办法
```
Maybe run: yum groups mark install (see man yum)
No packages in any requested group available to install or update
```
解决：
```
yum groupinstall "Office Suite and Productivity" --setopt=group_package_types=mandatory,default,optional

```

- xauth:  file /root/.serverauth.21702 does not exist
```
yum update
yum groupinstall "X Window System"
yum groupinstall "Desktop"
```
### 查看yum安装的清单
yum grouplist



## (2)startx 启动图形界面

我们可以通过命令 startx 进入图形界面，第一次进入会比较慢，请耐心等待。

modeset(0): Initializing kms color map for depth 16, 6 bpc

我的是腾讯云服务器，只需要切换登录服务器的方式（用VNC登录方式登录服务器），其他的方式登录默认是命令行界面

## (3)系统切换形式

系统启动默认还是命令行页面的，需要我们进行切换。如果想要使系统启动即为图形化窗口，需要执行下面的命令

ln -sf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target

### 获取默认target
systemctl get-default //获取当前的默认target

# 阿里云的ecs服务器中CentOS安装图形化界面-CentOS8系统

## 安装图形界面
### 使用以下命令安装图形桌面的软件包。
```
# centos8
yum groupinstall "Server with GUI" -y 

# centos7
yum groupinstall "MATE Desktop" -y 
yum groupinstall "GNOME Desktop" "Graphical Administration Tools" -y
yum groupinstall "X Window System"

```

### 使用以下命令设置图形模式为默认模式启动。
```
# centos8
systemctl set-default graphical

# centos7
systemctl set-default graphical.target

结果
Removed symlink /etc/systemd/system/default.target.
Created symlink from /etc/systemd/system/default.target to /usr/lib/systemd/system/graphical.target.

systemctl set-default multi-user.target  //设置成命令模式
systemctl set-default graphical.target  //设置成图形模式


```
### 使用以下命令重启，重启后即可通过阿里云网页控制台上的VNC连接看到图形界面。
```
reboot
```


## 安装VNC Server

### 使用以下命令安装相关软件包。
```
yum install tigervnc-server tigervnc-server-module -y
```
### 使用以下命令设置vnc密码。
```
vncpasswd
```
### 使用以下命令启动VNC Server。
```
vncserver :1
```
说明：:1表示用6001端口，注意安全组记得放行端口。

### 232vnc密码
```
hmxMD3
```

> 如果你的xshell是设置隧道关联xmanager，能展示图形桌面的话，说明ECS设置没问题，可在ECS管理控制台的管理终端下按Ctrl+Alt+F1，进入图形界面。


> 图形化界面默认只能VNC方式连接，也可以搭配VNC server服务本地通过VNC viewer工具进行连接，具体VNC server服务配置方式可以外站搜索看下

## tcp测试ip的某个端口是否开启

tcping 120.78.237.232 6001

netstat -anplt | grep 6001

## 当starx 进入到图形化界面后，右键：open in terminal 失效问题
```
yum -y install nautilus-open-terminal

reboot
```