---
title: 'GNU Autotools自動編譯'
date: "2014-08-30 07:32:00"
comments: true
categories: 
---
在開發 Open Source 項目時，經常會遇到 Autotools。翻了一下網路文章，覺得這張圖給出不錯的表示。
[瘋狂駭客的技術隨筆 - 使用GNU Autotools自動編譯項目](http://www.cnblogs.com/crazyhack/archive/2011/12/17/2291410.html)

![Autotool](http://images.cnblogs.com/cnblogs_com/crazyhack/201112/201112172255386655.png)

> 圖中橢圓形狀的就是gnu autotools里的主要工具了，包括１autoscan２aclocal３autoheader４automake５autoconf等.而方形形狀只有Makefile.am和configure.ac是需要我們寫的，别的方框里除了Makefile是最終的配置文件，其它都是中間文件。(Makefile文件是由６configure生成的)

Ref: [http://en.wikipedia.org/wiki/Autoconf](http://en.wikipedia.org/wiki/Autoconf)