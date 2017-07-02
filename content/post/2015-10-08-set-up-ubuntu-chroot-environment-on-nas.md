---
title: '在 NAS 上架設 ubuntu chroot 環境'
date: "2015-10-08 15:47:00"
comments: true
categories: 
---
今天發現可以透過 Canonical Ltd. 的 [linuxcontainer](https://linuxcontainers.org) image 快速的在 NAS 上建立一個 chroot 環境。我的機器 cpu 是 armhf ，下面示範建立 Ubuntu 15.04 Vivid 的 chroot 環境。

步驟1：下載 Image，解開後進入 rootfs，並修改 nameserver
```
wget http://images.linuxcontainers.org/images/ubuntu/vivid/armhf/default/20151008_03:49/rootfs.tar.xz
mkdir rootfs
tar xvf rootfs.tar.xz -C rootfs
cd rootfs
echo "nameserver 8.8.8.8" > etc/resolv.conf
```
步驟2：mount 需要的 sysfs
```
mount -t proc proc proc/
mount -t sysfs sys sys/
mount -o bind /dev dev/
mount -t devpts pts dev/pts/
```
步驟3：chroot
```
chroot . su -l
```