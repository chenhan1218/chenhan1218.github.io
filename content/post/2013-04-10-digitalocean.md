---
title: 'DigitalOcean 初體驗'
date: "2013-04-10 07:02:00"
comments: true
categories: 
---


前幾天剛好有虛擬機器的需要，所以上 [DigitalOcean](https://www.digitalocean.com) 開了一台最便宜的來試試。

架設 Server 十分容易，方案選一下，信用卡開下去就有了。
設備：512MB Memory, 1 Core, 20GB SSD Disk, 1TB Transfer

我選在 New York 的 Data Center，從台灣連過去的 Latency 大約是230ms。差強人意，但以我的用途可接受。
使用12小時花了 $0.09 美元，實在是非常划算。

後來因為用不到了，所以把機器做了個 Snapshot，然後就把機器刪除了。
這樣就不會產生任何花費。等到以後需要再從 Snapshot 重新建一台 Server 回來用就好。

能夠以使用時數計費，還有價格相對於 [Linode](http://www.linode.com/) 便宜，是我選擇 DigitalOcean 的原因。

Ref[1]: [DigitalOcean 與 Linode 的比較…](http://blog.gslin.org/archives/2013/02/13/3203/digitalocean-%E8%88%87-linode-%E7%9A%84%E6%AF%94%E8%BC%83/)

Ref[2]: [Linode vs DigitalOcean, performance benchmarks](http://jasonormand.com/2013/02/08/linode-vs-digitalocean-performance-benchmarks/)