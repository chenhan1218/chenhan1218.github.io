---
title: 'Mutex VS Spinlock'
date: "2014-02-07 04:10:00"
comments: true
categories: 
---
這篇發問的最佳回答 [When should one use a spinlock instead of mutex?](http://stackoverflow.com/questions/5869825/when-should-one-use-a-spinlock-instead-of-mutex) 說明了 mutex 與 spinlock 的不同。 
mutex 的機制是當 process 無法鎖定 mutex 時，process 會進入 sleep，中間會需要付出 context switch 的代價。spinlock 的機制是採用 busy-waiting，直到鎖定 spinlock 為止。
依據兩者的特性，一般來說，在單核心的系統中，會採用 mutex。而多核心，且 critical section 只耗用一小段時間的狀況下，適合使用 spinlock。  
解答者 Mecki 還補充了實務上的狀況。由於要預期應用情境下的 lock 狀況相當困難，現代的作業系統中也加入一些機制增加彈性，發展出了 hybrid mutex, hybrid spinlock。當 process 無法鎖住 hybrid mutex 時，作業系統不會馬上讓 process 進入睡眠，而是以類似 spinlock 的方式 busy-waiting 一小段時間，確定真的無法鎖住 hybrid mutex，才讓 process 進入睡眠。而當 process 無法鎖住 hybrid spinlock 時，作業系統會允許 process 進行 busy-waiting。但超過某個時間限制，則會讓 process 進入睡眠，讓其它 thread 運作。

[pthread mutex vs pthread spinlock](http://www.alexonlinux.com/pthread-mutex-vs-pthread-spinlock) 這篇文章則是給出實作，實際表現出在多核環境，且critical section佔用極小時間的情況下，pthread spinlock 的表現優於 pthread mutex

More Link: [Jserv - Mutex與火車排班](http://orzlab.blogspot.tw/2007/03/mutex.html)