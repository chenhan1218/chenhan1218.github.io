+++
css = []
date = "2017-08-30T16:04:13+08:00"
description = ""
draft = false
highlight = true
scripts = []
tags = []
title = "disable suspend via polkit"

+++

https://gist.github.com/schlomo/183524530d17d6a888d0

/var/lib/polkit-1/localauthority/50-local.d/disable-suspend.pkla
```
[Completely disable suspend and hibernate]
Identity=unix-user:*
Action=org.freedesktop.upower.suspend;org.freedesktop.upower.hibernate;org.freedesktop.login1.suspend*;org.freedesktop.login1.hibernate*
ResultAny=no
ResultInactive=no
ResultActive=no
```
