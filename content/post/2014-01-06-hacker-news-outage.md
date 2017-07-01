---
title: 'Hacker News outage'
date: "2014-01-06 16:00:00"
comments: true
categories: 
---
精神、技術食糧 Hacker News 這兩天突然出現問題無法運作。連到 Hacker News 就會傳回一個頁面表示正在維修中。但仔細探究回傳的訊息，會發現其中不恰當的地方。有網友寫了一篇 [HackerNews down, unwisely returning http 200 for outage message](http://bibwild.wordpress.com/2014/01/06/hackernews_http_200_outage/)，我簡短做個摘要。

首先，維修頁面回傳了 HTTP 200 的 status code，這樣的訊息表示伺服器正常的回應。但一個正在維修的頁面，不應該回傳 HTTP 200。否則，這樣的頁面會被視為資料而被快取下來。以Google 為例，他會保有一些 webpage cache。如果Google 沒有更進一步判讀這其實是維修頁面，那這個記錄就會留存。任何像 Google 這樣的搜尋服務或是第3方服務都會受到影響。比較好的做法是回傳 503 Service Temporarily Unavailable 的 status code.

第二，這個維修頁面的 expire time 太久了，設置的 expire time 到 Thu, 04 Jan 2024 13:14:48 GMT，也就是10年之後。換句話說如果一個使用者或 http proxy 沒有進行 hard refresh，即使 Hacker News 恢復運作，當使用者造訪 Hacker News 的時候，他看到的仍然會是這個維修頁面。

第二個問題其實也是因為第一個問題造成的，如果使用適當的 status code，那就不會有 expire 的 issue。