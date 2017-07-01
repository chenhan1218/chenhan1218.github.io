---
title: 'Openfire 即時訊息伺服器'
date: "2014-07-09 10:08:00"
comments: true
categories: 
---
最近嘗試使用 Openfire，來架構私人使用的即時訊息server。 Openfire 是一套使用 xmpp protocol 的開源軟體，安裝上也非常簡單，提供有 deb 安裝檔。在 Debian/Ubuntu 上很快就可以安裝好了。之後就可以透過 9090 port 登入 admin 帳號進行設定。

這裡分享一下我設定的心得，我架設的是單一伺服器。假設我決定 xmpp domain 為 openfire.example.io，那麼就必須把 dns 設定好，讓 openfire.example.io 指向安裝有 openfire 的機器。並且在 Openfire 的軟體設定， xmpp.domain 的值設定為 openfire.example.io。之後再新增 user1, user2 的帳號，就可以讓雙方(user1@openfire.example.io, user2@openfire.example.io )相互傳訊息。 Client端我是使用 [Xabber](http://www.xabber.org/) on Android, [Jitsi](https://jitsi.org/) on Ubuntu14.04

如果手上沒有 domain，xmpp domain也是可以直接設定成 ip ，像是 192.168.0.2。

另外，Openfire也有 Group Chat Rooms 的功能，很方便大家在同一個頻道上加入討論。

之後希望可以看看 Openfire 是否能再結合 libjingle 做到 VOIP 的功能。如果可以的話，我想會是很棒的私人訊息軟體。

Ref:
[How To Install Openfire XMPP Server on a Debian or Ubuntu VPS](https://www.digitalocean.com/community/tutorials/how-to-install-openfire-xmpp-server-on-a-debian-or-ubuntu-vps)

註：不過目前還有個小問題，client雙方可以互相傳文字訊息，卻看不到對方上線。看其它網友也有遇到相同狀況，之後有空再來看怎麼解決