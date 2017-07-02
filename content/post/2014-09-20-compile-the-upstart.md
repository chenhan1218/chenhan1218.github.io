---
title: '編譯 Upstart 1.13.2'
date: "2014-09-20 04:55:00"
comments: true
categories: 
---
編譯 Upstart 1.13.2：
```
sudo apt-get install libnih-dbus-dev libjson-c-dev
cd upstart 1.13.2/
./configure
make
```

編譯完成後，會得到以下的執行檔，這樣就得到一組 userspace 上開關機所需要的 utility 了
```
init/init
util/initctl
util/reboot
util/runlevel
shutdown
telinit
upstart-event-bridge
upstart--bridge
upstart-dbus-bridge
upstart-socket-bridge
upstart-local-bridge
```