---
title: 'Comparing two Git Branch with common ancestor'
date: "2014-08-26 10:16:00"
comments: true
categories: 
---
今天在c9s的 facebook 上看到這個，才發現有這種用法。

http://stackoverflow.com/questions/9834689/comparing-two-branches-in-git 
原來還有這種用法 two dots 跟three dots 是不一樣的

```
# produce the diff between the tips of the two branches.
git diff branch_1..branch_2
# use three dots instead of two to find the diff from their common ancestor
git diff branch_1...branch_2
```