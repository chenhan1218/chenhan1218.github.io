---
title: '用python fcntl 取得 file lock'
date: "2014-09-23 05:01:00"
comments: true
categories: 
---
在 Stack Overflow 上看到的問答。稍微修改了一下為可執行的版本，下面的Python程式碼可以對一個檔案做lock。同時執行2個這樣的 python script，先取得 file lock 的 process 可以順利印出 "No error"，沒取得 file lock 的 process 則會得到 IOError, 印出 "can't immediately lock the file" 後結束程式。
``` python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
import fcntl
import time
f = open('/tmp/locktest', 'r')
try:
    fcntl.flock(f, fcntl.LOCK_EX | fcntl.LOCK_NB)
except IOError:
    print("can't immediately lock the file")
else:
    print("No error")
    time.sleep(10)
f.close()
```

先取得 file lock 的 process：
``` bash
# python test.py
No error
```

沒取得 file lock 的 process：
``` bash
# python test.py
can't immediately lock the file
```
離 Python System Programming 更近一步了!

Ref: [Python fcntl does not lock as expected](http://stackoverflow.com/questions/9907616/python-fcntl-does-not-lock-as-expected)