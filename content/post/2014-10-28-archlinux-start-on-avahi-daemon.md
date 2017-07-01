---
title: '在 Archlinux 上啟動Avahi-daemon'
date: "2014-10-28 02:38:00"
comments: true
categories: 
---
這篇回覆介紹了如何在 Archlinux 上使用 systemd 來開啟 avahi-daemon，使得區域網路內的電腦可以用 .local 來連線到其它電腦。

1. `pacman -S avahi nss-mdns` Installs the Avahi services daemon and the Multicast DNS resolver.
nano /etc/nsswitch.conf This file tells the C library how to obtain name-service information.
2. Change the line `hosts: files dns myhostname` to `hosts: files mdns_minimal [NOTFOUND=return] dns myhostname`, save and exit.
3. `systemctl start avahi-daemon` Starts the Avahi service manually since we're already booted.look for errors)
4. `systemctl enable avahi-daemon` Enables the Avahi service on boot.

[How do I get to use .local hostnames with Arch Linux?](http://unix.stackexchange.com/a/146025/89399)