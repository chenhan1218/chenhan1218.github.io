---
title: 'mozmill-tests debugging'
date: "2014-04-30 13:29:00"
comments: true
categories: 
---
之前曾經想幫忙解 Mozilla 上的一個 first good bug，可惜 patch 送過去來來回回很多次後，後來沒空能完成它。不過過程中學到很多在 mozmill-tests 這項專案上 debug 的技巧。這邊做一下記錄。

## 編寫 mozmill-tests 的 module 時，可運用 controller.window.dump 輸出訊息
``` javascript
controller.window.dump("message")
```

## 使用 mozmill-tests 時，搭配 Firefox Nightly Build (約29.0版) 與 javascript debugger 的方式：
``` bash
mozmill -t firefox/lib/tests/testFindBar.js -b ~/Downloads/FirefoxNightly.app/ --show-errors -a javascript_debugger-0.9.89-sm+tb+fx.xpi --app-arg=-venkman
```
