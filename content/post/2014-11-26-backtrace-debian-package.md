---
title: 'backtrace debian package'
date: "2014-11-26 06:13:00"
comments: true
categories: 
---
``` bash
$ apt-cache search hello | grep dbg
```

```
# apt-get install hello-dbg
gdb /usr/bin/hello
```
- [HowToGetABacktrace - Debian Wiki](https://wiki.debian.org/HowToGetABacktrace)