---
title: 'python3 UnicodeDecodeError'
date: "2015-04-16 10:08:00"
comments: true
categories: 
---
遇到 python UnicodeDecodeError 其實有點頭大。

``` python
#!/usr/bin/python3
# -*- coding: utf-8 -*-

import subprocess
import os
import sys
import locale

if __name__ == "__main__":
	locale.setlocale(locale.LC_ALL, 'en_US.UTF8')
	proc = subprocess.Popen(['date'], stdout=subprocess.PIPE,
									 stderr=subprocess.PIPE,
									 stdin=subprocess.PIPE,
									 env={'LANG': 'zh_TW.UTF8', 'LANGUAGE': 'zh_TW:zh'},
									 universal_newlines=True, shell=True)
	(out, err) = proc.communicate()
	import codecs
	sys.stdout = codecs.getwriter("utf-8")(sys.stdout.detach())
	print(out)
	print(err)
```

``` bash
$ ./date.py
```

再進一步查了一下，發現這跟環境變數有關。
```
$ env -i LANG='en_US.UTF8' /usr/bin/python3 -c 'import locale; print(locale.getpreferredencoding(False))'               
UTF-8
$ env -i  /usr/bin/python3 -c 'import locale; print(locale.getpreferredencoding(False))'
ANSI_X3.4-1968
```

看完這份 slides ，才比較知道 Unicode 在 Python 中較好的處理方法 [Unicode In Python, Completely Demystified](http://farmdev.com/talks/unicode/)

>Solution
1. Decode early
2. Unicode everywhere
3. Encode late

或是類似 Ubiquity 的直接強制使用 C.UTF
[http://bazaar.launchpad.net/~ubuntu-installer/ubiquity/trunk/view/head:/bin/ubiquity#L44](http://bazaar.launchpad.net/~ubuntu-installer/ubiquity/trunk/view/head:/bin/ubiquity#L44)
