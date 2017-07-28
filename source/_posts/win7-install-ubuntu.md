title: Windows 7下硬盘安装 ubuntu 16.04 LTS
date: 2017-7-27
tags:
- Win7
- ubuntu
- 安装

---

## 准备材料

ubuntu 光盘映像文件 ubuntu-16.04.2-desktop-amd64.iso ， [下载地址](http://releases.ubuntu.com/16.04/)
EasyBCD  [下载地址](https://www.techspot.com/downloads/3112-easybcd.html)

## 安装步骤

- 使用解压软件，打开ubuntu 光盘映像文件, 将以下文件解压到C：盘：
  - `.disk`目录
  - “casper”文件夹下的“vmlinuz.efi”和“initrd.lz”
- 下载并安装EasyBCD软件
  - 配置Linux开机引导，如下操作：
    ![](http://img.blog.csdn.net/20160708005425948)
  - 写入如下配置：
```
title Install Ubuntu 16.04

root (hd0,4)

kernel (hd0,4)/vmlinuz.efi boot=casper iso-scan/filename=/ubuntu-16.04.2-desktop-amd64.iso ro quiet splash locale=zh_CN.UTF-8

initrd (hd0,4)/initrd.lz

```

> 特别注意:
> 1、ubuntu-16.04.2-desktop-amd64.iso 是你的iso的名字，别写成我的了，这个要改成你的。
> 2、 安装64位Ubuntu-16.04时上面的第二行代码的vmkinuz.efi 是加了.efi 的，但是32的 Ubuntu 是不用加的。
> 3、 hd0 表示第一块硬盘，对于笔记本来说大部分只有一块硬盘吧，如果有第二块就是hd1 ,同理，root(hd0,0)中的‘0’ 表示第一个分区，但是现在的win7系统下C盘的盘符不是'0' 而是‘1’。第一块分区作系统保留用，我的G盘的盘符是4。

## 安装Ubuntu

重启开机，会有开机选项“Install Ubuntu 16.04”，选择它进入安装界面。

注意一点，首先开启终端，使用如下命令：
```
sudo umount -l /isodevice
```

然后，打开桌面上的安装Ubuntu图标，进行安装。

## 更新源

- 备份文件 `/etc/apt/source.list`
- 修改上面文件，加入如下 16.04 源：
```
deb-src http://archive.ubuntu.com/ubuntu xenial main restricted #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb http://mirrors.aliyun.com/ubuntu/ xenial multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse #Added by software-properties
deb http://archive.canonical.com/ubuntu xenial partner
deb-src http://archive.canonical.com/ubuntu xenial partner
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-security multiverse
```
- 使用命令更新`sudo apt-get update`
