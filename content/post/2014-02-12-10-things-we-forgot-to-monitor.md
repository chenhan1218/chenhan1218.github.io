---
title: '10項系統監控'
date: "2014-02-12 03:36:00"
comments: true
categories: 
---
[10 Things We Forgot to Monitor](http://word.bitly.com/post/74839060954/ten-things-to-monitor)
在做系統監控時，我們常想到Disk Usage, Memory Usage, CPU Load, Ping latency。[bitly](https://bitly.com/)的工程師 Jehiah 分享10項有用但平常少提及的系統監控項目，有些項目甚至附上了 script 供 Devops 參考。

1. Fork Rate
  - 異常的 Fork Rate 可能表示系統設置有問題。作者舉了一個例子，某次系統設置錯誤， curl 不斷觸發 modprobe
2. flow control packets
  - 確定網路流量管控機制的設定不會使得系統在某一時刻停止接受封包
3. Swap in/out rate
  - 藉由記錄 [vmstat](http://en.wikipedia.org/wiki/Vmstat) 的數據, 推算 swap in/out rate，確定系統流暢
4. Server Boot Notification
  - 系統重開機時，寄email給管理員
5. NTP Clock Offset
  - 確定 ntpd 在背景執行，並且記錄機器時鐘誤差，以及機房時間伺服器與外部的時鐘誤差
6. DNS Resolutions
  - 監控內部 DNS Resolutions 狀態，也監控外部 nameserver 的穩定性
7. SSL Expiration
  - 在 SSL 快過期前發出通知
8. DELL OpenManage Server Administrator (OMSA)
  - 購買硬體伺服器所需做的監控
9. Connection Limits
  - 了解系統並確定限制連線設定符合需求，作者這邊給的限制是 65536
10. Load Balancer Status.
  - Load Balancer health check

附註：看到 Hacker News 推文中有人另外列出一個也滿值得監控的數值： file descriptors 的最大數量
