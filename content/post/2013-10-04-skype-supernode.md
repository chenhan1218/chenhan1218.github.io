---
title: 'Skype Supernode'
date: "2013-10-04 16:00:00"
comments: true
categories: 
---


今天讀了一些關於[UDP hole punching](http://en.wikipedia.org/wiki/UDP_hole_punching)，才知道原來VOIP這一類的技術，如何穿越NAT。

位在NAT後的A,B兩方要進行通話前，必須先透過一個STUN Server，取得對方於公開網路上的IP位址及PORT埠口，然後再進行[NAT Traversal](http://en.wikipedia.org/wiki/NAT_traversal)。

在Skype的實作中，本身具有Public IP位址的使用者，也可能擔任這個STUN server(Skype稱之為，Supernode)，分擔主伺服器的工作。因此，也需要耗用一些頻寬與運算效能。關於這點，台灣的網路追追追有訪問過Skype:

> 這個Super Node技術用在每種P2P的服務中，已經發展了8～9年，Skype是第一個將它運用於語音服務上，Skype挑選比較好的等級以及比較大的頻寬的用戶來當Super Node，並不會讓一個配備很差的電腦，還繼續拖垮它，而頻寬與資源佔用也只是一點點，集合眾多Super Node的力量完成。

不過在Microsoft買下Skype後，架構也有了調整，使用者將不再需要擔任STUN Server的角色，完全由微軟的伺服器來完成 Hole Punching 所需的資料交換。

Ref:

* [UDP hole punching](http://en.wikipedia.org/wiki/UDP_hole_punching)
* [NAT traversal](http://en.wikipedia.org/wiki/NAT_traversal)
* [VoIP 穿越防火牆的技術](http://www.cs.nccu.edu.tw/~lien/Writing/NGN/firewall.htm)
* Supernode <http://en.wikipedia.org/wiki/Supernode_(networking)>
* [網路追追追／用Skype到底安不安全？　PChome回應](http://rumor.nownews.com/2007/11/15/515-1728533.htm)
* [Skype replaces P2P supernodes with Linux boxes hosted by Microsoft](http://arstechnica.com/business/2012/05/skype-replaces-p2p-supernodes-with-linux-boxes-hosted-by-microsoft/)