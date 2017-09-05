+++
css = []
date = "2017-08-09T19:12:42+08:00"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "autostart x11vnc in gnome-session"

+++

```
$ cat ~/.config/autostart/x11vnc.desktop
[Desktop Entry]
Type=Application
Exec=sh -c "/usr/bin/x11vnc -auth $XAUTHORITY -rfbauth $HOME/.x11vnc/passwd -forever -shared -bg --noxfixes -noxrecord -noxdamage -rfbport 5900 -display $DISPLAY -o $HOME/.x11vnc/vnc_server.log"
Hidden=false
NoDisplay=false
X-GNOME-Autostart-enabled=true
Name[en_US]=x11vnc
Name=x11vnc
Comment[en_US]=
Comment=
```
