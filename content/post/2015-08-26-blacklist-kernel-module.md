---
title: 'Debugging system hang by blacklist kernel module'
date: "2015-08-26 06:54:00"
comments: true
categories: 
---
有時在機器上會遇到 system hang 的狀況，特別是在 enable 新硬體時。遇到這種情況，可以試著 blacklist 可疑的 kernel module

以 mwifiex_sdio 為例 
```
# Do not load the 'mwifiex_sdio' module on boot.
echo > /etc/modprobe.d/debug.conf <EOF
blacklist mwifiex_sdio
EOF
```
再重開機即可

如果這個 module 仍會被其它 module depends 而載入，可以再進一步的 blacklist
```
# Do not load the 'mwifiex_sdio' module on boot.
echo > /etc/modprobe.d/debug.conf <EOF
install mwifiex_sdio /bin/false
EOF
```

[Using files in /etc/modprobe.d/](https://wiki.archlinux.org/index.php/Kernel_modules#Using_files_in_.2Fetc.2Fmodprobe.d.2F_2)