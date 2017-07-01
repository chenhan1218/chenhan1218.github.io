---
title: 'File Descriptor in Bash Shell'
date: "2013-05-08 16:00:00"
comments: true
categories: 
---

一個程式至少會開啟三個Input/Output 串流，分別為

1. Standard input (stdin)  標準輸入
2. Standard output (stdout) 標準輸出
3. Standard error (stderr) 標準錯誤訊息

操作時相對應的代號就是file descriptor。

在 Bash Shell 中，你最多可以有10個 file descriptor。利用這些 descriptor，你可以結合他們把輸出訊息、錯誤訊息，都導到同一個檔案中，並同時在螢幕上顯示出來。

## I/O redirection 的順序性

在進行 I/O redirection 的時候，要注意順序性 (If redirecting both stdout and stderr, the order of the commands makes a difference.)。
以下2個命令是不同的。
```
$ sh script.sh >log.txt 2>&1
$ sh script.sh 2>&1 >log.txt
```
-第1個命令，將stdout 導向 log.txt，然後stderr 導向 stdout。如此一來，stderr 也將導入 log.txt。
-第2個命令，將stderr 導向 stdout，然後原先的stdout 導向 log.txt。此時log.txt 只會包含 stdout

進階應用的話可以參考 Fourdollars 的文章[關於 Bash 的 Redirection 使用的心得](http://fourdollars.blogspot.tw/2013/03/bash-redirection.html)。
裡面提到了如何將標準輸出訊息跟標準錯誤訊息都導進 fdisk.log 裡面，然後將標準錯誤訊息顯示出來。

Ref:

1. [關於 Bash 的 Redirection 使用的心得](http://fourdollars.blogspot.tw/2013/03/bash-redirection.html)
2. [File descriptor與I/O導向](http://www.study-area.org/cyril/scripts/scripts/node32.html)
3. [Advanced Bash-Scripting Guide: Chapter 20. I/O Redirection](http://www.tldp.org/LDP/abs/html/io-redirection.html)
