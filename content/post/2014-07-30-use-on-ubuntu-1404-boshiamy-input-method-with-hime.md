---
title: 'Ubuntu 14.04 上使用嘸蝦米輸入法 with hime'
date: "2014-07-30 05:12:00"
comments: true
categories: 
---
Facebook [Ubuntu 正體中文社團](https://www.facebook.com/groups/ubuntu.zh.hant/711655822223076/) 上有人提問如何在 Ubuntu 14.04 上使用嘸蝦米輸入法。我的回應看來有幫忙解決問題了，順手貼在自己的部落格供大家參考。

14.04上面可以安裝 hime (有hime-chewing套件提供注音輸入) ，安裝好以後把嘸蝦米字典檔放到 ~/.config/hime/ ，再用 im-config 把預設輸入法改為 hime 即可.

hime 細部設定可以用 hime-setup

====================

Update: "發現在 Ubuntu 14.04 上使用 fcitx 更為方便，也不需要準備字典檔。安裝方式::00"
``` bash
sudo apt-get install fcitx-table-boshiamy
```
另外可以再安裝 fcitx 注音輸入法
``` bash
sudo apt-get install fcitx-chewing
```
進入 System Settings 的 Lauguage Support 設定輸入法為 fcitx 後，登出再登入即可。
