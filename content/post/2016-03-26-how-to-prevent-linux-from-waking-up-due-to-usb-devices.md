---
title: 'How to prevent Linux from waking up due to USB devices'
date: "2016-03-26 03:06:00"
comments: true
categories: 
---
最近換了一台工作機，但我發現在 Ubuntu 14.04.3 上，有時候會休眠失敗。
在失敗的時候，機器有 suspend 成功，但是過2秒後機器就會自動醒來。查看了 /var/log/kern.log, /var/log/syslog, /var/log/pm-suspend.log 沒有太異常的訊息。後來上網查了一下，這可能是有 BIOS 有問題或 device 不正常運作。

在 /proc/acpi/wakeup 中，列出了數種 wakeup event, 以下面的表來說，代表了機器開放了 EHC1, EHC2, PWRB, LID0 這幾種 wakeup event
```
RP06      S4    *disabled
PXSX      S4    *disabled
RP07      S4    *disabled
PXSX      S4    *disabled
EHC1      S0    *enabled   pci:0000:00:1d.0
EHC2      S4    *enabled  pci:0000:00:1a.0
PWRB      S4    *enabled   platform:PNP0C0C:00
LID0      S4    *enabled   platform:PNP0C0D:00
```
試著開關 wakeup trigger 來找出問題
``` bash
# ignore XHC device wakeup event
echo "XHC" > /proc/acpi/wakeup
# try suspend, still failed

# ignore EHC1 device wakeup event
echo "EHC1" > /proc/acpi/wakeup
# try suspend, still failed

# ignore EHC1 device wakeup event
echo "EHC2" > /proc/acpi/wakeup
# try suspend. Bingo!! It suspend successfully!
```
發現只要關閉 EHC2 wakeup trigger, 機器就能正常 suspend。可以放罝一個 upstart script，讓每次開機時，都自動關閉 EHC2 wakeup trigger
```
# /etc/init/disable-EHC2.conf
start on started dbus
stop on stopping dbus

script
   sudo -u root sh -c "echo 'EHC2' > /proc/acpi/wakeup"
end script
```

Ref:
- [Ubuntu 14.04 wake up immediately after suspend - Ask Ubuntu](http://askubuntu.com/questions/479254/ubuntu-14-04-wake-up-immediately-after-suspend)
- [UnderstandingSuspend - Ubuntu Wiki](https://wiki.ubuntu.com/UnderstandingSuspend)
- [Power management/Suspend and hibernate - ArchWiki](https://wiki.archlinux.org/index.php/Power_management/Suspend_and_hibernate#Instantaneous_wakeups_from_suspend)
- [acpitool(1) - Linux man page](http://linux.die.net/man/1/acpitool)
- [Best practice to debug Linux* suspend/hibernate issues | 01.org](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues)