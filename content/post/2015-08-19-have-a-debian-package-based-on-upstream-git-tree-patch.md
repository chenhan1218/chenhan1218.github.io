---
title: '基於 upstream git-tree 產生 debian package patch'
date: "2015-08-19 03:21:00"
comments: true
categories: 
---
最近在工作上遇到一個 bug，在某些狀況下執行 lshw (02.16-2ubuntu1.2) 會 segmentation fault。找了 [lshw](https://github.com/lyonel/lshw) 最新的 code 編譯執行後發現沒有這個問題。於是就開始了 git bisect。最後找到是 [d048d300b5daeb44887a7fc06ddeb120119cac8a](https://github.com/lyonel/lshw/commit/d048d300b5daeb44887a7fc06ddeb120119cac8a) 這筆修改在 src/core/scsi.cc 上面的 commit 解決了這個問題

順著這筆 commit，找到了 lshw project 的 bug report [lshw segfaults, with some 16GB USB-3 sticks from Patriot](http://www.ezix.org/project/ticket/653) 。也了解是 USB3.0 stick plugged 時會出現問題。在手上的機器上試了一下，果然是這樣沒錯。原本沒有頭緒的 random segmentation fault，現在則是有了 root cause 的 issue。

既然找到了 Solution，就開始要加 patch 進 Ubuntu source 了。為了將 patch 加到 Ubuntu 14.04 (Trusty) 目前的 lshw (02.16-2ubuntu1.2) 裡，我們還必須加上 src/core/scsi.cc 的前一個 commit [b79f299319f61bc80e8d38e61631cfee7521a729](https://github.com/lyonel/lshw/commit/b79f299319f61bc80e8d38e61631cfee7521a729) 
``` bash
# clone upstream
git clone https://github.com/lyonel/lshw lshw-lyonel
# clone ubuntu source
bzr branch lp:ubuntu/trusty-proposed/lshw

# make patch from upstream git tree
cd lshw-lyonel/
git format-patch b79f299^..b79f299
git format-patch d048d30^..d048d30
cd ..

# import patches to ubuntu source
cd lshw/
dquilt push -a # apply existing patches
dquilt import ../lshw-lyonel/0001-use-a-different-approach-for-scanning-SCSI-generic-d.patch
dquilt import ../lshw-lyonel/0001-presumably-fix-653.patch

# edit changelog
dch -v 02.16-2ubuntu1.3 -D trusty

# local commit
debcommit
```

這樣就完成了，最後這一包 source 就可以拿來做 debian package 的打包，並且開始跑 Ubuntu package propose 的流程。

Ref: 
1. [how to add upstream git patches to an existing debian package](https://xpressubuntu.wordpress.com/2013/11/27/how-to-add-upstream-git-patches-to-an-existing-debian-package/)
2. [Chapter 3. Modifying the source](https://www.debian.org/doc/manuals/maint-guide/modify.en.html)
3. [How To Survive With Many Patches or Introduction to Quilt](https://stuff.mit.edu/afs/athena/system/i386_deb50/os/usr/share/doc/quilt/quilt.html)