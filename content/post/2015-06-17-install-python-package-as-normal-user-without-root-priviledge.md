---
title: '一般使用者權限安裝 python package (無root 權限)'
date: "2015-06-17 16:01:00"
comments: true
categories: 
---
在一些工作站上，有時需要用到一些 python package，但不具有 root 權限時。Python 設定了一個方法，可以安裝在家目錄下的 .local/ 資料夾中

[Alternate installation: the user scheme — Python 2.7.10 documentatio](https://docs.python.org/2/install/index.html#alternate-installation-the-user-scheme)
``` bash
python setup.py install --user
```
之後再設定 PYTHONPATH, PATH 變數即可

``` bash
export PYTHONPATH=$HOME/.local/lib/python2.7/site-packages:$PYTHONPATH
PATH=$PATH:$HOME/.local/bin
export PATH
```