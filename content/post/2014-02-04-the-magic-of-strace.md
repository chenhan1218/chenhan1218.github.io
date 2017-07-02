---
title: 'The Magic of Strace'
date: "2014-02-04 03:22:00"
comments: true
categories: 
---
過年讀了這篇 [The Magic of Strace](http://chadfowler.com/blog/2014/01/26/the-magic-of-strace/) ，裡面介紹了使用 strace 來追蹤 unix 下的程序使用 system call 的運作情況。觀察 process 對 system call 的呼叫，包括 file read/write, database read/write, Inter-process communication，可以找出其中出現的 bug, error 。對於某些很難重現的錯誤，可以藉由 strace 進行 log 。下次在 unix 上多個工具可以試試了。

updata: [Understanding how killall works using strace](http://jvns.ca/blog/2013/12/22/fun-with-strace/) 這篇文章也很有意思，利用 strace 去追蹤 killall 的流程。  
首先 killall 爬過所有 process 的 stat (/proc/$PID/stat)，找到相同的 process name 就把 PID 送進 kill system call。  
最後底下推文回應還提到了 ltrace，可用來追蹤 library call，以及一份關於 /proc 的文件 [THE /proc FILESYSTEM](https://www.kernel.org/doc/Documentation/filesystems/proc.txt)