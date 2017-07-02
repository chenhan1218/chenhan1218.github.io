---
title: 'debugging fork child process in GDB'
date: "2015-04-25 08:06:00"
comments: true
categories: 
---
剛在 python 遇到 subprocess 的問題，處理一陣子後突然想到，如果是 C++ 的話要怎麼用 GDB 來 debug. 查了文件後發現有2個方式：

1. 讓 child sleep 一段時間，手動取得 PID 後，再讓 GDB attach 上去

這個方式可以想的到，有點暴力解的感覺。看來處理 multi-process 真的沒什麼好方法。
2. 設定 follow-fork-mode

GDB 預設只會 attach 在 parent process 上，而不會控制 child process。但如果將 follow-fork-mode 設為 child，那在 fork() 之後，parent process 將不受 GDB 控制，只有 child process 在 GDB 的控制中。換句話說，同一時間只有一個 process 會被 attached。
```bash
set follow-fork-mode parent
# The original process is debugged after a fork. The child process runs unimpeded. This is the default. 
set follow-fork-mode child
#The new process is debugged after a fork. The parent process runs unimpeded.
```

由 folow-fork-mode 還延伸出 detach-on-fork，預設值開啟代表沒被 attached 的 process 會獨立的運作。關閉代表沒被 attached 的 process 會被 suspend。

Ref: [Forks - Debugging with GDB](https://sourceware.org/gdb/onlinedocs/gdb/Forks.html)
