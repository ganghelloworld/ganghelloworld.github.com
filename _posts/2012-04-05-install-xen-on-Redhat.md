---
layout: post
title: "在Redhat上安装Xen"
description: "重点注意小版本一致问题"
category: software install
tags: [Xen, Redhat, linux, kernel]
---
{% include JB/setup %}
> RedHat 相信大家熟知，Xen我也就不介绍了，我也是才开始接触。

下面介绍一下简单的安装步骤和遇到的问题。

## 一。配置好yum源

## 二。用yum install XX, 安装kernel-xen和xen-libs，一般在安装镜像里有相应的包，若没有，下载rpm包即可。此次安装用到的包为：

1.  kernel-xen-2.6.18-274.el5.i686.rpm
2.  kernel-xen-devel-2.6.18-274.el5.i686.rpm
3.  xen-libs-3.0.3-132.el5.i386.rpm

## 三。修改grub.conf中的default，让其从带有xen的内核启动

## 四。reboot，重启系统

## 五。下载xen工具的rpm包，以及所需要的其他工具包，通过命令rpm -ivh安装

### xen包有:

	1.  xen-3.0.3-132.el5.i386.rpm
	2.  xen-devel-3.0.3-132.el5.i386.rpm

### 所依赖的包有：

	1.  gnome-applet-vm-0.1.2-1.el5.i386.rpm
	2.  libvirt-devel-0.1.8-15.el5.i386.rpm
	3.  python-virtinst-0.99.0-2.el5.noarch.rpm
	4.  libvirt-0.1.8-15.el5.i386.rpm
	5.  libvirt-python-0.1.8-15.el5.i386.rpm
	6.  virt-manager-0.2.6-7.el5.i386.rpm
	7.  Virtualization-en-US-5.0.0-7.noarch.rpm
	8.  Virtualization-zh-CN-5.0.0-7.noarch.rpm

## 六。这里要特别注意，xen-libs-3.0.3-132.el5.i386.rpm包中的版本号要和xen-3.0.3-132.el5.i386.rpm，xen-devel-3.0.3-132.el5.i386.rpm中的版本号**绝对保持一致**，也就是说3.0.3-132.e15.i386这些数字及字母是一个都不能差的，否则会引起的问题有：

	1.  在图形界面启动xen virt manager回出现对话框显示vefrify that:Local host xen kernel booted, xend started，大概就是这些信息，准确的不记得了。
	2.  在字符界面运行xm list命令时打印，couldn't find file, xend is running 的信息
	3.  在/var/log/xen/xend.log 输出ERROR (SrvDaemon:297) Exception starting xend ((13, 'Permission denied'))这样的信息。

## 七.所以，请一定确保版本的一致。 其中在找xen相关的rpm包不是很好找，贴出几个源供参考

	1.  http://www.mars-china.com.cn/redhat/As5.5_32bit/as55/ 下面的Server及VT目录
	2.  http://ftp.sjtu.edu.cn/centos/5.6/cr/i386/RPMS/

安装过程再就没什么问题了。
