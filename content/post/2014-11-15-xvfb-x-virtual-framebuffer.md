---
title: 'Xvfb (X virtual framebuffer)'
date: "2014-11-15 17:08:00"
comments: true
categories: 
---
最近才知道原來有 X virtual framebuffer 這種東西，可以在 Linux Server 端先把畫面 render 好，而 Client 端只要準備好 VNC Client，就可以連過去使用。啟動 X virtual framebuffer 與 x11vnc，並且開啟 window manager 與簡單的 gnome-panel 範例如下，初步試了一下滿順暢的(我跟server之間的 Round-trip time 約 38 ms)：

(以下範例的 vnc port 為6000，登入密碼為 pass)
``` bash
Xvfb :33 -screen 0 800x600x16 &
x11vnc -storepasswd pass ~/.vnc/passwd
x11vnc -display :33 -geometry 800x600 -rfbauth ~/.vnc/passwd -forever -rfbport 6000 -httpport 6001 &
export DISPLAY=:33
openbox-session &
gnome-panel &
```

Ref.
1. [fcwu/docker-ubuntu-vnc-desktop](https://github.com/fcwu/docker-ubuntu-vnc-desktop)
2. [Xvfb - Wikipedia](http://en.wikipedia.org/wiki/Xvfb)
