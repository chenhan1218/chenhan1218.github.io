---
title: '使用 qemu (or KVM) 建立 debian VM'
date: "2014-10-30 00:14:00"
comments: true
categories: 
---
有很多工具可以用來建立 Virtual Machine ，例如 VirtualBox, VMware, LXC, Qemu, Qemu with KVM, Xen 等等。

[QEMU - Debian Wiki](https://wiki.debian.org/QEMU) 簡單的介紹了如何使用 Qemu 來運行虛擬環境

### 使用現有 Image
Debian developer Aurelien Jarno 提供了數個預先建立的 Image [https://people.debian.org/~aurel32/qemu/](https://people.debian.org/~aurel32/qemu/)，這邊我使用 amd64 的架構做示範幾種啟動虛擬環境的方式：

- 開啟 QEMU，預設使用 [SDL](https://www.libsdl.org/) 顯示 guest OS 的畫面
``` bash
qemu-system-x86_64 -hda debian_wheezy_amd64_standard.qcow2 -m 256
```

- 開啟 QEMU，使用 terminal 操作虛擬環境  (一般PC上開機約180秒)
``` bash
qemu-system-x86_64 -hda debian_wheezy_amd64_standard.qcow2 -m 256 -curses
```

- 開啟QEMU，並將 host OS port 5555 的封包轉送給 Guest OS 的 port 80
``` bash
qemu-system-x86_64 -hda debian_wheezy_amd64_standard.qcow2 -m 256 -curses -redir tcp:5555::80
```

- 開啟QEMU，並且開啟 kvm full virtualization support。如果 kernel，processor 有支援，將大大提昇虛擬環境運行速度。這項操作需 root 權限。 (一般PC上開機約30秒，可大大看出 -enable-kvm 的差異)
``` bash
qemu-system-x86_64 -hda debian_wheezy_amd64_standard.qcow2 -m 256 -curses -enable-kvm
```

特別注意的是我這邊沒有特別對網路做設定，根據 Documentation ，TCP, UDP可以運作，但ICMP 不會。我實際測試的結果確實是如此。(Note - if you are using the (default) SLiRP user networking, then ping (ICMP) will not work, though TCP and UDP will. Don't try to use ping to test your QEMU network configuration!)

### 自已建立 qemu image
- 我們也可以選擇自己使用 debootstrap 建立 debian base system。[debian.org - Installing Debian GNU/Linux from a Unix/Linux System](https://www.debian.org/releases/stable/amd64/apds03.html.en) 這篇文章提供了很好的教學，差別只在於我們的硬碟為一個虛擬硬碟。步驟：

1. 建立虛擬硬碟
``` bash
dd if=/dev/zero of=rootfs.img bs=1G count=2
```
2. 格式化虛擬硬碟為 ext4
``` bash
mkfs.ext4 rootfs.img
```
3. mount 虛擬硬碟 (需要 root 權限)
``` bash
mount -o loop rootfs.img /mnt
```
4. 執行 debootstrap (需要 root 權限)
``` bash
debootstrap --no-check-gpg --arch=amd64 wheezy /mnt/ http://debian.nctu.edu.tw/debian/
```
5. 查詢虛擬硬碟的 UUID，我這邊是"4cc6834a-df20-4cb3-ad55-79433346e000"
``` bash
blkid rootfs.img
```

> rootfs.img: UUID="4cc6834a-df20-4cb3-ad55-79433346e000" TYPE="ext4"

6. 填寫 /etc/fstab，讓虛擬機開機時就會 mount 虛擬硬碟
``` bash
echo "UUID=4cc6834a-df20-4cb3-ad55-79433346e000 / ext4 0 1" >> /mnt/etc/fstab
```
7. chroot 進 /mnt，安裝 linux kernel，安裝並設定 grub bootloader。結束後退出 chroot 環境。(需root權限)
```
chroot /mnt
apt-get update
apt-get install -y linux-image-amd64
apt-get install -y grub-pc
grub-install /dev/hda
update-grub
exit
```
8. umount 虛擬硬碟 (需 root 權限)
``` bash
umount /mnt
```

至此，rootfs.img裡面就是一個完整的 debian OS 了。可以用前面所說的方法，以 qemu 開啟。也可以將這個虛擬硬碟轉換為 qcow2 格式，可以佔用較小空間(但虛擬作業系統跑起來的時候則需多花一些計算效能)。
```
qemu-img convert -f raw -O qcow2 rootfs.img mydebian.qcow2
```

Ref: 
- [QEMU - Debian Wiki](https://wiki.debian.org/QEMU)
- [QEMU - ArchWiki](https://wiki.archlinux.org/index.php/QEMU)
- [debian.org - Installing Debian GNU/Linux from a Unix/Linux System](https://www.debian.org/releases/stable/amd64/apds03.html.en)
- [QEMU/Networking](http://en.wikibooks.org/wiki/QEMU/Networking)
- [Creating a Debian Based QEMU Image](http://www.ziviani.net/2013/customized-debian-qemu)

Update:
Linaro 有提供 Debian Jessie 8.0 的 image: http://images.validation.linaro.org/kvm/jessie.img.gz