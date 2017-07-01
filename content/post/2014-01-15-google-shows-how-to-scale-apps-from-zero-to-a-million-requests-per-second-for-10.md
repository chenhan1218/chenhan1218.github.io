---
title: 'Google Shows How To Scale Apps From Zero To A Million Requests Per Second, For $10'
date: "2014-01-15 12:52:00"
comments: true
categories: 
---
[Google Shows How To Scale Apps From Zero To A Million Requests Per Second, For $10](http://www.forbes.com/sites/reuvencohen/2013/11/26/google-shows-how-to-scale-apps-from-zero-to-one-million-requests-per-second-for-10/)
你可以在 7分半鐘的時間內，利用他們的工具架出一套架構，包含一台 load balance, 數百台 apache server
可以接受 1M/second 的 Request.

等於是自已加 64台機器當 client, 用 curl 每秒發送 1M http request
然後架一台 load balance, 200台 apache server，當做server 來接收 request
用這樣的方式來模擬網路服務