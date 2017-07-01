---
title: 'cURL HTTP redirects'
date: "2013-05-09 16:00:00"
comments: true
categories: 
---

cURL 是一個 unix 下以命令操作來取得檔案、頁面的工具，在網頁測試中經常使用到。不過要注意的是，cURL 預設並不處理 HTTP 重導向。

昨天在 github 上看到了一個有趣的專案 [screenshot-as-a-service](https://github.com/fzaninotto/screenshot-as-a-service/)，這個專案給使用者的第一個範例就是用 cURL 來進行操作。不過在 Readme.md 裡有點小錯誤。於是我就將它改正過來，並送了一個 Pull Request。
[revise usage example in Readme.md](https://github.com/fzaninotto/screenshot-as-a-service/pull/35)

今天發現作者已經將我的 patch 合併進了專案，有興趣的人可以抓下來試一試。


註：現今的網頁設計中，重導向至少有三種。

1. HTTP redirects
2. Redirects with HTML tag
3. Redirects with javascript

在 cURL 中，可以下參數讓 cURL 進行第1種 HTTP 重導向。至於第 2, 3 種，cURL 則是完全不支援。原因很簡單，就如同 cURL 最初的設計，是用來取得檔案、頁面用的。它並不是特別用來處理 HTML 的工具，所以這2類重導向就交給其它的工具去處理了。

Ref:

1. [How do I tell curl to follow HTTP redirects?](http://curl.haxx.se/docs/faq.html#How_do_I_tell_curl_to_follow_HTT)
2. [Redirects work in browser but not with curl!](http://curl.haxx.se/docs/faq.html#Redirects_work_in_browser_but_no)
